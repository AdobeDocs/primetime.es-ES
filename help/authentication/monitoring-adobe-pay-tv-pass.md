---
title: Supervisión de la autenticación de Adobe Primetime
description: Supervisión de la autenticación de Adobe Primetime
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# Supervisión de la autenticación de Adobe Primetime {#monitoring-adobe-primetime-authentication}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Introducción {#intro}

Los clientes pueden utilizar [Nagios](http://www.nagios.org) u otras herramientas para comprobar si la autenticación de Adobe Primetime está activada o desactivada. 

## Monitorización de extremos {#monitoring-endpoints}

### Puntos finales que se pueden monitorizar {#endpoints-to-monitor}

* El punto final de configuración para todas las plataformas: `https://sp.auth.adobe.com/adobe-services/config/[your-config-ID]`: está disponible a través de HTTP o HTTPS (según la opción que realice el desarrollador del proveedor de contenido). Si falta este punto final, significa que el contenido no estará disponible en todas las plataformas y todos los MVPD. Para la API de REST sin cliente también tenemos el siguiente punto final:  `https://api.auth.adobe.com/adobe-services/config your-config-ID]`.

* Los siguientes extremos son parte del SDK web de autenticación de Adobe Primetime.  Si falta, significa que pay-TVpass está caído para todos los programadores y todas las propiedades web:

   * `https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js`
   * `https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js`

 
### Puntos de conexión que no se deben monitorizar {#endpoints-not-monitor}

* `https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer`

   Siempre recibirá un error 503, porque este extremo necesita una respuesta SAML de MVPD.

* Otros puntos finales de derecho - `adobe-services/1.0/authenticate/`, `adobe-services/1.0/deviceShortAuthorize`, `adobe-services/1.0/authorize`

No puede monitorizar estos extremos porque necesitan una carga útil para obtener una respuesta relevante.
