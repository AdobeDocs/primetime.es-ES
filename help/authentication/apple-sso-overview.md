---
title: Información general de Apple SSO
description: Información general de Apple SSO
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1452'
ht-degree: 0%

---



# Información general de Apple SSO {#apple-sso-overview}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Introducción {#Introduction}

Apple proporciona una API que permite a las personas iniciar sesión en su cuenta de proveedor de TV a nivel de sistema de dispositivo, lo que elimina la necesidad de autenticarse en cada aplicación.

Por lo tanto, Apple y Adobe Primetime Authentication se asociaron para crear la experiencia de usuario de Single Sign-On (SSO) de la plataforma en el ecosistema de TV en todas partes para propietarios de iPhone, iPad y Apple TV.

Para beneficiarse de la experiencia de usuario del inicio de sesión único (SSO) en un dispositivo Apple, hay una lista de requisitos previos que deben completarse.

</br>

## Requisitos previos {#Prerequisites}

Los requisitos previos pueden aplicarse a una o varias entidades involucradas en el negocio de TVE, como programadores, MVPD, autenticación de Adobe Primetime o Apple.

</br>

### Programador {#Programmer}

Para beneficiarse de la experiencia de usuario del Registro único (SSO), un programador debe:

1. Utilice al menos Xcode versión 8 y iOS/tvOS versión 10.

