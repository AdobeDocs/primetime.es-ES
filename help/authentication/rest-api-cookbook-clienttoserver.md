---
title: Guía de la API de REST (de cliente a servidor)
description: Rest API cookbook de cliente a servidor.
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 0%

---

# Guía de la API de REST (de cliente a servidor) {#rest-api-cookbook-client-to-server}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.


## Información general {#overview}

Este documento proporciona instrucciones paso a paso para que el equipo de ingeniería de un programador integre un &quot;dispositivo inteligente&quot; (consola de juegos, aplicación de televisión inteligente, decodificador, etc.) con autenticación de Adobe Primetime mediante servicios de API de REST. Este método de cliente a servidor, que utiliza API de REST en lugar de un SDK de cliente, ofrece una compatibilidad más amplia con diferentes plataformas para las que no sería posible desarrollar un número significativo de SDK únicos. Para obtener una amplia descripción técnica del funcionamiento de la solución sin cliente, consulte la [Información técnica de Clientless](/help/authentication/rest-api-overview.md).


Este método requiere dos componentes (aplicación de streaming y aplicación AuthN) para completar los flujos necesarios: los flujos de inicio, registro, autorización y medios de visualización en la aplicación de streaming, y el flujo de autenticación en la aplicación AuthN.

## Componentes {#components}

En una solución de cliente a servidor en funcionamiento están implicados los siguientes componentes:



| Tipo | Componente | Descripción |
| --- | --- | --- |
| Dispositivo de streaming | Aplicación de streaming | La aplicación de programador que reside en el dispositivo de transmisión del usuario y reproduce vídeo autenticado. |
| | Módulo \[Optional\] AuthN | si el dispositivo de streaming tiene un agente de usuario (es decir, un explorador web), el módulo AuthN es responsable de autenticar al usuario en el MVPD IdP. |
| \[Opcional\] Dispositivo AuthN | Aplicación AuthN | si el dispositivo de streaming no tiene un agente de usuario (es decir, un explorador web), la aplicación AuthN es una aplicación web de programador a la que se accede desde un dispositivo de un usuario independiente mediante un explorador web. |
| Infraestructura de Adobe | Servicio de Adobe Pass | Servicio que se integra con el servicio MVPD IdP y AuthZ y proporciona decisiones de autenticación y autorización. |
| Infraestructura de MVPD | ID de MVPD | Punto final de MVPD que proporciona un servicio de autenticación basado en credenciales para validar la identidad de su usuario. |
| | Servicio AuthZ de MVPD | Punto final de MVPD que proporciona decisiones de autorización basadas en las suscripciones del usuario, los controles parentales, etc. |



Los términos adicionales utilizados en el flujo se definen en la variable [Glosario](/help/authentication/glossary.md).

## Flujos{#flows}

### Registro dinámico de clientes (DCR)

Adobe Pass utiliza DCR para proteger las comunicaciones de cliente entre una aplicación o un servidor de programación y los servicios de Adobe Pass. El flujo DCR es independiente, dependiente y de requisito previo, y se puede encontrar en [Registro dinámico de clientes](/help/authentication/dynamic-client-registration.md)


### Flujos de aplicaciones de streaming (Smart Device)

![](assets/smart-device-app-flow.png)

#### Flujo de inicio

1. La aplicación se inicia y carga su interfaz de usuario inicial.

2. Obtenga o genere un ID de dispositivo.

3. Ejecute una llamada de autenticación de comprobación para ver si el dispositivo ya está autenticado.  Por ejemplo: [`<SP_FQDN>/api/v1/checkauthn [device ID]`](/help/authentication/check-authentication-token.md)

4. Si la variable `checkauthn` La llamada se ha realizado correctamente, continúe con el flujo de autorización a partir del paso 2.  Si se produce un error, inicie el flujo de registro.



#### Flujo de registro

