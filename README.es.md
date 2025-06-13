<!-- hide -->
# Construyendo y Asegurando una Red con una DMZ

> Por [@vanemorocho](https://github.com/vanemorocho) y [otros colaboradores](https://github.com/breatheco-de/commands-for-remote-hacking/graphs/contributors) en [4Geeks Academy](https://4geeksacademy.co/)

*Estas instrucciones [están disponibles en 🇪🇸 español](https://github.com/4GeeksAcademy/installing-windows-on-virtual-machine/blob/main/README.es.md) :es:*
<!-- endhide -->

Este laboratorio está diseñado para que los estudiantes adquieran competencias fundamentales en ciberseguridad defensiva, mediante la configuración de una Zona Desmilitarizada (DMZ) en Cisco Packet Tracer. El objetivo es:

- Aislar servicios críticos (DMZ)
- Controlar de tráfico mediante ACLs
- Exponer de forma controlada servicios web
- Configuración segura de NAT


### ⚠️ Nota Importante para el Estudiante
Este ejercicio ha sido diseñado con una estructura paso a paso para ayudarte a comprender cómo se configura y protege una red con DMZ de forma correcta y segura. **Es muy importante que sigas con precisión las instrucciones proporcionadas,** especialmente el plan de direccionamiento IP y los comandos indicados.

   > Usar otras IPs o cambiar el orden de configuración puede romper la conectividad, impedir el funcionamiento del NAT o invalidar las ACLs.

*Más adelante podrás practicar creando una DMZ libre, diseñando tu propia topología y reglas de acceso. Pero en este laboratorio, el objetivo es que comprendas primero la lógica y los fundamentos siguiendo un modelo controlado.*

## 🌱 ¿Cómo empezar este proyecto?

[Descarga aquí](https://github.com/breatheco-de/Building-and-Securing-a-Network-with-a-DMZ/raw/main/assets/DMZ_PROJECT.pka) el archivo y ábrelo con Packet Tracer.

Una vez que hayas abierto el archivo con Packet Tracer, verás una ventana flotante con instrucciones a seguir.

## 📝 Instrucciones

Al comenzar este laboratorio, **no necesitarás crear ni cablear la red desde cero**. Ya se te proporciona una **topología funcional prehecha** en Packet Tracer para que puedas concentrarte en lo más importante: la **configuración de seguridad**.


### Topología del laboratorio

**Router Central (`Router_FW`): Cisco ISR 2911**

- `GigabitEthernet0/0` conectado a `SW_Internal` (red LAN)  
- `GigabitEthernet0/1` conectado a `SW_DMZ` (red DMZ)  
- `GigabitEthernet0/2` conectado a `SW_External` (red externa / internet)  

**Switches Cisco 2960:**

- `SW_Internal` conecta al `PC_Internal`  
- `SW_DMZ` conecta al `Server-PT Web_DMZ`  
- `SW_External` conecta al `PC_External`  

**Dispositivos finales:**

- `PC_Internal` (usuario en red LAN)  
- `Server-PT Web_DMZ` (servidor web en la DMZ)  
- `PC_External` (usuario externo simulando internet)  

### ¿Qué debes hacer tú?

Tu tarea consistirá en **completar la configuración lógica** de esta red prehecha. Deberás:

1. **Asignar direcciones IP** a todos los dispositivos finales y al router.  
   Esto garantiza que cada zona (LAN, DMZ, Externa) tenga conectividad básica.

2. **Configurar NAT estático** en el router, para que el servidor DMZ pueda ser accesible desde el exterior.  
   > El uso de NAT es una técnica clave para ocultar direcciones privadas y exponer servicios públicos de forma controlada.

3. **Aplicar Listas de Control de Acceso (ACLs)** para restringir el tráfico entre las zonas.  
   > Las ACLs simulan un firewall, bloqueando accesos no autorizados y permitiendo solo lo necesario para cada rol.

4. **Realizar pruebas de validación funcional**:
   - Pings desde distintos puntos de la red
   - Acceso HTTP desde la red externa al servidor
   - Verificar que ciertos accesos estén **bloqueados**, como el intento de conexión desde la DMZ hacia la LAN (INTERNAL_NETWORK)

Estas pruebas simulan situaciones reales de seguridad, donde se verifica que solo se permita el tráfico legítimo y se bloquee el malicioso o innecesario.


## 🚛 ¿Cómo entregar este proyecto?

Una vez que hayas finalizado los pasos de instrucción de Packet Tracer, deberás guardar tu archivo y preparar un informe técnico siguiendo la plantilla oficial proporcionada [plantilla del informe](https://github.com/breatheco-de/Building-and-Securing-a-Network-with-a-DMZ/raw/main/assets/report_DMZ.es.md). **¡Importante!** Usa la plantilla como guía para redactar tu informe. No se aceptarán entregas sin estructura o incompletas.

1. Crea un repositorio público en tu cuenta de GitHub con el nombre `dmz-lab` (o similar).
2. Sube los siguientes archivos:
   - Tu archivo final de Packet Tracer.
   - `informe/Informe_DMZ_Laboratorio.md`: el informe completado usando la plantilla.
   - `evidencias/`: capturas de pantalla de las pruebas realizadas.
3. Agrega un `README.md` que explique brevemente el objetivo del laboratorio y los contenidos del repositorio.
4. **Entrega el enlace del repositorio en la plataforma 4Geeks.**


<!-- hide -->
## Colaboradores

Gracias a estas maravillosas personas ([clave de emojis](https://github.com/kentcdodds/all-contributors#emoji-key)):

1. [Vanessa Morocho (vanemorocho)](https://github.com/vanemorocho) contribución: (construir tutorial) ✅, (documentación) 📖
  
2. [Alejandro Sanchez (alesanchezr)](https://github.com/alesanchezr), contribución: (reportes de bugs) 🐛

Este y muchos otros ejercicios son creados por estudiantes como parte del [Bootcamp de Ciberseguridad](https://4geeksacademy.com/us/coding-bootcamps/cybersecurity) de 4Geeks Academy por [Alejandro Sánchez](https://twitter.com/alesanchezr) y muchos otros colaboradores. Descubre más sobre nuestro [Curso de Desarrollador Full Stack](https://4geeksacademy.com/us/coding-bootcamps/part-time-full-stack-developer) y el [Bootcamp de Ciencia de Datos](https://4geeksacademy.com/us/coding-bootcamps/datascience-machine-learning).

<!-- endhide -->
