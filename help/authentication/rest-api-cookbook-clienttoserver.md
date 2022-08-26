---
title: Guía de la API de REST (cliente a servidor)
description: Rest API cookbook client to server.
source-git-commit: 4c3a0dd56b4ef99ac8c57cfde61f792088b0ff4d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Guía de la API de REST (cliente a servidor) {#rest-api-cookbook-client-to-server}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.


## Información general {#overview}

Este documento proporciona instrucciones paso a paso para que el equipo de ingeniería de un programador integre un &quot;dispositivo inteligente&quot; (consola de juegos, aplicación de TV inteligente, cuadro superior, etc.) con autenticación de Adobe Primetime mediante los servicios de API de REST. Este enfoque de cliente a servidor, que utiliza API de REST en lugar de un SDK de cliente, permite una compatibilidad más amplia con diferentes plataformas para las que no sería posible desarrollar un número significativo de SDK únicos. Para obtener una descripción general técnica del funcionamiento de la solución sin cliente, consulte la [Información general técnica sin cliente](/help/authentication/rest-api-overview.md).


Este método requiere dos componentes (aplicación de flujo continuo y aplicación AuthN) para completar los flujos necesarios: inicio, registro, autorización y flujos de visualización de medios en la aplicación de flujo continuo y el flujo de autenticación en la aplicación AuthN.

## Componentes {#components}

En una solución de cliente a servidor en funcionamiento, se incluyen los siguientes componentes:

 

| Tipo | Componente | Descripción |
| --- | --- | --- |
| Dispositivo de transmisión | Aplicación de flujo continuo | La aplicación Programador que reside en el dispositivo de transmisión del usuario y reproduce vídeo autenticado. |
|  | \[Opcional\] Módulo AuthN | si el dispositivo de transmisión tiene un agente de usuario (es decir, un explorador web), el módulo AuthN es responsable de autenticar al usuario en el IdP de MVPD. |
| \[Opcional\] Dispositivo AuthN | Aplicación AuthN | si el dispositivo de transmisión no tiene un agente de usuario (es decir, un explorador web), la aplicación AuthN es una aplicación web del programador a la que se accede desde el dispositivo de un usuario independiente mediante un explorador web.  |
| Infraestructura de Adobe | Servicio de Adobe Pass | Servicio que se integra con el IdP de MVPD y el servicio AuthZ y que proporciona decisiones de autenticación y autorización. |
| Infraestructura MVPD | IdP de MVPD | Un extremo MVPD que proporciona un servicio de autenticación basado en credenciales para validar la identidad de su usuario. |
|  | Servicio MVPD AuthZ | Punto final de MVPD que proporciona decisiones de autorización basadas en suscripciones del usuario, controles parentales, etc. |

 

Los términos adicionales utilizados en el flujo se definen en la variable [Glosario](http://tve.helpdocsonline.com/adobe-pass-glossary).

## Flujos{#flows}

### Registro de cliente dinámico (DCR)

Adobe Pass utiliza DCR para proteger las comunicaciones de los clientes entre una aplicación o servidor de programador y los servicios de Adobe Pass. El flujo de DCR es independiente, dependiente y de requisito previo, y se puede encontrar aquí: http://tve.helpdocsonline.com/dynamic-client-registration


### Flujos de aplicaciones de transmisión (dispositivo inteligente)

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/clientless_1st_screen_updated.PNG)

 

#### Flujo de inicio

1. La aplicación se inicia y carga su IU inicial.

2. Obtenga o genere un ID de dispositivo.

3. Ejecute una llamada Check-authentication para ver si el dispositivo ya está autenticado.  Por ejemplo: [`<SP_FQDN>/api/v1/checkauthn [device ID]`](/help/authentication/check-authentication-token.md)

4. Si la variable `checkauthn` La llamada de se realiza correctamente, vaya al flujo de autorización desde el paso 2 en adelante.  Si falla, inicie el flujo de registro.

 

#### Flujo de registro

1. Obtenga un código de registro y una URL que el usuario utilice para acceder a la aplicación de inicio de sesión de la segunda pantalla y preséntela al usuario:

   a. Envíe una solicitud de POST al servicio de código de registro de Adobe, pasando un ID de dispositivo con hash y una &quot;URL de registro&quot;.  Por ejemplo: [`<REGGIE_FQDN>/reggie/v1/[requestorId]/regcode [device ID]`](/help/authentication/registration-code-request.md)

   b. Presente al usuario el código de registro y la URL devueltos.

   c. Indique al usuario que cambie a un dispositivo compatible con web, navegue hasta la URL y, a continuación, introduzca el código de registro.

 

#### Flujo de autorización

1. El usuario vuelve de la aplicación de la segunda pantalla y pulsa el botón &quot;Continuar&quot; del dispositivo. Como alternativa, puede implementar un mecanismo de sondeo para comprobar el estado de autenticación, pero la autenticación de Adobe Primetime recomienda el método del botón Continuar en lugar de la encuesta. <!--(For information on employing a "Continue" button versus polling the Adobe Primetime authentication backend server, see the Clientless Technical Overview: Managing 2nd-Screen Workflow Transition.)--> Por ejemplo: [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/authn](/help/authentication/retrieve-authentication-token.md)

2. Envíe una solicitud de GET al servicio de autorización de autenticación de Adobe Primetime para iniciar la autorización. Por ejemplo: `<SP_FQDN>/api/v1/authorize [device ID, Requestor ID, Resource ID]`

<!-- end list -->

- Si la respuesta indica éxito: El usuario tiene un token AuthN válido Y el usuario está autorizado para ver el contenido multimedia solicitado (hay un token AuthZ válido para este usuario).

- Si la respuesta indica un error: Examine la excepción lanzada para determinar su tipo (AuthN, AuthZ u otro):

   - Si se trataba de un error AuthN, vuelva a iniciar el flujo de registro.

   - Si se trata de un error AuthZ, el usuario no está autorizado a ver el contenido multimedia solicitado y se debe mostrar algún tipo de mensaje de error al usuario.

   - Si hay algún otro error (error de conexión, error de red, etc.) a continuación, muestre un mensaje de error apropiado al usuario.

 

#### Ver flujo de medios

1. Presente las opciones de medios. El usuario selecciona los medios que desea ver.

2. ¿Los medios están protegidos?

   a. La aplicación comprueba si los medios están protegidos.

   b. Si el contenido está protegido, la aplicación inicia el flujo de autorización (AuthZ) anterior.

   c. Si el medio no está protegido, reproduzca el contenido para el usuario.

3. Reproducción del contenido.


### Flujo de aplicación AuthN (segunda pantalla)

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/smart_dev_second_flow.png)

