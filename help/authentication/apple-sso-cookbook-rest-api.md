---
title: Guía de Apple SSO (API de REST)
description: Guía de Apple SSO (API de REST)
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 0%

---


# Guía de Apple SSO (API de REST) {#apple-sso-cookbook-rest-api}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Introducción {#Introduction}

La API de REST de autenticación de Adobe Primetime es compatible con la autenticación de inicio de sesión único (SSO) de plataforma para usuarios finales de aplicaciones cliente que se ejecutan en iOS, iPadOS o tvOS a través de lo que llamamos flujo de trabajo de SSO de Apple.

Tenga en cuenta que este documento actúa como una extensión de la documentación de API de REST existente, que se puede encontrar [here](/help/authentication/rest-api-reference.md).

</br>

## Cookbooks {#Cookbooks}

Para beneficiarse de la experiencia de usuario de Apple SSO, una aplicación tendría que integrar la variable [Cuenta de suscriptor de vídeo](https://developer.apple.com/documentation/videosubscriberaccount) desarrollada por Apple, aunque con respecto a la comunicación de la API de REST de autenticación de Adobe Primetime, tendría que seguir la secuencia de sugerencias que se presentan a continuación.

</br>

### Autenticación {#Authentication}

- [¿Hay un token de autenticación de Adobe válido?](#Is_there_a_valid_Adobe_authentication_token)
- [¿El usuario ha iniciado sesión mediante Platform SSO?](#Is_the_user_logged_in_via_Platform_SSO)
- [Buscar configuración de Adobe](#Fetch_Adobe_configuration)
- [Iniciar el flujo de trabajo SSO de Platform con la configuración de Adobe](#Initiate_Platform_SSO_workflow_with_Adobe_config)
- [¿El inicio de sesión del usuario se ha realizado correctamente?](#Is_user_login_successful)
- [Obtener una solicitud de perfil de Adobe para el MVPD seleccionado](#Obtain_a_profile_request_from_Adobe_for_the_selected_MVPD)
- [Reenviar la solicitud de Adobe a Platform SSO para obtener el perfil](#Forward_the_Adobe_request_to_Platform_SSO_to_obtain_the_profile)
- [Intercambiar el perfil SSO de Platform por un token de autenticación de Adobe](#Exchange_the_Platform_SSO_profile_for_an_Adobe_authentication_token)
- [¿El token de Adobe se genera correctamente?](#Is_Adobe_token_generated_successfully)
- [Iniciar el flujo de trabajo de autenticación de la segunda pantalla](#Initiate_second_screen_authentication_workflow)
- [Proceder con flujos de autorización](#Proceed_with_authorization_flows)

 

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/qu/platform-sso.jpeg)

</br>

#### Paso: &quot;¿Hay un token de autenticación de Adobe válido?&quot; {#Is_there_a_valid_Adobe_authentication_token}

>[!TIP]
>
> **<u>Sugerencia:</u>** Implemente esto a través del [Autenticación de Adobe Primetime](/help/authentication/check-authentication-token.md) servicio.

</br>

#### Paso: &quot;¿El usuario ha iniciado sesión mediante Platform SSO?&quot; {#Is_the_user_logged_in_via_Platform_SSO}

>[!TIP]
>
> **<u>Sugerencia:</u>** Implemente esto a través del [Cuenta de suscriptor de vídeo](https://developer.apple.com/documentation/videosubscriberaccount) marco.

- La solicitud tendría que comprobar [permiso de acceso](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) la información de suscripción del usuario y continúe solo si el usuario la ha permitido.
- La solicitud tendría que presentar un [solicitud](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) para obtener información de la cuenta del suscriptor.
- La aplicación tendría que esperar y procesar el [metadata](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) información.

 

>[!TIP]
>
> **<u>Consejo de Pro:</u>** Siga el fragmento de código y preste especial atención a los comentarios.

```swift
...
let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();

videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
            switch (accessStatus) {
            // The user allows the application to access subscription information.
            case VSAccountAccessStatus.granted:
                    // Construct the request for subscriber account information.
                    let vsaMetadataRequest: VSAccountMetadataRequest = VSAccountMetadataRequest();

                    // This is actually the SAML Issuer not the channel ID.
                    vsaMetadataRequest.channelIdentifier = "https://saml.sp.auth.adobe.com";
    
                    // This is the subscription account information needed at this step.
                    vsaMetadataRequest.includeAccountProviderIdentifier = true;
                    
                    // This is the subscription account information needed at this step.
                    vsaMetadataRequest.includeAuthenticationExpirationDate = true;
                    
                    // This is going to make the Video Subscriber Account framework to refrain from prompting the user with the providers picker at this step. 
                    vsaMetadataRequest.isInterruptionAllowed = false;
                    
                    // Submit the request for subscriber account information - accountProviderIdentifier.
                    videoSubscriberAccountManager.enqueue(vsaMetadataRequest) { vsaMetadata, vsaError in        
                        if (vsaMetadata != nil && vsaMetadata!.accountProviderIdentifier != nil) {
                            // The vsaMetadata!.authenticationExpirationDate will contain the expiration date for current authentication session.
                            // The vsaMetadata!.authenticationExpirationDate should be compared against current date.
                            ...
                            // The vsaMetadata!.accountProviderIdentifier will contain the provider identifier as it is known for the platform configuration.
                            // The vsaMetadata!.accountProviderIdentifier represents the platformMappingId in terms of Adobe Primetime Authentication configuration.
                            ...
                            // The application must determine the MVPD id property value based on the platformMappingId property value obtained above.
                            // The application must use the MVPD id further in its communication with Adobe Primetime Authentication services.
                            ...
                            // Continue with the "Obtain a profile request from Adobe for the selected MVPD" step.
                            ...
                            // Continue with the "Forward the Adobe request to Platform SSO to obtain the profile" step.
                            ...
                        } else {
                            // The user is not authenticated at platform level, continue with the "Fetch Adobe configuration" step.
                            ...
                        }
                    }
        
            // The user has not yet made a choice or does not allow the application to access subscription information.
            default:
                // Fallback to regular authentication workflow.
                ...
            }
}
...  
```

</br>

#### Paso: &quot;Buscar configuración de Adobe&quot; {#Fetch_Adobe_configuration}

>[!TIP]
>
> **<u>Sugerencia:</u>** Implemente esto a través del [Autenticación de Adobe Primetime](/help/authentication/provide-mvpd-list.md) servicio.


>[!TIP]
>
> **<u>Consejo de Pro:</u>** Tenga en cuenta las propiedades de MVPD: *`enablePlatformServices`*, *`boardingStatus`*, *`displayInPlatformPicker`*, *`platformMappingId`*, *`requiredMetadataFields`* y preste especial atención a los comentarios presentados en fragmentos de código de otros pasos.

</br>

#### Paso &quot;Iniciar el flujo de trabajo SSO de Platform con configuración de Adobe&quot; {#Initiate_Platform_SSO_workflow_with_Adobe_config}

>[!TIP]
>
> **<u>Sugerencia:</u>** Implemente esto a través del [Cuenta de suscriptor de vídeo](https://developer.apple.com/documentation/videosubscriberaccount) marco.

- La solicitud tendría que comprobar [permiso de acceso](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) la información de suscripción del usuario y continúe solo si el usuario la ha permitido.
- La solicitud tendría que proporcionar un [delegate](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanagerdelegate) para VSAccountManager.
- La solicitud tendría que presentar un [solicitud](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) para obtener información de la cuenta del suscriptor.
- La aplicación tendría que esperar y procesar el [metadata](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) información.

 

>[!TIP]
>
> **<u>Consejo de Pro:</u>** Siga el fragmento de código y preste especial atención a los comentarios.


```swift
    ...
    let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();
    
    // This must be a class implementing the VSAccountManagerDelegate protocol.
    let videoSubscriberAccountManagerDelegate: VideoSubscriberAccountManagerDelegate = VideoSubscriberAccountManagerDelegate();
    
    videoSubscriberAccountManager.delegate = videoSubscriberAccountManagerDelegate;
    
    videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
                switch (accessStatus) {
                // The user allows the application to access subscription information.
                case VSAccountAccessStatus.granted:
                        // Construct the request for subscriber account information.
                        let vsaMetadataRequest: VSAccountMetadataRequest = VSAccountMetadataRequest();
    
                        // This is actually the SAML Issuer not the channel ID.
                        vsaMetadataRequest.channelIdentifier = "https://saml.sp.auth.adobe.com";
        
                        // This is the subscription account information needed at this step.
                        vsaMetadataRequest.includeAccountProviderIdentifier = true;
                        
                        // This is the subscription account information needed at this step.
                        vsaMetadataRequest.includeAuthenticationExpirationDate = true;
                        
                        // This is going to make the Video Subscriber Account framework to prompt the user with the providers picker at this step. 
                        vsaMetadataRequest.isInterruptionAllowed = true;
                        
                        // This can be computed from the [Adobe Primetime Authentication](/help/authentication/provide-mvpd-list.md) service response in order to filter the TV providers from the Apple picker.
                        vsaMetadataRequest.supportedAccountProviderIdentifiers = supportedAccountProviderIdentifiers;
    
                        // This can be computed from the [Adobe Primetime Authentication](/help/authentication/provide-mvpd-list.md) service response in order to sort the TV providers from the Apple picker.
                        if #available(iOS 11.0, tvOS 11, *) {
                            vsaMetadataRequest.featuredAccountProviderIdentifiers = featuredAccountProviderIdentifiers;
                        }
                        
                        // Submit the request for subscriber account information - accountProviderIdentifier.
                        videoSubscriberAccountManager.enqueue(vsaMetadataRequest) { vsaMetadata, vsaError in                        
                            // This represents the checks for the "Is user login successful?" step.
                            if (vsaMetadata != nil && vsaMetadata!.accountProviderIdentifier != nil) {
                                // The vsaMetadata!.authenticationExpirationDate will contain the expiration date for current authentication session.
                                // The vsaMetadata!.authenticationExpirationDate should be compared against current date.
                                ...
                                // The vsaMetadata!.accountProviderIdentifier will contain the provider identifier as it is known for the platform configuration.
                                // The vsaMetadata!.accountProviderIdentifier represents the platformMappingId in terms of Adobe Primetime Authentication configuration.
                                ...
                                // The application must determine the MVPD id property value based on the platformMappingId property value obtained above.
                                // The application must use the MVPD id further in its communication with Adobe Primetime Authentication services.
                                ...
                                // Continue with the "Obtain a profile request from Adobe for the selected MVPD" step.
                                ...
                                // Continue with the "Forward the Adobe request to Platform SSO to obtain the profile" step.
                                ...
                            } else {
                                // The user is not authenticated at platform level.
                                if (vsaError != nil) {
                                    // The application can check to see if the user selected a provider which is present in Apple picker, but the provider is not onboarded in platform SSO.
                                    if let error: NSError = (vsaError! as NSError), error.code == 1, let appleMsoId = error.userInfo["VSErrorInfoKeyUnsupportedProviderIdentifier"] as! String? {
                                        var mvpd: Mvpd? = nil;
    
                                        // The requestor.mvpds must be computed during the "Fetch Adobe configuration" step. 
                                        for provider in requestor.mvpds {
                                            if provider.platformMappingId == appleMsoId {
                                                mvpd = provider;
                                                break;
                                            }
                                        }
                                        
                                        if mvpd != nil {
                                            // Continue with the "Initiate second screen authentcation workflow" step, but you can skip prompting the user with your MVPD picker and use the mvpd selection, therefore creating a better UX.
                                            ...
                                        } else {
                                            // Continue with the "Initiate second screen authentcation workflow" step.
                                            ...
                                        }
                                    } else {
                                        // Continue with the "Initiate second screen authentcation workflow" step.
                                        ...
                                    }
                                } else {
                                    // Continue with the "Initiate second screen authentcation workflow" step.
                                    ...
                                }
                            }
                        }
            
                // The user has not yet made a choice or does not allow the application to access subscription information.
                default:
                    // Fallback to regular authentication workflow.
                    ...
                }
    }
    ...
```

</br>

#### Paso: &quot;¿El inicio de sesión del usuario es correcto?&quot; {#Is_user_login_successful}

>[!TIP]
>
> **<u>Consejo de Pro:</u>** Tenga en cuenta el fragmento de código de la variable [&quot;Iniciar el flujo de trabajo SSO de Platform con la configuración de Adobe&quot;](#Initiate_Platform_SSO_workflow_with_Adobe_config) paso a paso. El inicio de sesión del usuario se realiza correctamente en caso de que el *`vsaMetadata!.accountProviderIdentifier`* contiene un valor válido y la fecha actual no ha pasado la variable *`vsaMetadata!.authenticationExpirationDate`* valor.

</br>

#### Paso &quot;Obtener una solicitud de perfil de Adobe para el MVPD seleccionado&quot; {#Obtain_a_profile_request_from_Adobe_for_the_selected_MVPD}

>[!TIP]
>
> **<u>Sugerencia:</u>** Implemente esto mediante la autenticación de Adobe Primetime [Solicitud de perfil](/help/authentication/retrieve-profilerequest.md) servicio.

>[!TIP]
>
> **<u>Consejo de Pro:</u>** Tenga en cuenta que el identificador de proveedor obtenido del marco de cuentas de suscriptor de vídeo representa la variable *`platformMappingId`* en términos de la configuración de autenticación de Adobe Primetime. Por lo tanto, la aplicación debe determinar el valor de la propiedad id de MVPD, utilizando la variable *`platformMappingId`* a través del medio de autenticación de Adobe Primetime [Proporcionar lista MVPD](/help/authentication/provide-mvpd-list.md) servicio.

</br>

#### Paso: &quot;Reenviar la solicitud de Adobe a Platform SSO para obtener el perfil&quot; {#Forward_the_Adobe_request_to_Platform_SSO_to_obtain_the_profile}

>[!TIP]
>
> **<u>Sugerencia:</u>** Implemente esto a través del [Cuenta de suscriptor de vídeo](https://developer.apple.com/documentation/videosubscriberaccount) marco.


- La solicitud tendría que comprobar [permiso de acceso](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) la información de suscripción del usuario y continúe solo si el usuario la ha permitido.
- La solicitud tendría que presentar un [solicitud](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) para obtener información de la cuenta del suscriptor.
- La aplicación tendría que esperar y procesar el [metadata](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) información.

 

>[!TIP]
>
> **<u>Consejo de Pro:</u>** Siga el fragmento de código y preste especial atención a los comentarios.

```swift
    ...
    let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();
    
    videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
                switch (accessStatus) {
                // The user allows the application to access subscription information.
                case VSAccountAccessStatus.granted:
                        // Construct the request for subscriber account information.
                        let vsaMetadataRequest: VSAccountMetadataRequest = VSAccountMetadataRequest();
    
                        // This is actually the SAML Issuer not the channel ID.
                        vsaMetadataRequest.channelIdentifier = "https://saml.sp.auth.adobe.com";
        
                        // This is going to include subscription account information which should match the provider determined in a previous step.
                        vsaMetadataRequest.includeAccountProviderIdentifier = true;
                        
                        // This is going to include subscription account information which should match the provider determined in a previous step.
                        vsaMetadataRequest.includeAuthenticationExpirationDate = true;
                        
                        // This is going to make the Video Subscriber Account framework to refrain from prompting the user with the providers picker at this step. 
                        vsaMetadataRequest.isInterruptionAllowed = false;
    
                        // This are the user metadata fields expected to be available on a successful login and are determined from the [Adobe Primetime Authentication](/help/authentication/provide-mvpd-list.md) service. Look for the requiredMetadataFields associated with the provider determined in a previous step.
                        vsaMetadataRequest.attributeNames = requiredMetadataFields;
    
                        // This is the payload from [Adobe Primetime Authentication](/help/authentication/retrieve-profilerequest.md) service.
                        vsaMetadataRequest.verificationToken = profileRequestPayload;
                        
                        // Submit the request for subscriber account information.
                        videoSubscriberAccountManager.enqueue(vsaMetadataRequest) { vsaMetadata, vsaError in
                            if (vsaMetadata != nil && vsaMetadata!.samlAttributeQueryResponse != nil) {
                                var samlResponse: String? = vsaMetadata!.samlAttributeQueryResponse!;
                                
                                // Remove new lines, new tabs and spaces.
                                samlResponse = samlResponse?.replacingOccurrences(of: "[ \\t]+", with: " ", options: String.CompareOptions.regularExpression);
                                samlResponse = samlResponse?.components(separatedBy: CharacterSet.newlines).joined(separator: "");
                                samlResponse = samlResponse?.trimmingCharacters(in: CharacterSet.whitespacesAndNewlines);
                                
                                // Base64 encode.
                                samlResponse = samlResponse?.data(using: .utf8)?.base64EncodedString(options: []);
                                
                                // URL encode. Please be aware not to double URL encode it further.
                                samlResponse = samlResponse?.addingPercentEncoding(withAllowedCharacters: CharacterSet.init(charactersIn: "!*'();:@&=+$,/?%#[]").inverted);
                                
                                // Continue with the "Exchange the Platform SSO profile for an Adobe authentication token" step.
                                ...
                            } else {
                                // Fallback to regular authentication workflow.
                                ...
                            }
                        }
                        
                // The user has not yet made a choice or does not allow the application to access subscription information.
                default:
                    // Fallback to regular authentication workflow.
                    ...
                }
    }
    ...
```

</br>

#### Paso: &quot;Intercambie el perfil SSO de Platform por un token de autenticación de Adobe&quot; {#Exchange_the_Platform_SSO_profile_for_an_Adobe_authentication_token}

>[!TIP]
>
> **<u>Sugerencia:</u>** Implemente esto mediante la autenticación de Adobe Primetime [Token Exchange](/help/authentication/token-exchange.md) servicio.


>[!TIP]
>
> **<u>Consejo de Pro:</u>** Tenga en cuenta el fragmento de código de la variable [&quot;Reenviar la solicitud de Adobe a Platform SSO para obtener el perfil&quot;](#Forward_the_Adobe_request_to_Platform_SSO_to_obtain_the_profile) paso a paso. Esta *`vsaMetadata!.samlAttributeQueryResponse!`* representa la variable *`SAMLResponse`*, que debe transmitirse [Token Exchange](/help/authentication/token-exchange.md) y requiere manipulación y codificación de cadenas (*Base64* codificado y *URL* codificado posteriormente) antes de realizar la llamada.

</br>

#### Paso: &quot;¿El token de Adobe se genera correctamente?&quot; {#Is_Adobe_token_generated_successfully}

>[!TIP]
>
> **<u>Sugerencia:</u>** Implemente esto a través de la autenticación media de Adobe Primetime [Token Exchange](/help/authentication/token-exchange.md) respuesta correcta, que será *`204 No Content`*, indicando que el token se creó correctamente y está listo para utilizarse para los flujos de autorización.

</br>

#### Paso: &quot;Iniciar el flujo de trabajo de autenticación de la segunda pantalla&quot; {#Initiate_second_screen_authentication_workflow}

**Importante:** La terminología &quot;Segundo flujo de trabajo de autenticación de pantalla&quot; es adecuada para Apple TV, mientras que la terminología &quot;Primer flujo de trabajo de autenticación de pantalla&quot; / &quot;Flujo de trabajo de autenticación regular&quot; sería más apropiada para iPhone y iPads.


>[!TIP]
>
> **<u>Sugerencia:</u>** Implemente esto mediante la autenticación de Adobe Primetime

[Solicitud de código de registro](/help/authentication/registration-code-request.md), [Iniciar autenticación](/help/authentication/initiate-authentication.md) y [Token de autenticación de recuperación de API de REST](/help/authentication/retrieve-authentication-token.md) o [Comprobar token de autenticación](/help/authentication/check-authentication-token.md) servicios.


>[!TIP]
>
> **<u>Consejo de Pro:</u>** Siga los pasos a continuación para las implementaciones de tvOS.

- La solicitud tendría que [obtener un código de registro](/help/authentication/registration-code-request.md) y preséntela al usuario final en el primer dispositivo (pantalla).
- La aplicación tendría que iniciarse [sondeo para reconocer el estado de autenticación](/help/authentication/retrieve-authentication-token.md) en el primer dispositivo (pantalla) después de obtener el código de registro.
- Otra solicitud tendría que [iniciar autenticación](/help/authentication/initiate-authentication.md) en un segundo dispositivo (pantalla) cuando se utiliza el código de registro.
- La aplicación tendría que detenerse [sondeo](/help/authentication/retrieve-authentication-token.md) en el primer dispositivo (pantalla) cuando se genera el token de autenticación.

 

>[!TIP]
>
> **<u>Consejo de Pro:</u>** Siga los pasos que se indican a continuación para las implementaciones de iOS/iPadOS.

- La solicitud tendría que [obtener un código de registro](/help/authentication/registration-code-request.md) que no debe presentarse al usuario final en el primer dispositivo (pantalla).
- La solicitud tendría que [iniciar autenticación](/help/authentication/initiate-authentication.md) en el primer dispositivo (pantalla) que utiliza el código de registro y un [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) o [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) componente.
- La aplicación tendría que iniciarse [sondeo para conocer el estado de autenticación](/help/authentication/retrieve-authentication-token.md) en el primer dispositivo (pantalla) después del [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) o [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) cierre de componentes.
- La aplicación tendría que detenerse [sondeo](/help/authentication/retrieve-authentication-token.md) en el primer dispositivo (pantalla) cuando se genera el token de autenticación.

</br>

#### Paso: &quot;Proceder con flujos de autorización&quot; {#Proceed_with_authorization_flows}

>[!TIP]
>
> **<u>Sugerencia:</u>** Implemente esto mediante la autenticación de Adobe Primetime [Iniciar autorización](/help/authentication/initiate-authorization.md) y [Obtener token de medio corto](/help/authentication/obtain-short-media-token.md) servicios.

</br>

### Cerrar sesión {#Logout}

La variable [Cuenta de suscriptor de vídeo](https://developer.apple.com/documentation/videosubscriberaccount) framework no proporciona una API para cerrar la sesión mediante programación de las personas que han iniciado sesión en su cuenta de proveedor de TV a nivel de sistema de dispositivos. Por lo tanto, para que el cierre de sesión surta efecto, el usuario final tendría que cerrar sesión explícitamente desde *`Settings -> TV Provider`* en iOS/iPadOS o *`Settings -> Accounts -> TV Provider`* en tvOS. La otra opción que tendría el usuario es retirar el permiso para acceder a la información de suscripción del usuario de la sección de configuración específica de la aplicación (acceso del proveedor de TV).

>[!TIP]
>
> **<u>Sugerencia:</u>** Implemente esto mediante la autenticación de Adobe Primetime [Llamada de metadatos de usuario](/help/authentication/user-metadata.md) y [Cerrar sesión](/help/authentication/initiate-logout.md) servicios.


>[!TIP]
>
> **<u>Consejo de Pro:</u>** Siga los pasos a continuación para las implementaciones de tvOS.
 

- La aplicación tendría que determinar si la autenticación se ha producido como resultado de un inicio de sesión a través del SSO de la plataforma o no, utilizando el *tokenSource&quot;* [metadatos de usuario](/help/authentication/user-metadata.md) del servicio de autenticación de Adobe Primetime.
- La aplicación tendría que indicar/pedir al usuario que cierre la sesión explícitamente *`Settings -> Accounts -> TV Provider`* en tvOS **only** en caso de que *&quot;tokenSource&quot;* el valor es igual a &quot;*Apple&quot;.*
- La solicitud tendría que [iniciar el cierre de sesión](/help/authentication/initiate-logout.md) del servicio de autenticación de Adobe Primetime mediante una llamada HTTP directa. Esto no facilitaría la limpieza de la sesión en el lado MVPD.

 

>[!TIP]
>
> **<u>Consejo de Pro:</u>** Siga los pasos que se indican a continuación para las implementaciones de iOS/iPadOS.

- La aplicación tendría que determinar si la autenticación se ha producido como resultado de un inicio de sesión a través del SSO de la plataforma o no, utilizando el *tokenSource&quot;* [metadatos de usuario](/help/authentication/user-metadata.md) del servicio de autenticación de Adobe Primetime.
- La aplicación tendría que indicar/pedir al usuario que cierre la sesión explícitamente *`Settings -> TV Provider`* en iOS/iPadOS **only** en caso de que *&quot;tokenSource&quot;* el valor es igual a *&quot;Apple&quot;*.
- La solicitud tendría que [iniciar el cierre de sesión](/help/authentication/initiate-logout.md) del servicio de autenticación de Adobe Primetime mediante un [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) o [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) componente. Esto facilitaría la limpieza de la sesión en el lado MVPD.

<!--

## Resources

- [Apple SSO Overview](/help/authentication/apple-sso-overview.md)
- [REST API Overview](/help/authentication/rest-api-overview.md)
- [REST API Cookbook (Server-to-Server)](/help/authentication/rest-api-cookbook-servertoserver.md)
- [REST API Cookbook (Client-to-Server)](/help/authentication/rest-api-cookbook-clienttoserver.md)
- [REST API Reference](/help/authentication/rest-api-reference.md)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->

