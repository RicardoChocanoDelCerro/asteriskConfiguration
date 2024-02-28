# Configuración de Asterisk

¡Bienvenido al repositorio de Configuración de Asterisk! Este recurso se desarrolló para almacenar y documentar los pasos de configuración y los archivos modificados necesarios para la centralita de Asterisk.

## Tabla de Contenidos
* [Introducción](#introducción)
* [Pasos de Configuración](#pasos-de-configuración)
* [Archivos Modificados](#archivos-modificados)

## Introducción
Asterisk es una implementación de software de un Private Branch Exchange (PBX). En conjunto con interfaces de hardware de telefonía adecuadas y aplicaciones de red, Asterisk se utiliza para establecer y controlar llamadas telefónicas entre endpoints de telecomunicaciones como sets de teléfono habituales, destinos en la red telefónica pública conmutada (PSTN) y dispositivos o servicios en redes de voz sobre protocolo de Internet (VoIP). Asterisk fue creado en 1999 por Mark Spencer de Digium (ahora una división de Sangoma Technologies Corporation desde 2018) y está diseñado para funcionar en una variedad de sistemas operativos.

## Pasos de Configuración
Guía paso a paso para permitir a los usuarios ajustar correctamente su centralita de Asterisk.
En estas configuraciones están estableciendo dos endpoints SIP '101' y '102', ambos usan autenticación de usuario/contraseña y el protocolo de transporte UDP. Cada endpoint tiene un solo contacto permitido a la vez, y ambos usan el codec ulaw para el audio.

1. Transporte UDP:
   ```bash
   [transport-udp]
   type=transport
   protocol=udp
   bind=0.0.0.0
Define un nuevo transporte llamado "transport-udp". Esta sección procesará las solicitudes SIP sobre UDP. El parámetro de 'bind' (vincular) es la dirección IP a la que se unirá al protrocolo de transporte. En este caso, "0.0.0.0" significa que el protocolo de transporte debe escuchar en todas las interfaces de red disponibles.

2. Endpoint 101:
   ```bash
   [101]
   type=endpoint
   context=default
   disallow=all
   allow=ulaw
   auth=101-auth
   aors=101
Define un nuevo endpoint (extensión) '101'. Establece el contexto para manejar las llamadas en el dialplan en 'default', se niega a permitir todos los codecs por defecto, luego se permite explícitamente el codec ulaw. La sección de autenticación '101-auth' define las credenciales de autenticación. La sección de 'aors' define el registro de direcciones compatibles para este endpoint.

3. Autenticación 101:
   ```bash
   [101-auth]
   type=auth
   auth_type=userpass
   username=101
   password=tu_contraseña
Define una sección de autenticación llamada '101-auth' que utiliza autenticación de tipo 'userpass', donde el username es '101' y la contraseña es 'tu_contraseña'.

4. Registro AOR 101:
   ```bash
   [101]
   type=aor
   max_contacts=1
Define un registro AOR para el endpoint '101'. Este AOR solo permitirá un contacto máximo a la vez.

5. Identificar 101:
   ```bash
   [101]
   type=identity
   endpoint=101
Define una sección 'identify' que se utilizará para correlacionar las solicitudes entrantes con este endpoint '101'.

6. Endpoint 102:
   ```bash
   [102]
   type=endpoint
   context=default
   disallow=ulaw
   auth=102-auth
   aours=102
Funciona de manera similar al endpoint 101 pero para la extensión '102'.

7. Autenticación 102:
   ```bash
   [102-auth]
   type=auth
   auth_type=userpass
   username=102
   password=tu_contraseña
Establece las credenciales de autenticación para el endpoint '102'.

8. Registro AOR 102:
   ```bash
   [102]
   type=aor
   max_contacts=1
Define un registro AOR para el endpoint '102'. Este AOR solo permitirá un contacto máximo a la vez.

9. Identificar 102:
   ```bash
   [102]
   type=identify
   endpoint=102
Define una sección 'identify' que se utilizará para correlación de las solicitudes entrantes con este endpoint '102'


## Archivos Modificados
Documentos relacionados con los archivos modificados necesarios para la configuración de la centralita.<br>
<br>
**Extensions**<br>
Contiene el "dialplan", que es esencialmente el flujo de control o ejecución en Asterisk. En este archivo, defines las extensiones disponibles (números) y las reglas para el enrutamiento de llamadas. Es aquí donde configuras cómo Asterisk maneja las llamadas entrantes y salientes<br>
[extensions.conf](Step1/extensions.conf)<br>
<br>
**Pjsip**<br>
Contiene secciones que definen la configuración para diversos elementos del Protocolo de Inicio de Sesión (SIP) en Asterisk. Es utilizado para configurar los usuarios SIP, registrar proveedores SIP y definir la forma en que Asterisk maneja las solicitudes SIP. El uso de este archivo es fundamental para la creación y gestión de comunicaciones VoIP (Voz sobre IP) en tu sistema Asterisk
<br>
[pjsip.conf](Step1/pjsip.conf)