1. Tenga la variable [Derecho de inicio de sesión único del suscriptor de vídeo](https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_developer_video-subscriber-single-sign-on) configurado en su cuenta de desarrollador de Apple. Póngase en contacto con Apple para habilitar [Marco de cuentas de suscriptor de vídeo](https://developer.apple.com/documentation/videosubscriberaccount) para su ID de equipo de Apple.

1. Habilite el inicio de sesión único (YES) para cada integración deseada (Canal x MVPD) y la plataforma deseada (iOS / tvOS) a través del [TVE Dashboard de Adobe Primetime](https://console.auth.adobe.com/).

1. Integre los flujos de trabajo SSO de Apple mediante una de las dos soluciones siguientes que ofrece el equipo de autenticación de Adobe Primetime:

   - La API de REST de autenticación de Adobe Primetime puede admitir la autenticación de inicio de sesión único (SSO) de plataforma para usuarios finales de aplicaciones cliente que se ejecuten en iOS, iPadOS o tvOS. Consulte también [Guía de Apple SSO (API de REST)](/help/authentication/apple-sso-cookbook-rest-api.md).

   - El SDK de Adobe Primetime Authentication AccessEnabler iOS/tvOS puede admitir la autenticación de plataforma Single Sign-On (SSO) para usuarios finales de aplicaciones cliente que se ejecuten en iOS, iPadOS o tvOS. Consulte también [Guía de Apple SSO (SDK de iOS/tvOS)](/help/authentication/apple-sso-cookbook-iostvos-sdk.md).

   - **<u>Consejo de Pro:</u>** Para tener acceso a la información de suscripción del usuario, el usuario debe dar permiso a la aplicación para continuar, de forma similar a proporcionar acceso a la cámara o el micrófono del dispositivo. Este permiso debe solicitarse por aplicación y el dispositivo guardará la selección del usuario. Tenga en cuenta que el usuario puede cambiar su decisión accediendo a la configuración de la aplicación (acceso de permiso del proveedor de TV) o a la sección desde *`Settings -> TV Provider`* en iOS/iPadOS o *`Settings -> Accounts -> TV Provider`* en tvOS.

   - **<u>Consejo de Pro:</u>** Se recomienda solicitar el permiso del usuario cuando la aplicación entre en estado de primer plano, pero es solo una sugerencia, ya que la aplicación puede comprobar [permiso de acceso](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) la información de suscripción del usuario en cualquier momento antes de requerir la autenticación del usuario. Además, las API del SDK de iOS/tvOS de AccessEnabler solicitarán automáticamente el permiso del usuario cuando lo necesite.

   - **<u>Consejo de Pro:</u>** Recomendamos incentivar a los usuarios que se nieguen a dar permiso para acceder a la información de suscripción explicando las ventajas de la experiencia de usuario del inicio de sesión único (SSO). Tenga en cuenta que el usuario puede cambiar su decisión accediendo a la configuración de la aplicación (acceso de permiso del proveedor de TV) o a la sección desde *`Settings -> TV Provider`* en iOS/iPadOS o *`Settings -> Accounts -> TV Provider`* en tvOS.

El resultado debe crear una experiencia en línea con los siguientes flujos de usuario, que le sugerimos consultar antes de comenzar a desarrollar la aplicación:

- [iPhone/iPad](http://tve.zendesk.com/hc/article_attachments/205624966/User_flows_AppleSSO_iOS_v2.pdf) flujos de usuario
- [Apple TV](http://tve.zendesk.com/hc/article_attachments/206669126/User_flows_tvOS.pdf) flujos de usuario


>[!IMPORTANT]
>
> Cuando la función Inicio de sesión único está **enabled** para iOS/tvOS **y** en el caso de Apple **ya incorporado (compatible) o selector** MVPD Los flujos de autenticación/cierre de sesión procedentes de los flujos de trabajo de SSO de Apple implicarán las soluciones de autenticación de Apple y Adobe Primetime, mientras que todos los demás flujos (autorización, preautorización, metadatos, etc.) solo recibirá el servicio de autenticación de Adobe Primetime.


>[!IMPORTANT]
>
> Cuando la función Inicio de sesión único está **disabled** para iOS/tvOS **o** en el caso de Apple **no integrado (no compatible)** MVPD Los flujos de autenticación/cierre de sesión se devolverán de los flujos de trabajo de SSO de Apple a los normales a los que solo presta servicio la autenticación de Adobe Primetime.


>[!IMPORTANT]
>
> Una de las principales ventajas del flujo de trabajo de Apple SSO es el flujo de usuario de autenticación de una pantalla, que también se puede entregar en Apple TV cuando la función Inicio de sesión único está **enabled** para tvOS **y** en el caso de Apple **Incorporado (compatible)** MVPD.


### MVPD {#MVPD}

Para beneficiarse de la experiencia de usuario del Registro único (SSO), un MVPD debe:

 

1. Se debe incorporar al flujo de trabajo de Apple SSO en Apple. Póngase en contacto con Apple para facilitar el proceso de incorporación.
1. Proporcionar una aplicación TVML de JavaScript capaz de gestionar el formulario de inicio de sesión del usuario. Póngase en contacto con Apple para recibir la documentación adecuada.
1. Proporcione un valor de cadena que represente el identificador de proveedor asignado por Apple durante el proceso de incorporación. Póngase en contacto con la autenticación de Adobe Primetime para realizar cambios en la configuración.

</br>

## Preguntas frecuentes {#FAQ}

1. En caso de que algo salga mal en el flujo de trabajo de SSO de Apple, ¿puede la aplicación que utiliza el SDK de AccessEnabler iOS/tvOS tener la capacidad de realizar un seguimiento del flujo de autenticación normal?
   - Esto es posible, pero requiere que se realice un cambio de configuración en la variable [TVE Dashboard de Adobe Primetime](https://console.auth.adobe.com/). La variable *Habilitar el inicio de sesión único* debe estar activado *NO* para la integración deseada (Canal x MVPD) y la plataforma deseada (iOS/tvOS).
   - La aplicación solo reconocería el cambio de configuración después de llamar a [setRequestor](/help/authentication/iostvos-sdk-api-reference.md#setReqV3) en caso de que utilice el SDK de AccessEnabler iOS/tvOS.
1. ¿Sabe la aplicación cuándo se ha producido una autenticación como resultado de un inicio de sesión a través del SSO de la plataforma en otro dispositivo u otra aplicación?
   - Esta información no estará disponible.
1. ¿Sabe la aplicación cuándo se ha producido una autenticación como resultado de un inicio de sesión a través del SSO de la plataforma en el mismo dispositivo? 
   - Esta información está disponible como parte de la clave de metadatos del usuario: *tokenSource*, que debería devolver el valor de la cadena: &quot;Apple&quot; en este caso.
1. ¿Qué sucede si un usuario inicia sesión yendo a la *`Settings -> TV Provider`* en iOS/iPadOS o *`Settings -> Accounts -> TV Provider`* en la sección tvOS utilizando un MVPD que no está integrado con la aplicación?
   - Cuando el usuario inicia la aplicación, este no se autentica mediante el flujo de trabajo de Apple SSO. Por lo tanto, la aplicación tendría que recurrir al flujo de autenticación regular y presentar su propio selector de MVPD.
1. ¿Qué sucede si un usuario inicia sesión yendo a la *`Settings -> TV Provider`* en iOS/iPadOS o *`Settings -> Accounts -> TV Provider`* en la sección tvOS usando un MVPD que tiene el *Habilitar el inicio de sesión único* configurado *NO* en el [TVE Dashboard de Adobe Primetime](https://console.auth.adobe.com/) para la plataforma iOS/tvOS?
   - Cuando el usuario inicia la aplicación, este no se autentica mediante el flujo de trabajo de Apple SSO. Por lo tanto, la aplicación tendría que recurrir al flujo de autenticación regular y presentar su propio selector de MVPD.
1. ¿Qué sucede si un usuario tiene un MVPD que Apple no ha incorporado (no admite), pero que está presente en el selector de Apple?
   - Cuando el usuario inicia la aplicación, solo selecciona el MVPD mediante el flujo de trabajo de Apple SSO sin completar el flujo de autenticación. Por lo tanto, la aplicación tendría que recurrir al flujo de autenticación regular, pero podría utilizar el MVPD ya seleccionado.
1. ¿Qué sucede si un usuario tiene un MVPD que Apple no incorpora (no admite)?
   - Cuando el usuario inicia la aplicación, selecciona la opción de selector &quot;Otros proveedores de TV&quot; a través del flujo de trabajo de Apple SSO. Por lo tanto, la aplicación tendría que recurrir al flujo de autenticación regular y presentar su propio selector de MVPD.
1. Qué sucede si un usuario tiene un MVPD degradado a través del medio de [TVE Dashboard de Adobe Primetime](https://console.auth.adobe.com/)?
   - Cuando el usuario inicia la aplicación, se autentica mediante el mecanismo de degradación y no mediante el flujo de trabajo de Apple SSO.
   - La experiencia debe ser perfecta para el usuario, mientras que la aplicación se informará a través del *N010* código de advertencia en caso de que utilice el SDK de AccessEnabler iOS/tvOS.
1. ¿Cambiará el ID de usuario de MVPD entre Apple SSO y el flujo de autenticación SSO que no sea de Apple?
   - La expectativa es que el ID de usuario no cambie, pero debe verificarse para cada proveedor seleccionado. 
1. ¿Habrá algún cambio en los TTL de autenticación?
   - La autenticación de Adobe Primetime seguirá respetando los TTL requeridos por los programadores para su integración con cada MVPD.
   - Cuando se navega de una aplicación Programer a otra aplicación Programador a través de Apple SSO, la segunda aplicación tendrá el TTL de su integración correspondiente Programer x MVPD (no compartirá el TTL de la primera aplicación que se autentique)

|  | TTL de autenticación de Adobe Primetime caducado | TTL de autenticación de Adobe Primetime válido |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| **El TTL del token del dispositivo Apple expiró** | El usuario NO está autenticado (debería aparecer el selector de MVPD) | El usuario está autenticado y el TTL es el tiempo restante de su token de autenticación de Adobe Primetime |
| **TTL del token del dispositivo Apple válido** | El usuario se autentica silenciosamente y obtiene otro token de autenticación de Adobe Primetime con el TTL especificado en el panel de control de Televisión | El usuario está autenticado y el TTL es el tiempo restante de su token de autenticación de Adobe Primetime |

<!--

## Resources {#Resources}

- [Apple SSO Cookbook (REST API)](/help/authentication/apple-sso-cookbook-rest-api.md)
- [Apple SSO Cookbook (iOS/tvOS SDK)](/help/authentication/apple-sso-cookbook-iostvos-sdk.md)
- [Sign in with your TV provider on your iPhone, iPad, or iPod touch](https://support.apple.com/en-us/HT207035)
- [Use your pay TV or cable provider with Apple TV](https://support.apple.com/en-us/HT207035)
- [TV providers that let you sign in on your iPhone, iPad, or Apple TV](https://support.apple.com/en-us/HT208084)
- [TV Provider Authentication](https://developer.apple.com/design/human-interface-guidelines/tvos/system-capabilities/tv-provider-authentication/)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->
