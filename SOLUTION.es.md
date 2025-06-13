
# Configuración de Zona Desmilitarizada (DMZ) con Router Cisco

Configurar una Zona Desmilitarizada (DMZ) utilizando un router Cisco ISR para alojar un servidor web, permitiendo acceso controlado desde la red externa y la red interna, mientras se aísla la red interna de la DMZ.


## Topología del Laboratorio

- **Router Central (Router_FW)**: Cisco ISR (ej. 2911 o 4331)
  - GigabitEthernet0/0 (LAN) -> SW_Internal
  - GigabitEthernet0/1 (DMZ) -> SW_DMZ
  - GigabitEthernet0/2 (External) -> SW_External

- **Switches**: 3x Cisco 2960 (o 2960 IOS15)

- **Dispositivos Finales**:
  - PC_Internal (en SW_Internal)
  - Server-PT Web_DMZ (en SW_DMZ)
  - PC_External (en SW_External)


## Paso 1: Plan de Direccionamiento IP

### PC_Internal:
```
IP Address: 192.168.1.10
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.1.1
DNS Server: 0.0.0.0
```

### Server-PT Web_DMZ:
```
IP Address: 192.168.2.10
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.2.1
DNS Server: 0.0.0.0
```

### PC_External:
```
IP Address: 192.168.3.10
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.3.1
DNS Server: 0.0.0.0
```

---

## Paso 2: Configuración de Interfaces en el Router (Router_FW)

```bash
Router> enable
Router# configure terminal

Router_FW(config)# interface GigabitEthernet0/0
Router_FW(config-if)# ip address 192.168.1.1 255.255.255.0
Router_FW(config-if)# no shutdown
Router_FW(config-if)# exit

Router_FW(config)# interface GigabitEthernet0/1
Router_FW(config-if)# ip address 192.168.2.1 255.255.255.0
Router_FW(config-if)# no shutdown
Router_FW(config-if)# exit

Router_FW(config)# interface GigabitEthernet0/2
Router_FW(config-if)# ip address 192.168.3.1 255.255.255.0
Router_FW(config-if)# no shutdown
Router_FW(config-if)# exit

Router_FW(config)# end
Router_FW# write memory
```


## ✅ Paso 3: Verificación de Conectividad Básica

Realiza `ping` desde cada dispositivo a su gateway. Todos deben devolver `Replies`.

Si falla:
- Verifica IP, máscara y gateway.
- Usa `show ip interface brief` en el router.
- Verifica puertos en los switches (`show interface status`).
- Asegura que los cables sean correctos y estén conectados (indicadores verdes).



## Paso 4: Configuración de NAT Estático en el Router

```bash
Router_FW(config)# interface GigabitEthernet0/1
Router_FW(config-if)# ip nat inside
Router_FW(config)# interface GigabitEthernet0/2
Router_FW(config-if)# ip nat outside
Router_FW(config)# ip nat inside source static 192.168.2.10 192.168.3.1
Router_FW# write memory
```


## Paso 5: Activar Servicios Web en el Servidor DMZ

- Activa HTTP y HTTPS desde la pestaña `Services`.
- (Opcional) Personaliza `index.html`.


## Paso 6: Pruebas de Acceso Web Inicial

Desde PC_External:
- Accede a `http://192.168.3.1`

Desde PC_Internal:
- Accede a `http://192.168.2.10`

## 🔒 Paso 7: Configuración de ACLs para Seguridad

```bash
Router_FW# configure terminal

! ACL 101 - tráfico desde exterior a DMZ
no access-list 101
ip access-list extended 101
10 permit icmp any any
20 permit tcp any host 192.168.3.1 eq 80
30 permit tcp any host 192.168.3.1 eq 443
exit

! ACL 100 - tráfico desde DMZ hacia LAN e Internet
ip access-list extended 100
10 permit icmp any 192.168.1.0 0.0.0.255 echo-reply
20 permit tcp any 192.168.1.0 0.0.0.255 established
30 permit tcp any 192.168.3.0 0.0.0.255 established
40 permit icmp any 192.168.3.0 0.0.0.255 echo-reply
50 deny ip 192.168.2.0 0.0.0.255 192.168.1.0 0.0.0.255
60 permit ip any any
exit

! Aplicar ACLs a interfaces
interface GigabitEthernet0/1
ip access-group 100 in
exit

interface GigabitEthernet0/2
ip access-group 101 in
exit

end
write memory
```

---

## 🔍 Paso 8: Verificación Final de Seguridad

Desde PC_External:
- `ping 192.168.3.1` → debería funcionar (por regla temporal)
- Navegar a `http://192.168.3.1` → debe cargar página

Desde PC_Internal:
- `ping 192.168.2.10` → debe responder
- `telnet 192.168.2.10 80` → debe conectar

Desde Server-PT Web_DMZ:
- `ping 192.168.1.10` → debe fallar
- `telnet 192.168.1.10 80` → debe fallar

---

## 🛡️ Paso 9: Buenas Prácticas (Eliminar ICMP en Producción)

```bash
Router_FW# configure terminal
ip access-list extended 101
no 10
end
write memory
```

Verifica que el `ping` desde PC_External a `192.168.3.1` ahora falle, pero el acceso web funcione.
