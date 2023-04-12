---
title: Guía de la API de REST (servidor a servidor)
description: Rest API cookbook server to server.
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1825'
ht-degree: 0%

---


# Guía de la API de REST (servidor a servidor) {#rest-api-cookbook-server-to-server}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.


## Información general {#overview}

El propósito de este documento de la guía es detallar las prácticas recomendadas para implementar la autenticación de Adobe Primetime mediante las arquitecturas de servidor a servidor.  Proporciona requisitos básicos, implementación de flujo paso a paso y consideraciones generales para entornos y operaciones de producción.

 

## Componentes {#components}

En una solución de servidor a servidor que funciona, se incluyen los siguientes componentes:

 
| Tipo | Componente | Descripción | | — | — | — | | Dispositivo de transmisión | Aplicación de flujo continuo | La aplicación Programador que reside en el dispositivo de transmisión del usuario y reproduce vídeo autenticado. | | | \[Opcional\] Módulo AuthN | Si el dispositivo de transmisión tiene un agente de usuario (es decir, un navegador web), el módulo AuthN es responsable de autenticar al usuario en el IdP de MVPD. | | \[Opcional\] Dispositivo AuthN | Aplicación AuthN | si el dispositivo de transmisión no tiene un agente de usuario (es decir, un navegador web), la aplicación AuthN es una aplicación web del programador a la que se accede desde el dispositivo de un usuario independiente mediante un navegador web. | | Infraestructura de programación | Servicio de programación | Servicio que vincula el dispositivo de transmisión con el servicio de Adobe Pass para obtener decisiones de autenticación y autorización. | | Infraestructura de Adobe | Servicio Adobe Pass | Servicio que se integra con el servicio MVPD IdP y AuthZ y que proporciona decisiones de autenticación y autorización. | | Infraestructura MVPD | IdP de MVPD | Un extremo MVPD que proporciona un servicio de autenticación basado en credenciales para validar la identidad de su usuario. | | | Servicio MVPD AuthZ | Punto final de MVPD que proporciona decisiones de autorización basadas en suscripciones del usuario, controles parentales, etc. |


Los términos adicionales utilizados en el flujo se definen en la variable
[Glosario](/help/authentication/glossary.md).

## Flujos {#flows}

### Registro de cliente dinámico (DCR)


Adobe Pass utiliza DCR para proteger las comunicaciones de los clientes entre una aplicación o servidor de programador y los servicios de Adobe Pass. El flujo de DCR es independiente, dependiente y de requisito previo, y se puede encontrar en [Registro de cliente dinámico](/help/authentication/dynamic-client-registration.md).


### Autenticación (authN)

El flujo de autenticación se utiliza para permitir que un usuario se identifique con su MVPD para determinar si tiene una cuenta válida. 

1. El usuario inicia la aplicación de dispositivo de transmisión e intenta iniciar sesión o ver contenido protegido.
2. La aplicación de dispositivo de transmisión solicita al servicio de programación que determine si el dispositivo ya está autenticado.
3. El servicio de programación registra la aplicación mediante DCR.
4. El servicio de programación comprueba el estado authN del dispositivo de transmisión llamando al servicio de Adobe Pass **checkauthn** API.
5. En el caso de que la variable **checkauthn** devuelve el estado de autenticación del dispositivo de usuario y, a continuación, la aplicación puede continuar con el flujo de autorización.
6. En el caso de que la variable **checkauthn** devuelve el estado de que el dispositivo de usuario NO está autenticado y la aplicación debe esperar a que se inicie sesión una solicitud de usuario.
7. Cuando el usuario solicita iniciar sesión directamente (p. ej., selecciona un botón de inicio de sesión) o indirectamente (p. ej., selecciona contenido protegido cuando no está autenticado), la aplicación de dispositivo de transmisión realiza una solicitud al servicio de programación para iniciar la autenticación del usuario. El servicio de programación solicita y recibe un código de registro único (regcode) llamando al servicio de Adobe Pass **regcode** API.
8. El servicio de programación también recupera la lista de MVPD y atributos actuales llamando al servicio de Adobe Pass **config** API. Nota: también se puede llamar a esta API anteriormente en el flujo y en la caché.
9. El servicio de programación devuelve el regcode a la aplicación de dispositivo de transmisión y la lista de MVPD procesada solicitada en el paso \#7. Nota: El Programador especifica el formato de lista MVPD procesado y puede filtrarse para permitir o bloquear explícitamente MVPD específicos (es decir, listas de permitidos o de bloqueados).
10. Si el es diferente del dispositivo AuthN (es decir, &quot;segunda pantalla&quot;), ya sea por elección o por necesidad (es decir, el dispositivo de transmisión no admite un agente de usuario), el dispositivo de transmisión debe mostrar el código regresivo y un URI para que el usuario acceda a la aplicación AuthN. El usuario escribe el URI en el agente de usuario del dispositivo AuthN para iniciar la aplicación AuthN y, a continuación, escribe el regcode en esa aplicación. Si el dispositivo de transmisión es el mismo que el dispositivo AuthN, el código regresivo se puede pasar mediante programación al módulo AuthN.
11. El módulo AuthN inicia la autenticación de usuarios con el MVPD mostrando un selector de MVPD. Una vez que el usuario selecciona el MVPD, el módulo AuthN llama a **autenticar** con regcode, que redirige el agente de usuario al IdP de MVPD. Cuando el usuario se autentica correctamente con el MVPD, el agente de usuario se redirige a través del servicio de Adobe Pass, donde la autenticación correcta se registra con el regcode y, a continuación, se redirige de nuevo al módulo AuthN.
12. Si el dispositivo de transmisión es diferente del dispositivo AuthN, entonces el dispositivo AuthN debería mostrar un mensaje de autenticación exitoso al usuario y pasos para continuar (p. ej. &quot;Correcto\! Ahora puede volver a su consola de juegos para continuar \[...\]&quot;). Si el dispositivo de transmisión es el mismo que el dispositivo AuthN, el dispositivo de transmisión puede detectar mediante programación la finalización de la autenticación.

 

