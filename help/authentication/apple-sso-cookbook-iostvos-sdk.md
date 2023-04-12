---
title: Guía de Apple SSO (SDK de iOS/tvOS)
description: Guía de Apple SSO (SDK de iOS/tvOS)
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1867'
ht-degree: 0%

---



# Guía de Apple SSO (SDK de iOS/tvOS) {#apple-sso-cookbook-iostvos-sdk}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Introducción {#Introduction}

El SDK de Adobe Primetime Authentication AccessEnabler para iOS/tvOS puede admitir la autenticación de plataforma Single Sign-On (SSO) para usuarios finales de aplicaciones cliente que se ejecuten en iOS, iPadOS o tvOS a través de lo que llamamos flujo de trabajo de Apple SSO.

Tenga en cuenta que este documento actúa como extensión de la documentación existente del SDK de AccessEnabler iOS/tvOS, que se puede encontrar [here](/help/authentication/iostvos-sdk-api-reference.md).

</br>

## Guía paso a paso {#Cookbook}

Para beneficiarse de la experiencia de usuario de SSO de Apple, una aplicación tendría que integrar el SDK de iOS/tvOS de AccessEnabler y seguir la secuencia de sugerencias que se presentan a continuación.

</br>

### Requisitos previos {#Prerequisites}

</br>

#### Permiso

>[!TIP]
>
> **<u>Consejo de Pro:</u>** Para tener acceso a la información de suscripción del usuario, el usuario debe dar permiso a la aplicación para continuar, de forma similar a proporcionar acceso a la cámara o el micrófono del dispositivo. Este permiso debe solicitarse por aplicación y el dispositivo guardará la selección del usuario. Tenga en cuenta que el usuario puede cambiar su decisión accediendo a la configuración de la aplicación (acceso de permiso del proveedor de TV) o a la sección desde *`Settings -> TV Provider`* en iOS/iPadOS o *`Settings -> Accounts -> TV Provider`* en tvOS.

>[!TIP]
>
> **<u>Consejo de Pro:</u>** Se recomienda solicitar el permiso del usuario cuando la aplicación entre en estado de primer plano, pero es solo una sugerencia, ya que la aplicación puede comprobar [permiso de acceso](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) la información de suscripción del usuario en cualquier momento antes de requerir la autenticación del usuario. Además, las API del SDK de iOS/tvOS de AccessEnabler solicitarán automáticamente el permiso del usuario cuando lo necesite.

>[!TIP]
>
> **<u>Consejo de Pro:</u>** En caso de que el usuario no conceda acceso a su información de suscripción o en caso de que falle la comunicación con la infraestructura de la cuenta del suscriptor de vídeo, el SDK de AccessEnabler iOS/tvOS volverá al flujo de autenticación normal.

>[!TIP]
>
> **<u>Consejo de Pro:</u>** Recomendamos incentivar a los usuarios que se nieguen a dar permiso para acceder a la información de suscripción explicando las ventajas de la experiencia de usuario del inicio de sesión único (SSO). Tenga en cuenta que el usuario puede cambiar su decisión accediendo a la configuración de la aplicación (acceso de permiso del proveedor de TV) o a la sección desde *`Settings -> TV Provider`* en iOS/iPadOS o *`Settings -> Accounts -> TV Provider`* en tvOS.


```swift
    ...
    let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();
    
    videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
                switch (accessStatus) {
                // The user allows the application to access subscription information.
                case VSAccountAccessStatus.granted:
                   // Do nothing.
                
                // The user has not yet made a choice or does not allow the application to access subscription information.
                default:
                   // Incentivize users who refuse to give permission to access subscription information by explaining the benefits of the Single Sign-On (SSO) user experience. Please bear in mind that the user can change its decision by going to the application settings (TV Provider permission access) or to the section from Settings -> TV Provider on iOS/iPadOS or Settings -> Accounts -> TV Provider on tvOS.
                   ...
                }
    }
    ... 
```

</br>

#### Llamadas

>[!TIP]
>
> **<u>Consejo de Pro:</u>** Implemente la siguiente lista de [callbacks](/help/authentication/iostvos-sdk-api-reference.md) que son específicos del flujo de trabajo de Apple SSO.

