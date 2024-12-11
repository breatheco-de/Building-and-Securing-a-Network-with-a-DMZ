<!-- hide -->
# Construyendo y Asegurando una Red con una DMZ

> Por [@vanemorocho](https://github.com/vanemorocho) y [otros colaboradores](https://github.com/breatheco-de/commands-for-remote-hacking/graphs/contributors) en [4Geeks Academy](https://4geeksacademy.co/)

*Estas instrucciones [están disponibles en 🇪🇸 español](https://github.com/4GeeksAcademy/installing-windows-on-virtual-machine/blob/main/README.es.md) :es:*
<!-- endhide -->

<onlyfor saas="false" withBanner="false">

## 🌱 ¿Cómo empezar este proyecto?

[Descarga aquí](https://github.com/breatheco-de/Building-and-Securing-a-Network-with-a-DMZ/raw/main/assets/ProjectDMZ.pka) el archivo y ábrelo con Packet Tracer.

Una vez que hayas abierto el archivo con Packet Tracer, verás una ventana flotante con las instrucciones a seguir.

</onlyfor>

## 📝 Instrucciones

Crea un entorno de red simulado que incluya una Zona Desmilitarizada (DMZ), configura firewalls, gateways y sistemas de detección de red, y garantiza la seguridad de la red.

### Componentes:

1. **Diseño de Red:**
   - Diseña un esquema de red que incluya una DMZ, red interna y red externa.
   - Configura máquinas virtuales o utiliza una herramienta de simulación de red para crear el entorno.

2. **Configuración del Firewall:**
   - Configura firewalls para segmentar la red en redes DMZ e internas.
   - Establece reglas de firewall para controlar el tráfico entre la red interna, la DMZ y la red externa.

3. **Configuración de la DMZ:**
   - Despliega servicios en la DMZ como un servidor web, servidor de correo o servidor DNS.
   - Asegura que la DMZ esté aislada de la red interna pero sea accesible desde la red externa.

4. **Gateway o Servidor Proxy:**
   - Configura un gateway o servidor proxy para gestionar el tráfico entre la red interna y la externa.
   - Implementa políticas de control de acceso en el servidor proxy.

5. **Detección y Respuesta de Red (NDR):**
   - Despliega y configura herramientas NDR para monitorear el tráfico de red y detectar actividades sospechosas.
   - Configura alertas y registros para eventos de la red.

6. **Pruebas de Seguridad:**
   - Realiza escaneos de red y evaluaciones de vulnerabilidades utilizando herramientas como Nmap para identificar posibles problemas de seguridad.
   - Prueba las reglas del firewall y la segmentación de la red para asegurar que se prevenga el acceso no autorizado.

7. **Documentación e Informes:**
   - Documenta el diseño de la red, las reglas del firewall y las configuraciones de seguridad.
   - Prepara un informe que resuma el proyecto, incluyendo cualquier vulnerabilidad descubierta y los pasos tomados para abordarlas.

Este proyecto brindará a los participantes experiencia práctica en la configuración y seguridad de un entorno de red, aplicando los conceptos de defensa de red, firewalls, DMZ y detección y respuesta de red.

## 🚛 ¿Cómo entregar este proyecto?

Una vez que hayas finalizado los pasos de instrucción de Packet Tracer, por favor guarda tus cambios y adjunta el archivo en la plataforma de 4geeks.com en el proyecto correspondiente.

- Configuración de las redes Interna, Externa y DMZ en el diseño de red propuesto.
- Configuración del firewall y gateway para controlar el tráfico entre los ambientes interno, externo y DMZ.
- Capturas de pantalla de pruebas de acceso y bloqueo de tráfico entre los ambientes especificados.
- Informe detallando las medidas de seguridad aplicadas y recomendaciones de seguridad para el diseño propuesto.

<!-- hide -->
## Colaboradores

Gracias a estas maravillosas personas ([clave de emojis](https://github.com/kentcdodds/all-contributors#emoji-key)):

1. [Vanessa Morocho (vanemorocho)](https://github.com/vanemorocho) contribución: (construir tutorial) ✅, (documentación) 📖
  
2. [Alejandro Sanchez (alesanchezr)](https://github.com/alesanchezr), contribución: (reportes de bugs) 🐛

Este y muchos otros ejercicios son creados por estudiantes como parte del [Bootcamp de Ciberseguridad](https://4geeksacademy.com/us/coding-bootcamps/cybersecurity) de 4Geeks Academy por [Alejandro Sánchez](https://twitter.com/alesanchezr) y muchos otros colaboradores. Descubre más sobre nuestro [Curso de Desarrollador Full Stack](https://4geeksacademy.com/us/coding-bootcamps/part-time-full-stack-developer) y el [Bootcamp de Ciencia de Datos](https://4geeksacademy.com/us/coding-bootcamps/datascience-machine-learning).

<!-- endhide -->