El diagrama siguiente ilustra el flujo de autenticación:

![](assets/authn-flow.png)

### Autorización (authZ)

El flujo de autorización se utiliza para determinar si un usuario tiene derecho a acceder al contenido solicitado.

1. Cada vez que el usuario intenta ver contenido protegido en la aplicación del dispositivo de transmisión, la aplicación del dispositivo de transmisión llama al servicio de programación para identificar el contenido y solicitar el permiso y la información necesarios para iniciar la emisión.
1. El servicio de programación llama a Adobe Pass **authorization** API que pasa el ID de recurso junto con otros parámetros necesarios. El servicio de Adobe llama al servicio MVPD AuthZ con el ID de recurso y recibe una decisión de autorización que luego se devuelve al servicio de programación. El servicio Adobe Pass almacenará en caché esta decisión de autorización durante un periodo configurable. En subsiguientes **authorization** llamadas del servicio de programación al servicio de Adobe Pass, el valor almacenado en caché se devolverá siempre que sea válido.
1. Si se concede la autorización, el servicio de programación debe llamar a Adobe Pass **/tokens/media** API, que devolverá un token de medios firmado. El servicio de programación debe validar el token de medios mediante la biblioteca de verificador de tokens de medios (JAR). Si es válido, el servicio de programación debe devolver el permiso y las necesidades para iniciar la emisión (por ejemplo, la URL de la emisión) solicitadas en el paso \#1.
1. Si se deniega la autorización, la variable **authorization** devolverá un código de error y una descripción al servicio de programación. El servicio de programación debe devolver el código y la descripción de error (o un mensaje modificado por el programador) a la solicitud en el paso \#1.

El diagrama siguiente ilustra el flujo de autorización:

![](assets/authz-flow.png)

### Cerrar sesión

El flujo de cierre de sesión permite al usuario eliminar la identidad asociada actualmente a la aplicación.

1. Cuando el usuario solicita cerrar la sesión (es decir, eliminar del dispositivo la cuenta MVPD actual asociada con la aplicación), la aplicación de dispositivo de transmisión llama al servicio de programación diciéndole que cierre la sesión del dispositivo.
1. El servicio de programación debe llamar a Adobe Pass **cierre de sesión** API.

El diagrama siguiente ilustra el flujo de cierre de sesión:

![](assets/logout-flow.png)

### \[Opcional\] Preautorización (también conocida como pre-vuelo)

La preautorización se puede utilizar para determinar rápidamente a partir de un conjunto de recursos a los que un usuario puede tener acceso.  El resultado de esta llamada se suele utilizar para personalizar la interfaz de usuario de un usuario individual.

1. Una vez autenticado el usuario, el dispositivo de transmisión puede llamar al servicio de programación para solicitar el contenido al que el usuario está autorizado a transmitir.

1. El servicio de programación debe llamar a Adobe Pass **preautorizar** API con una lista de ID de recursos, que son una cadena simple que generalmente representa un canal al que un usuario puede acceder para la transmisión. *Nota: Actualmente, la variable* ***preautorizar*** *está configurada para limitar la lista a cinco (5) ID de recurso. Cuando se necesitan más de cinco recursos, varios* ***preautorizar*** *se pueden realizar llamadas o la llamada se puede configurar para aceptar más de cinco recursos con un acuerdo de los MVPD. Los implementadores deben tener en cuenta el coste de un* ***preautorizar*** *llamar tanto a los recursos de MVPD como al tiempo de respuesta al Programador y estructurar su uso de la llamada de manera sensata.*