- [*currentTVProviderDialog*](/help/authentication/iostvos-sdk-api-reference.md#presenttvproviderdialog-presenttvdialog) - Llamada de retorno activada cuando se va a abrir el selector de MVPD de Apple.
- [*dismissTVProviderDialog*](/help/authentication/iostvos-sdk-api-reference.md#dismisstvproviderdialog-dismisstvdialog) - Llamada de retorno activada cuando el selector de MVPD de Apple va a cerrarse.

</br>

#### Informes de errores

>[!TIP]
>
> **<u>Consejo de Pro:</u>** Implemente la siguiente lista de [códigos de error avanzados](/help/authentication/error-reporting.md) que son específicos del flujo de trabajo de Apple SSO.

- ***N003*** - El usuario seleccionó la opción &quot;Otro proveedor de TV&quot; del selector MVPD de Apple.
- ***N004*** - El usuario seleccionó un proveedor de TV del selector de MVPD de Apple, que el solicitante actual no admite (integración o inicio de sesión único desactivado).
- ***N005*** - El usuario decidió cancelar el selector MVPD normal o el selector MVPD de Apple.
- ***VSA403*** - Se deniega el permiso del proveedor de TV del usuario para la aplicación.
- ***VSA404*** - El permiso del proveedor de TV del usuario es indeterminado para la aplicación.
- ***VSA503*** - Error en la solicitud de metadatos de la cuenta del suscriptor de vídeo, se proporciona más contexto en la *message* campo .
- ***AAPL/APPL_ERROR*** - Error en la solicitud de metadatos de la cuenta del suscriptor de vídeo, se proporciona más contexto en la *detalles* campo . 

</br>

### Autenticación {#Authentication}

>[!TIP]
>
> **<u>Sugerencia:</u>** Siga los pasos que se indican a continuación para las implementaciones de iOS/iPadOS/tvOS.

1. La solicitud tendría que [initialize](/help/authentication/iostvos-sdk-api-reference.md#initsoftwarestatement-initwithsoftwarestatement) el SDK de AccessEnabler iOS/tvOS.
1. La solicitud tendría que [establecer el identificador del solicitante actual](/help/authentication/iostvos-sdk-api-reference.md#setrequestorrequestorid-setrequestorrequestoridserviceproviders-setreqv3).

   **Importante:** Este segundo paso podría déclencheur un [código de error avanzado](/help/authentication/error-reporting.md) que es específico del flujo de trabajo de SSO de Apple, en caso de que **uno de los siguientes es true**:

   - ***VSA403*** - Se deniega el permiso del proveedor de TV del usuario para la aplicación.
   - ***VSA404*** - El permiso del proveedor de TV del usuario es indeterminado para la aplicación.
   - ***APPL*** : La comunicación entre el SDK de iOS/tvOS de AccessEnabler y el marco de cuentas de suscriptor de vídeo ha encontrado un error.

   Este segundo paso intentaría intercambiar silenciosamente el perfil SSO de Apple por un token de autenticación de Adobe, en caso de que **todos los anteriores son falsos** y **todos los siguientes son verdaderos**:

   - El permiso del proveedor de TV del usuario se concede para la aplicación.
   - El usuario ha iniciado sesión en su cuenta de proveedor de TV a nivel del sistema del dispositivo.
   - El SDK de AccessEnabler iOS/tvOS recibió el identificador de proveedor de TV del usuario del marco de cuentas de suscriptor de vídeo.
   - La integración del proveedor de TV del usuario con la aplicación se habilita mediante el panel de control de Televisión de Adobe Primetime.
   - El inicio de sesión único del proveedor de TV del usuario con la aplicación está habilitado a través del panel de control de Televisión de Adobe Primetime.
   - El proveedor de TV del usuario no se degrada a través del panel de control de Televisión de Adobe Primetime.
   - El SDK de AccessEnabler iOS/tvOS recibió la respuesta SAML del proveedor de TV del usuario desde el marco de cuentas del suscriptor de vídeo.

   **<u>Consejo de Pro:</u>** Este segundo paso no déclencheur ninguna otra devolución de llamada, aparte de la [setRequestorComplete](/help/authentication/iostvos-sdk-api-reference.md#setrequestorcomplete-setreqcomplete) llamada de retorno, ya que la autenticación no se inició explícitamente en la aplicación.

1. La solicitud tendría que [comprobar el estado de autenticación](/help/authentication/iostvos-sdk-api-reference.md#checkauthentication-checkauthn).

   **Importante:** Este tercer paso podría déclencheur un [código de error avanzado](/help/authentication/error-reporting.md) que es específico del flujo de trabajo de SSO de Apple, en caso de que **uno de los siguientes es true**:

   - ***VSA403** - El usuario ha iniciado sesión en su cuenta de proveedor de TV a nivel del sistema del dispositivo, pero se deniega el permiso de proveedor de TV del usuario para la aplicación.
   - ***VSA404** - El usuario ha iniciado sesión en su cuenta de proveedor de TV a nivel del sistema del dispositivo, pero el permiso de proveedor de TV del usuario no está determinado para la aplicación.
   - ***APPL\_ERROR** : El usuario ha iniciado sesión en su cuenta de proveedor de TV a nivel de sistema de dispositivo, pero la comunicación entre el SDK de iOS/tvOS de AccessEnabler y el marco de cuentas de suscriptor de vídeo ha encontrado un error.

   **Importante:** Este tercer paso déclencheur el [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) callback con *status* igual a 0, en caso de que **uno de los siguientes es true**:

   - El usuario no ha iniciado sesión en su cuenta de proveedor de TV a nivel del sistema del dispositivo o a través del flujo de autenticación regular.
   - El usuario ha iniciado sesión en su cuenta de proveedor de TV a nivel del sistema del dispositivo o a través del flujo de autenticación regular, pero el TTL del token de autenticación del proveedor de TV del usuario ha pasado.
   - El usuario ha iniciado sesión en su cuenta de proveedor de TV a nivel del sistema del dispositivo o a través del flujo de autenticación regular, pero la integración del proveedor de TV del usuario con la aplicación está deshabilitada a través del panel de control de Adobe Primetime TVE.
   - El usuario ha iniciado sesión en su cuenta de proveedor de TV a nivel de sistema de dispositivo, pero el inicio de sesión único del proveedor de TV del usuario con la aplicación está desactivado a través del panel de control de Adobe Primetime TVE.
   - El usuario ha iniciado sesión en su cuenta de proveedor de TV a nivel del sistema del dispositivo, pero se deniega el permiso de proveedor de TV del usuario para la aplicación.
   - El usuario ha iniciado sesión en su cuenta de proveedor de TV a nivel del sistema del dispositivo, pero el permiso de proveedor de TV del usuario no está determinado para la aplicación.
   - El usuario ha iniciado sesión en su cuenta de proveedor de TV a nivel del sistema del dispositivo, pero la comunicación entre el SDK de iOS/tvOS de AccessEnabler y el marco de cuentas del suscriptor de vídeo ha encontrado un error.

   **Importante:** Este tercer paso déclencheur el [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) callback con *status* igual a 1, en caso de que **todos los anteriores son falsos.**


1. La solicitud tendría que [inicializar la autenticación](/help/authentication/iostvos-sdk-api-reference.md#getauthentication-getauthenticationwithdata-getauthn) en caso de que la comprobación de estado de autenticación anterior activara la variable [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) callback con *status* igual a 0.

   **<u>Consejo de Pro:</u>** Implemente una de las siguientes API de SDK de AccessEnabler iOS/tvOS [getAuthentication](/help/authentication/iostvos-sdk-api-reference.md#getAuthN) o [getAuthentication:filter](/help/authentication/iostvos-sdk-api-reference.md#getAuthN_filter).

   **Importante:** Este cuarto paso podría déclencheur un [código de error avanzado](/help/authentication/error-reporting.md) que es específico del flujo de trabajo de SSO de Apple, en caso de que **uno de los siguientes es true**:

   - ***VSA403*** - Se deniega el permiso del proveedor de TV del usuario para la aplicación.
   - ***VSA404*** - El permiso del proveedor de TV del usuario es indeterminado para la aplicación.
   - ***VSA503*** : La comunicación entre el SDK de iOS/tvOS de AccessEnabler y el marco de cuentas de suscriptor de vídeo ha encontrado un error.
   - ***N003*** - El usuario seleccionó la opción &quot;Otro proveedor de TV&quot; del selector MVPD de Apple.
   - ***N004*** - El usuario seleccionó un proveedor de TV del selector de MVPD de Apple, que el solicitante actual no admite (integración o inicio de sesión único desactivado).
   - ***N005*** - El usuario decidió cancelar el selector MVPD normal o el selector MVPD de Apple.

   **Importante:** Este cuarto paso se volverá a utilizar para el flujo de autenticación regular, activando el [displayProviderDialog](/help/authentication/iostvos-sdk-api-reference.md#dispProvDialog) callback y **one** de lo anterior [códigos de error avanzados](/help/authentication/error-reporting.md), en caso de **uno de los anteriores es verdadero**. 

   **Importante:** Este cuarto paso se volverá a utilizar para el flujo de autenticación regular, activando el [navegarToUrl](/help/authentication/iostvos-sdk-api-reference.md#nav2url) o [navegarToUrl:useSVC](/help/authentication/iostvos-sdk-api-reference.md#nav2urlSVC) callback y **ninguno** de lo anterior [códigos de error avanzados](/help/authentication/error-reporting.md), en caso de que el usuario seleccione un proveedor de TV, que no admita Apple SSO, pero esté presente en el selector de MVPD de Apple.

   **<u>Consejo de Pro:</u>** El SDK de AccessEnabler iOS/tvOS llama silenciosamente a la función [setSelectedPrrovder](/help/authentication/iostvos-sdk-api-reference.md#setSelProv) , en caso de que el usuario seleccione un proveedor de TV, que no admita Apple SSO, pero esté presente en el selector de MVPD de Apple.

   **Importante:** Este cuarto paso intentaría intercambiar silenciosamente el perfil SSO de Apple por un token de autenticación de Adobe, en caso de que **todos los anteriores son falsos** y **todos los siguientes son verdaderos**:

   - El permiso del proveedor de TV del usuario se concede para la aplicación.
   - El usuario ha iniciado sesión o actualmente inicia sesión en su cuenta de proveedor de TV a nivel del sistema del dispositivo.
   - El SDK de AccessEnabler iOS/tvOS recibió el identificador de proveedor de TV del usuario del marco de cuentas de suscriptor de vídeo.
   - La integración del proveedor de TV del usuario con la aplicación se habilita mediante el panel de control de Televisión de Adobe Primetime.
   - El inicio de sesión único del proveedor de TV del usuario con la aplicación está habilitado a través del panel de control de Televisión de Adobe Primetime.
   - El proveedor de TV del usuario no se degrada a través del panel de control de Televisión de Adobe Primetime.
   - El SDK de AccessEnabler iOS/tvOS recibió la respuesta SAML del proveedor de TV del usuario desde el marco de cuentas del suscriptor de vídeo.


 

>**<u>Consejo de Pro:</u>** Este cuarto paso déclencheur el [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setAuthNStatus) llamada de retorno, independientemente de *status* , ya que la autenticación la inició explícitamente la aplicación.


</br>

### Metadatos {#Metadata}

La aplicación tiene la opción de determinar si la autenticación se ha producido como resultado de un inicio de sesión a través del SSO de la plataforma o no, utilizando el *tokenSource&quot;* [metadatos de usuario](/help/authentication/iostvos-sdk-api-reference.md#getMeta) API del SDK de AccessEnabler iOS/tvOS.

```swift
    ...
    accessEnabler.getMetadata([METADATA_OPCODE_KEY:Int(METADATA_USER_META), METADATA_USER_META_KEY: "tokenSource"])
    ...
```

</br>

### Cerrar sesión {#Logout}

La variable [Cuenta de suscriptor de vídeo](https://developer.apple.com/documentation/videosubscriberaccount) framework no proporciona una API para cerrar la sesión mediante programación de las personas que han iniciado sesión en su cuenta de proveedor de TV a nivel de sistema de dispositivos. Por lo tanto, para que el cierre de sesión surta efecto, el usuario final tendría que cerrar sesión explícitamente desde *`Settings -> TV Provider`* en iOS/iPadOS o *`Settings -> Accounts -> TV Provider`* en tvOS. La otra opción que tendría el usuario es retirar el permiso para acceder a la información de suscripción del usuario de la sección de configuración específica de la aplicación (acceso de permiso del proveedor de TV).

>[!TIP]
>
> **<u>Sugerencia:</u>** Implemente esto a través del SDK para iOS/tvOS de AccessEnabler [cierre de sesión](/help/authentication/iostvos-sdk-api-reference.md#logout) API.


>[!TIP]
>
> **<u>Consejo de Pro:</u>** Siga los pasos a continuación para las implementaciones de tvOS.

- La solicitud tendría que [iniciar el cierre de sesión](/help/authentication/iostvos-sdk-api-reference.md#logout) del SDK de AccessEnabler iOS/tvOS. Esto no facilitaría la limpieza de la sesión en el lado MVPD.
- La aplicación tendría que indicar/pedir al usuario que cierre la sesión explícitamente *`Settings -> Accounts -> TV Provider`* solo en el caso de tvOS [*VSA203* se activa el código de estado](/help/authentication/error-reporting.md).

>[!TIP]
>
> **<u>Consejo de Pro:</u>** Siga los pasos que se indican a continuación para las implementaciones de iOS/iPadOS.

- La solicitud tendría que [iniciar el cierre de sesión](/help/authentication/iostvos-sdk-api-reference.md#logout) del SDK de AccessEnabler iOS/tvOS. Esto facilitaría la limpieza de la sesión en el lado MVPD.
- La aplicación tendría que indicar/pedir al usuario que cierre la sesión explícitamente *`Settings -> TV Provider`* en iOS/iPadOS solo en caso de [*VSA203* se activa el código de estado](/help/authentication/error-reporting.md).


<!--
## Resources {#Resources}

- [Apple SSO Overview](/help/authentication/apple-sso-overview.md)
- [AccessEnabler iOS/tvOS SDK Overview](/help/authentication/iostvos-sdk-overview.md)
- [AccessEnabler iOS/tvOS SDK Cookbook](/help/authentication/iostvos-sdk-cookbook.md)
- [AccessEnabler iOS/tvOS SDK API Reference](/help/authentication/iostvos-sdk-api-reference.md)
- [Error Reporting](/help/authentication/error-reporting.md)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->