1. Obtenga un código de registro y una URL para que el usuario utilice para acceder a la aplicación de inicio de sesión en la segunda pantalla y preséntele al usuario lo siguiente:

   a. Envíe una solicitud de POST al Servicio de código de registro de Adobe, pasando un ID de dispositivo con hash y una &quot;URL de registro&quot;.  Por ejemplo: [`<REGGIE_FQDN>/reggie/v1/[requestorId]/regcode [device ID]`](/help/authentication/registration-code-request.md)

   b. Presente el código de registro devuelto y la dirección URL al usuario.

   c. Indique al usuario que cambie a un dispositivo compatible con la web, vaya a la URL y, a continuación, introduzca el código de registro.



#### Flujo de autorización

1. El usuario vuelve de la aplicación de la segunda pantalla y pulsa el botón &quot;Continuar&quot; del dispositivo. Alternativamente, puede implementar un mecanismo de sondeo para comprobar el estado de autenticación, pero la autenticación de Adobe Primetime recomienda el método del botón Continuar sobre el sondeo. <!--(For information on employing a "Continue" button versus polling the Adobe Primetime authentication backend server, see the Clientless Technical Overview: Managing 2nd-Screen Workflow Transition.)--> Por ejemplo: [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/authn](/help/authentication/retrieve-authentication-token.md)

2. Envíe una solicitud de GET al servicio de autorización de autenticación de Adobe Primetime para iniciar la autorización. Por ejemplo: `<SP_FQDN>/api/v1/authorize [device ID, Requestor ID, Resource ID]`

<!-- end list -->

* Si la respuesta indica éxito: El usuario tiene un token de AuthN válido Y el usuario está autorizado a ver los medios solicitados (hay un token de AuthZ válido para este usuario).

* Si la respuesta indica un error: Examine la excepción producida para determinar su tipo (AuthN, AuthZ o algo más):

   * Si se ha producido un error de AuthN, vuelva a iniciar el flujo de registro.

   * Si se ha producido un error de AuthZ, el usuario no tiene autorización para ver el contenido solicitado y se le debe mostrar algún tipo de mensaje de error.

   * Si hubo algún otro error (error de conexión, error de red, etc.) a continuación, mostrar un mensaje de error apropiado al usuario.



#### Ver flujo de medios

1. Opciones de medios actuales. El usuario selecciona los medios que desea ver.

2. ¿Están protegidos los medios?

   a. La aplicación comprueba si los medios están protegidos.

   b. Si el medio está protegido, la aplicación inicia el flujo de autorización (AuthZ) anterior.

   c. Si los medios no están protegidos, reproduzca los medios para el usuario.

3. Reproducción de los medios.


### Flujo de aplicación AuthN (2ª pantalla)

![](assets/secnd-screen-authn-flow.png)

1. Obtenga una lista de MVPD para este usuario. Por ejemplo: [`<SP_FQDN>/api/v1/config/[requestorID]`](/help/authentication/provide-mvpd-list.md)

1. Inicie el flujo de autenticación.  Por ejemplo: [`<SP_FQDN>/api/v1/authenticate [requestorID, MVPD ID, Redirect URL, Domain name, Registration Code, "noflash=true"]`](/help/authentication/initiate-authentication.md)

1. Compruebe si la autenticación se realizó correctamente. Por ejemplo:[`<SP_FQDN>/api/v1/checkauthn/[registration code][requestor ID]`](/help/authentication/check-authentication-token.md)

1. Envíe al usuario de nuevo a la aplicación de Smart Device para completar el flujo de autorización.

## Plataforma SSO {#platform-sso}

Algunas plataformas proporcionan compatibilidad dedicada con el inicio de sesión único (SSO). Se pueden encontrar los detalles de implementación para cada plataforma respectiva:

* [APPLE SSO](/help/authentication/apple-sso-cookbook-rest-api.md)
* AMAZON SSO

## TempPass y TempPass promocional para la API de REST {#temppass}

En el caso de las implementaciones de TempPass y Promotional TempPass en las que no se requiere que el usuario introduzca sus credenciales, la autenticación se puede implementar directamente en la aplicación de streaming.

**Para utilizar esta API, la aplicación de streaming debe asegurarse de que el ID del dispositivo sea único, ya que se utiliza para identificar el token, junto con los datos adicionales opcionales.**


![](assets/temp-pass-promo-temppass.png)