1. Obtenga una lista de MVPD para este usuario. Por ejemplo: [`<SP_FQDN>/api/v1/config/[requestorID]`](/help/authentication/provide-mvpd-list.md)

1. Inicie el flujo de autenticación.  Por ejemplo: [`<SP_FQDN>/api/v1/authenticate [requestorID, MVPD ID, Redirect URL, Domain name, Registration Code, "noflash=true"]`](/help/authentication/initiate-authentication.md)

1. Compruebe si la autenticación se ha realizado correctamente.  Por ejemplo: [`<SP_FQDN>/api/v1/checkauthn/[registration code][requestor ID]`](/help/authentication/check-authentication-token.md)

1. Vuelva a enviar al usuario a la aplicación de dispositivos inteligentes para completar el flujo de autorización.

 

## SSO de plataforma {#platform-sso}

Algunas plataformas proporcionan compatibilidad dedicada para el inicio de sesión único (SSO). Se pueden encontrar detalles de implementación para cada plataforma respectiva:

- [Apple SSO](http://tve.helpdocsonline.com/rest-api-apple-sso)
- Amazon SSO

## TempPass y TempPass promocional para la API de REST {#temppass}

Para implementaciones TempPass y Promotional TempPass en las que el usuario no está obligado a introducir credenciales, la autenticación se puede implementar directamente en la aplicación de flujo continuo. 

**Para utilizar esta API, la aplicación de flujo continuo debe asegurarse de la exclusividad del ID del dispositivo que se utiliza para identificar el token, junto con los datos adicionales opcionales.**


![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/Free%20preview%20option.png?dc=201612071020-0)

### Información relacionada {#related}

- [Referencia de API de REST](/help/authentication/rest-api-reference.md)