1. La variable **preautorizar** responderá al servicio de programación con un objeto JSON que contenga un valor TRUE o FALSE para cada ID de recurso en la solicitud que indica si el usuario tiene derecho o no al canal asociado. *Nota: Si un MVPD no proporciona una respuesta para un ID de recurso determinado (por ejemplo, debido a errores de red o tiempos de espera), el valor predeterminado será FALSE.*

1. El servicio de programación debe utilizar la variable **preautorizar** llame a response para crear una respuesta personalizada definida por el programador para el dispositivo de transmisión, normalmente para personalizar la presentación para el usuario según sus derechos.

El diagrama siguiente ilustra el flujo de preautorización:

![](assets/preauthz-flow.png)


### Metadatos \[Opcional\]

Los metadatos se pueden utilizar para recuperar información de usuario compartida por el MVPD.
 Algunos ejemplos de esto pueden ser: ID de usuario, código postal, etc.

1. Una vez autenticado el usuario, el servicio de programación puede llamar a Adobe Pass **usermetadata** para solicitar información sobre el usuario autenticado.

1. La respuesta incluirá todos los metadatos disponibles para el usuario dado. Los campos específicos se configuran por separado para cada integración Programador/MVPD.

El diagrama siguiente ilustra el flujo de preautorización:

 

![](assets/user-metadata-api-preauthz.png)

 

## Entornos y requisitos funcionales{#environments}

 

Un programador debe crear al menos dos entornos: uno para producción y uno o más para ensayo.


### Producción

El entorno de producción debe estar altamente disponible y ampliarse adecuadamente para picos grandes o inesperados (p. ej., deportes en directo o noticias de última hora).

 

El servicio Adobe Pass se ejecuta en varios centros de datos geográficamente dispersos en EE. UU.  Para lograr el mejor tiempo de respuesta (es decir, la latencia más baja) del servicio Adobe Pass, el Programador también debería crear una infraestructura de servicios geográficamente dispersa similar. 


El servicio Programador debería limitar la caché DNS a un máximo de 30 segundos en caso de que el Adobe necesite redirigir el tráfico. Esto puede ocurrir si un centro de datos deja de estar disponible.\
 

El programador debe proporcionar la gama IP pública del entorno de producción. Se incluirán en una lista de IP permitidas en la infraestructura de Adobe Pass para el acceso y se gestionarán mediante las políticas de uso de API justas de Adobe.

### Ensayo

El entorno de ensayo puede ser mínimo, pero debe incluir todos los componentes del sistema y la lógica empresarial. Debe funcionar de manera similar a la producción y permitir las versiones de prueba fuera de la producción. Lo ideal es que el entorno de ensayo se pueda conectar a los entornos de prueba de Adobe Pass para que lo utilice el programador y, cuando sea necesario, por Adobe para que podamos ayudarle a realizar pruebas y solucionar problemas.

### Requisitos funcionales

El servicio Programador debe transmitir información precisa de identificación del dispositivo para el dispositivo para el que ejecuta los flujos. Además, el servicio Programador debe pasar la IP del dispositivo para el que está ejecutando los flujos (en un encabezado x-forward-for) junto con el puerto de origen de la conexión (en el campo de información del dispositivo):

    **X-Forwarded-For : \&lt;client _ip=&quot;&quot;>** 
    
    donde \&lt;client _ip=&quot;&quot;> es la dirección IP pública del cliente
    
     
    
    El encabezado debe añadirse en las llamadas **regcode** y **authorization**
    
    Ejemplos :
    
    POST /reggie/v1/{req\_id}/regcode HTTP/1.1
    
    X-Forwarded-For:203.45.101.20
    
     
    
    GET /api/v1/authorized HTTP/1.1
    
    X-Forwarded-For:203.45.101.20

 

El servicio de programación debe enviar los datos y el formato requeridos por MVPD individuales o aplicaciones integradas (p. ej., IP del dispositivo, puerto de origen, información del dispositivo, MRSS, datos opcionales como ECID). <!--Please see the documentation for [Passing Device and Connection Information Cookbook](http://tve.helpdocsonline.com/passing-device-information-cookbook)-->.


El servicio de programación debe respetar los TTL authN y authZ cuando se almacenen en caché las sesiones authN o authZ e invalidan las mismas cuando se notifique.

El programador debe mantener certificados compartidos con Adobe.

<!--
## Related Information {#related}

* [REST API Reference](/help/authentication/rest-api-reference.md)
* [Glossary of Terms](/help/authentication/adobe-pass-glossary.md)
-->