---
title: 'Actualizaciones de cookies: indicadores SameSite y Secure'
description: 'Actualizaciones de cookies: indicadores SameSite y Secure'
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---



# Actualizaciones de cookies: indicadores SameSite y Secure {#cookies-updates---samesite-and-secure-flags}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

</br>


## Actualizaciones {#Updates}

Esta sección resalta los cambios introducidos por el explorador Chrome y la autenticación de Adobe Primetime para gestionar cookies de terceros.

 

### Actualizaciones de Chrome 80 {#Chrome}

A partir de la versión 80 de Chrome (excepto la versión 82), las cookies que no especifican un *SameSite* se tratará como si *SameSite=Lax*. Por lo tanto, las cookies que deben enviarse en un contexto entre sitios deben especificar explícitamente la variable *SameSite=None*, y también deben marcarse con la variable *Secure* atributo y entregado *HTTPS*. Puede leer más detalles sobre estas actualizaciones en la página oficial del cromo: <https://www.chromium.org/updates/same-site> y también de <https://web.dev/samesite-cookies-explained/>.


### Actualizaciones de autenticación de Adobe Primetime {#Pass-Updates}

El servicio de autenticación de Adobe Primetime actualmente depende de un par de cookies que se consideran cookies de terceros desde el punto de vista del explorador, incluido Chrome, para funcionar en combinación con algunas plataformas y versiones de SDK de autenticación de Adobe Primetime. Por lo tanto, para cumplir con los próximos cambios y seguir entregando estas cookies en un contexto entre sitios desde estos SDK más antiguos, el servicio de autenticación de Adobe Primetime implementa los cambios necesarios en la variable *adobe-pass-2.55.1* versión.

Estos cambios con respecto a *adobe-pass-2.55.1* versión que implica añadir *Secure* y *SameSite=None* atributos de todas las cookies que se devuelven a todos los SDK de autenticación de Adobe Primetime al utilizar navegadores Chrome a partir de la versión 80 (excepto la versión 82).

En la siguiente sección se presentan algunos problemas potenciales para una lista de plataformas y las versiones del SDK de autenticación de Adobe Primetime en caso de que un usuario utilice el explorador Chrome 80 y versiones posteriores (excepto la versión 82).

## Resolución de problemas {#Troubleshooting}

Al navegar por esta sección, tenga en cuenta que todas las cookies del servicio de autenticación de Adobe Primetime deben tener *Secure* conjunto de atributos en *adobe-pass-2.55.1* para todos los exploradores, mientras que la variable *SameSite=None* solo debe configurarse para los exploradores Chrome versión 80 y posteriores (excepto la versión 82).


### Resolución de problemas generales {#General}

1. Es importante tener en cuenta que se sabe que algunos agentes de usuario son incompatibles con el *SameSite=None* atributo.

   - Versiones de Chrome de Chrome 51 a Chrome 66 (ambos extremos incluyen). Estas versiones de Chrome rechazarán una cookie con *SameSite=None*. Esto también afecta a versiones anteriores de exploradores derivados de Chromium, así como a Android WebView. Este comportamiento era correcto según la versión de la especificación de cookies en ese momento, pero con la adición del nuevo valor &quot;Ninguno&quot; a la especificación, este comportamiento se ha actualizado en Chrome 67 y versiones posteriores. (Antes de Chrome 51, el atributo SameSite se ignoraba completamente y todas las cookies se trataban como si fueran *SameSite=None*.)
   - Versiones del explorador UC en Android anteriores a la versión 12.13.2. Las versiones anteriores rechazarán una cookie con *SameSite=None*. Este comportamiento era correcto según la versión de la especificación de cookies en ese momento, pero con la adición del nuevo valor &quot;Ninguno&quot; a la especificación, este comportamiento se ha actualizado en versiones más recientes del Explorador UC.
   - Versiones de Safari y navegadores incrustados en MacOS 10.14 y todos los navegadores en iOS 12. Estas versiones tratarán erróneamente las cookies marcadas con *SameSite=None* como si estuvieran marcados *SameSite=Strict*. Este error se ha corregido en versiones más recientes de iOS y MacOS.


1. Es importante tener en cuenta que las cookies que tienen la variable *Secure* debe enviarse *HTTPS*, de lo contrario, la cookie no llegará al servicio de autenticación de Adobe Primetime.

   - SDK de JavaScript de AccessEnabler:
      - Obligatorio de que la comunicación con *sp.auth.adobe.com* uses *HTTPS* para versiones *2,35* y *3,5,0* antes de introducir el registro de cliente dinámico.
   - SDK de AccessEnabler iOS/tvOS:
      - Obligatorio de que la comunicación con *sp.auth.adobe.com* uses *HTTPS* para versiones anteriores a *3.0.0* antes de introducir el registro de cliente dinámico.
   - SDK para Android de AccessEnabler:
      - Obligatorio de que la comunicación con *sp.auth.adobe.com* uses *HTTPS* para versiones anteriores a *3.0.0* antes de introducir el registro de cliente dinámico.
   - SDK de AccessEnabler FireOS:
      - Obligatorio de que la comunicación con *sp.auth.adobe.com* uses *HTTPS* para la versión *2.0.4*.

</br>

### Solución de problemas del SDK de JavaScript versión 2.35 de AccessEnabler {#235-Troubleshooting}

El flujo de autenticación del usuario puede verse afectado en Chrome 80 y versiones posteriores (excepto en la versión 82). Para asegurarse de que el usuario no tenga problemas para autenticarse debido a las actualizaciones anteriores, puede:

- Compruebe que la variable *JSESSIONID* se configura en el explorador y se usa la variable *SameSite=None* y *Secure* conjunto de atributos. 
- Compruebe que la variable *JSESSIONID* desde la cookie *https://sp.auth.adobe.com/authenticate/saml* la solicitud de red coincide con el *JSESSIONID* desde la cookie *https://sp.auth.adobe.com/session* solicitud de red.


### Solución de problemas del SDK de JavaScript de AccessEnabler versión 3.5.0 {#350-Troubleshooting}

El flujo de autenticación del usuario puede verse afectado en Chrome 80 y versiones posteriores (excepto en la versión 82). Para asegurarse de que el usuario no tenga problemas para autenticarse debido a las actualizaciones anteriores, puede:

- Compruebe que la variable *JSESSIONID* se configura en el explorador y se usa la variable *SameSite=None* y *Secure* conjunto de atributos. 
- Compruebe que la variable *JSESSIONID* desde la cookie *https://sp.auth.adobe.com/authenticate/saml* la solicitud de red coincide con el *JSESSIONID* desde la cookie *https://sp.auth.adobe.com/session* solicitud de red.
- Compruebe que la variable *pass\_sfp* se configura en el explorador y se usa la variable *SameSite=None* y *Secure* conjunto de atributos.
- Compruebe que la variable *pass\_sfp* cookie se configura en *https://sp.auth.adobe.com/session* solicitud de red.


El flujo de autorización del usuario podría verse afectado en Chrome 80 y versiones posteriores (excepto en la versión 82). Para asegurarse de que el usuario no tenga problemas para ver un recurso protegido, después de autenticarse correctamente, debido a las actualizaciones anteriores, puede:

- Compruebe que la variable *pass\_sfp* se configura en el explorador y se usa la variable *SameSite=None* y *Secure* conjunto de atributos.
- Compruebe que la variable *pass\_sfp* cookie se configura en *https://sp.auth.adobe.com/adobe-services/authorize* solicitud de red.
- Compruebe que la variable *pass\_sfp* cookie se configura en *https://sp.auth.adobe.com/adobe-services/shortAuthorize* solicitud de red.
