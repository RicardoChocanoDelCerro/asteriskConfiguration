# Configuración de Asterisk

¡Bienvenido al repositorio de Configuración de Asterisk! Este recurso se desarrolló para almacenar y documentar los pasos de configuración y los archivos modificados necesarios para la centralita de Asterisk.

## Tabla de Contenidos
* [Introducción](#introducción)
* [Pasos de Configuración](#pasos-de-configuración)
* [Archivos Modificados](#archivos-modificados)
* [Guías y Ejemplos](#guías-y-ejemplos)
* [Contribuyendo](#contribuyendo)

## Introducción
Introducción detallada acerca de la centralita de Asterisk y su importancia.

## Pasos de Configuración
Guía paso a paso para permitir a los usuarios ajustar correctamente su centralita de Asterisk.

#Step 1
1. Transporte UDP:
   ```bash
   [transport-udp]
   type=transport
   protocol=udp
   bind=0.0.0.0
Define un nuevo transporte llamado "transport-udp". Esta sección procesará las solicitudes SIP sobre UDP. El parámetro de 'bind' (vincular) es la dirección IP a la que se unirá el transportista. En este caso, "0.0.0.0" significa que el transportista debe escuchar en todas las interfaces de red disponibles.

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


## Archivos Modificados
Documentos relacionados con los archivos modificados necesarios para la configuración de la centralita.

## Guías y Ejemplos
Guías detalladas de configuración y ejemplos para facilitar la aplicación precisa de las configuraciones de Asterisk.

## Contribuyendo
Información sobre cómo se pueden realizar aportaciones y sugerencias a este proyecto.
