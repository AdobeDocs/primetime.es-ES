---
title: Ámbitos del proveedor de servicios
description: Ámbitos del proveedor de servicios
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---


# Ámbitos del proveedor de servicios {#service-provoider-scoping}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Información general {#overview}

La implementación predeterminada de una integración de autenticación de Adobe Primetime con un MVPD se basa en la variable **Especificación de OLCA**. La sección Requisitos de autenticación de la especificación OLCA (6.5, Identificador de sujeto), indica que es posible indicar el ámbito del proveedor de servicios (SP) para el identificador del sujeto. (El identificador del asunto es el ID de usuario ofuscado que el MVPD devuelve al SP.)  En una integración de autenticación de Adobe Primetime, es necesario que los MVPD habiliten el alcance de las solicitudes de autenticación de SP.

Con la autenticación de Adobe Primetime asumiendo la función de SP para el programador, es necesario implementar una personalización que permita el alcance del SP de la solicitud de autenticación.  Esto debe hacerse para que el MVPD pueda identificar la marca de red pasada en la afirmación SAML al proveedor de identidad (IdP) del MVPD.  El ámbito se puede implementar de una de las dos maneras descritas en la siguiente sección.

## Ámbitos del proveedor de servicios {#service-provider-scoping}

La autenticación de Adobe Primetime admite las dos formas siguientes de habilitar el ámbito de SP de las solicitudes de autenticación:

* **Enfoque del emisor SAML.**  En este enfoque, el &quot;ID del solicitante&quot; se anexa a la cadena del emisor SAML en la solicitud de autenticación SAML.

* **El Enfoque De Propiedad De Creación De Ámbitos Personalizado.**  En este enfoque, el &quot;ID del solicitante&quot; se incluye explícitamente como una propiedad personalizada de &quot;creación de ámbitos&quot; en la solicitud de autenticación SAML.

>[!NOTE]
>
>El &quot;ID del solicitante&quot; es el modo en que la autenticación de Adobe Primetime se refiere a la marca de red del programador (por ejemplo: &quot;CNN&quot; es una de las marcas de la red Turner).

### Enfoque de emisor SAML {#saml-issuer-approach}

Este método utiliza SAML `<Issuer>` en la solicitud de autenticación SAML, como se muestra en este fragmento:

```xml
...
<saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
    http://saml.sp.adobe.adobe.com/on-behalf-of/requestorID
</saml:Issuer>
...
```

### Enfoque de propiedad de ámbitos personalizado {#custom-scoping-property-approach}

Este método utiliza una propiedad personalizada denominada &quot;Scoping&quot;, como se muestra en este fragmento de una solicitud de autenticación SAML:

```xml
...
<samlp:Scoping xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <samlp:RequesterID xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">requestorID</samlp:RequesterID>
</samlp:Scoping>
...
```

<!--
>[!RELATEDINFORMATION]
>* [MVPD Authentication](/help/authentication/authn-usecase.md)
>* **OLCA Specification**
-->