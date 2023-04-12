---
title: Intercambio de metadatos de usuario de MVPD
description: Intercambio de metadatos de usuario de MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 0%

---


# Intercambio de metadatos de usuario de MVPD

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Introducción {#intro-user-metadata-exchange}

Los MVPD mantienen metadatos específicos del usuario sobre sus clientes que, en algunos casos, se comparten con los programadores. El objetivo de la autenticación de Adobe Primetime es intermediar en un intercambio de estos &quot;metadatos de usuario&quot;, pero no hacer cumplir ningún tipo de reglas con respecto al intercambio. Las reglas de intercambio son para que los MVPD trabajen con sus socios programadores.

Los tipos de metadatos de usuario disponibles para intercambiar incluyen actualmente lo siguiente:

* Código postal
* Clasificación máxima (VChip o MPAA)
* ID de usuario
* ID del hogar
* ID de canal

Con esta función, los MVPD y los programadores pueden implementar casos de uso especiales, como el control parental. Por ejemplo, un MVPD puede pasar los datos de clasificación parental a un programador, que luego utiliza esos datos para filtrar las opciones de visualización disponibles para un usuario.

Puntos clave de metadatos de usuario:

* El MVPD pasa los metadatos de usuario a la aplicación del programador durante los flujos de autenticación y autorización
* La autenticación de Adobe Primetime guarda los valores de metadatos en los tokens AuthN y AuthZ
* La autenticación de Adobe Primetime puede normalizar valores para MVPD que proporcionan metadatos de usuario en diferentes formatos
* Algunos parámetros pueden cifrarse con la clave del programador
* Los valores específicos están disponibles por Adobe a través de un cambio de configuración

>[!NOTE]
>
>Los metadatos de usuario son una extensión de los metadatos estáticos (TTL token de autenticación, TTL token de autorización e ID de dispositivo) disponibles anteriormente en la autenticación de Adobe Primetime.

## Ejemplos {#example-mvpd-user-metadata-exch}

### Control parental {#example-parental-control}

Este ejemplo muestra el intercambio de lo siguiente:

* [Intercambio de metadatos de Programador a MVPD](#progr-mvpd-metadata-exch)

* [Flujo de intercambio de metadatos de MVPD a Programador](#mvpd-progr-exchange-flow)

### Intercambio de metadatos de Programador a MVPD {#progr-mvpd-metadata-exch}

Actualmente, la API de programador, la autenticación de Adobe Primetime y los Autorizadores de MVPD solo admiten la autorización a nivel de canal. El canal se especifica como una cadena de texto sin formato en la llamada de API getAuthorization() del programador. Esta cadena se propaga hasta el back-end de autorización del MVPD:

Desde la aplicación o sitio del programador, el usuario elige un MVPD capaz de XACML (en este ejemplo, &quot;TNT&quot;). Para obtener información sobre XACML, consulte [Lenguaje de marcado de control de acceso extensible](https://en.wikipedia.org/wiki/XACML){target=_blank}.
La aplicación del programador forma una solicitud AuthZ que incluye el recurso y sus metadatos.  Este ejemplo incluye una clasificación MPAA de &quot;pg&quot; en el atributo media del elemento channel:

```XML
var resource = '<rss version="2.0" xmlns:media="http://video.search.yahoo.com/mrss/">
                    <channel> 
                        <title>TNT</title> 
                        <media:rating scheme="urn:mpaa">pg</media:rating>
                    </channel>
                </rss>';
getAuthorization(resource);
```

La autenticación de Adobe Primetime es compatible con una autorización más granular, hasta el nivel de recurso, cuando la admite el MVPD y el Programador. El recurso y sus metadatos son opacos para el Adobe; la intención es establecer un formato estándar para especificar el ID de recurso y los metadatos de forma normalizada, para enviar ID de recurso a diferentes MVPD.

>[!NOTE]
>
>Si el usuario elige un MVPD capaz de solo canales, la autenticación de Adobe Primetime extrae SOLO el título del canal (&quot;TNT&quot; en el ejemplo anterior) y pasa solamente el título al MVPD.

### Flujo de intercambio de metadatos de MVPD a Programador {#mvpd-progr-exchange-flow}

La autenticación de Adobe Primetime realiza las siguientes presuposiciones:

* El MVPD envía la clasificación máxima como parte de la respuesta SAML
* Esta información se guarda como parte del token de autenticación
* La autenticación de Adobe Primetime proporciona una API para permitir a los programadores recuperar esta información
* Los programadores implementan esta función en su sitio o aplicación (por ejemplo, para ocultar vídeos que superen la clasificación máxima del usuario)

```XML
<saml:Assertion ID="pfxec5f92e0-8589-3fc3-c708-f4fb8e2fad59"
                 IssueInstant="2010-07-20T10:05:41Z" Version="2.0"
                 xmlns:xs="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <saml:AttributeStatement>
        <saml:Attribute
                Name="MaxTVRating"
                NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
            <saml:AttributeValue xsi:type="xs:string">tv-ma</saml:AttributeValue>
        </saml:Attribute>
        <saml:Attribute
                Name="MaxMovieRating"
                NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
            <saml:AttributeValue xsi:type="xs:string">nc-17</saml:AttributeValue>
        </saml:Attribute>
    </saml:AttributeStatement>
</saml:Assertion>
```

### Notas {#notes-mvpd-progr-metadata-exch-flow}

**Normalización y validación de recursos.** Los ID de recurso se pueden pasar como una cadena sin formato o una cadena MRSS. Un programador puede decidir utilizar el formato de cadena simple o el MRSS, pero necesitará un acuerdo previo con el MVPD para que el MVPD sepa cómo tratar ese recurso.

**ID de recurso y especificación de metadatos.** La autenticación de Adobe Primetime utiliza el estándar RSS con la extensión Media RSS para especificar un recurso y sus metadatos. Junto con la extensión Media RSS, la autenticación de Adobe Primetime admite una amplia variedad de metadatos, como controles parentales (mediante `<media:rating>`) o geolocalización (`<media:location>`).

La autenticación de Adobe Primetime también puede admitir la conversión transparente de la cadena de canal heredada al recurso RSS correspondiente para los MVPD que requieren RSS. En la otra dirección, la autenticación de Adobe Primetime admite la conversión de RSS+MRSS a título de canal sin formato, para MVPD de solo canal.

**La autenticación de Adobe Primetime garantiza la compatibilidad total con versiones anteriores de las integraciones existentes.** Es decir, para los programadores que utilizan autenticación de nivel de canal, la autenticación de Adobe Primetime se encarga de empaquetar el ID de canal en el formato necesario antes de enviarlo a un MVPD que comprenda ese formato. Lo contrario también se aplica: si un programador especifica todos sus recursos en un nuevo formato, la autenticación de Adobe Primetime traduce el nuevo formato a una cadena de canal simple si la autorización se realiza con un MVPD que solo realiza la autorización a nivel de canal.

## Casos de uso de metadatos de usuario {#user-metadata-use-cases}

Los casos de uso cambian constantemente y se expanden a medida que más MVPD realizan arreglos legales y agregan funcionalidad. A continuación se muestran algunos ejemplos de uso de los metadatos de usuario.

* [ID de usuario de MVPD](#mvpd-user-id)
* [ID del hogar](#household-user-id)
* [Código postal](#zip-code)
* [Clasificación máxima (Control parental)](#max-rating-parental-control)
* [Vinculación de canales](#channel-line-up)

### ID de usuario de MVPD {#mvpd-user-id}

* Según lo previsto por la MVPD
* No la información de inicio de sesión real del usuario, ya que está almacenada en hash por el MVPD
* Se puede utilizar para indicar problemas con o para usuarios específicos
* Cifrado
* Compatibilidad con MVPD: Todos los MVPD

### ID de usuario del hogar {#household-user-id}

* Permite una buena información de métricas
* Cifrado
* Compatibilidad con MVPD: Algunos MVPD

### Código postal {#zip-code}

* El código postal de facturación del usuario
* Se utiliza principalmente para aplicar las reglas del periodo de congelación de eventos del Sporting
* Se puede proporcionar con la respuesta AuthZ para actualizaciones rápidas
* Compatibilidad con MVPD: Algunos MVPD

### Clasificación máxima (Control parental) {#max-rating-parental-control}

* Inicialmente, AuthN más la actualización de AuthZ
* Filtrado de contenido fuera de la interfaz de usuario
* Clasificaciones MPAA o VChip
* Compatibilidad con MVPD: Algunos MVPD

### Vinculación de canales {#channel-line-up}

* Los MVPD pueden proporcionar una lista de canales que el usuario puede ver
* Permite la pintura rápida de la interfaz de usuario
* La especificación OLCA permite esto como una AttributeStatement en la respuesta AuthN
* Soporte de MVPD: Algunos MVPD

<!--
>[!RELATEDINFORMATION]
>
>* [Proxy MVPD Web Service](/help/authentication/proxy-mvpd-webserv.md)
>* [Content Metadata Exhange](/help/authentication/mvpd-content-metadata-exchange.md)
>* [OLCA AuthN / AuthZ Specification](https://www.cablelabs.com/specifications/CL-SP-AUTH1.0-I04-120621.pdf){target=_blank}
>* [User Metadata (Programmer Integration Guide)](/help/authentication/user-metadata-feature.md)
-->
