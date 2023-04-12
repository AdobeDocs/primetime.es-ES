---
title: Intercambio de metadatos de contenido MVPD
description: Intercambio de metadatos de contenido MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Intercambio de metadatos de contenido MVPD

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Información general {#content-metadat-exchange-overview}

Esta página describe dos implementaciones estándar que utiliza la autenticación de Adobe Primetime para enviar datos estructurados a MVPD en la solicitud de autorización.  Los datos estructurados representan el recurso (el programador) que realiza la solicitud y, posiblemente, datos adicionales, como la clasificación de contenido.

En el lado del programador, la autenticación de Adobe Primetime admite los recursos de datos MRSS estructurados de la siguiente manera:

1. El programador envía el recurso como una cadena MRSS. La autenticación de Adobe Primetime no la codifica en el lado del cliente para dispositivos web o nativos. El MRSS se envía como una cadena normal al servidor de autenticación de Adobe Primetime.
1. En el servidor, el MRSS se valida con el esquema predefinido (http://search.yahoo.com/mrss/).  Si la validación pasa, la autenticación de Adobe Primetime extrae la información de los campos MRSS, incluidos:
   * título del canal
   * título del elemento
   * identificador de recurso
   * valor y tipo de clasificación
1. Los valores extraídos del MRSS se utilizan para crear la solicitud de autorización que se pasa al MVPD.

La autenticación de Adobe Primetime admite dos métodos para traducir el MRSS a formatos admitidos por los MVPD:

* **XACML**.  El primer enfoque se alinea con el estándar OLCA.  Utiliza XACML, en el que se extraen los valores MRSS para crear un XACMLResource con atributos que se asignan a los elementos MRSS.  A continuación, esto se pasa al MVPD.
* **REST**.  El segundo enfoque se basa en REST.  El MRSS está codificado en base64 y se pasa como parámetro de URL en la llamada REST.

En ambos enfoques, el MVPD procesa la solicitud de autorización incluyendo los valores extraídos dentro de su propio flujo lógico y devolviendo una respuesta de autorización.

## Detalles de la integración {#integration-details}

* Recurso estructurado XACML basado en OLCA
* Recurso estructurado basado en REST

### Recurso estructurado XACML basado en OLCA {#olca-based-xacml-struc-resource}

La mayoría de los MVPD orientados a cable utilizan el enfoque basado en XACML, pero aún no admiten el enfoque de datos estructurado en su totalidad.  Otros MVPD que admiten XACML toman el Título del canal y lo aceptan para el atributo ResourceID. El ejemplo siguiente muestra el enfoque basado en XACML estructurado completamente. El equipo de autenticación de Adobe Primetime recomienda que para los MVPD que utilizan XACML, pero que aún no admiten funciones como controles parentales, adapten su integración XACML al siguiente ejemplo:

```XML
<?xml version="1.0" encoding="UTF-8"?>
<soap11:Envelope xmlns:soap11=">
    <soap11:Header/>
    <soap11:Body>
        <xacml-samlp:XACMLAuthzDecisionQuery
                xmlns:xacml-samlp="urn:oasis:names:tc:xacml:2.0:profile:saml2.0:v2:schema:protocol"
                Destination="
                ID="_f1dd34469c5aeac016760e51dbba007d" IssueInstant="2012-06-26T16:30:24.879Z" Version="2.0">
            <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
                https://saml.sp.auth.adobe.com/
            </saml:Issuer>
            <ds:Signature xmlns:ds=">.......</ds:Signature>
            <xacml-context:Request xmlns:xacml-context="urn:oasis:names:tc:xacml:2.0:context:schema:os">
                [....info skipped for brevity....]
                <xacml-context:Resource>
 
        // The MRSS item GUID is passed as the XACML Resource resource-id
                    <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id">
                        <xacml-context:AttributeValue>DISNEY_GUID_12345</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
        // The MRSS channel title is passed as the XACML Resource tv-network
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:tv-network">
                        <xacml-context:AttributeValue>Disney</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
        // Adobe doesn't yet support an explicit namespace for the GUID, so we reuse the channel title as the GUID.  
        // We expect to add an explicit namespace later next year pulling it from the GUID scheme attribute.
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:id:namespace">
                        <xacml-context:AttributeValue>Disney</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
        // The MRSS item title is passed as the XACML Resource content title
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:title">
                        <xacml-context:AttributeValue>Disney Program X</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
        // The MRSS media rating is passed as the XACML Resource content rating 
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:rating:vchip">
                        <xacml-context:AttributeValue>TV-Y</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
                </xacml-context:Resource>
 
                <xacml-context:Action>
                    <xacml-context:Attribute>
                        <xacml-context:AttributeValue>VIEW</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
                </xacml-context:Action>
 
                [.....info skipped for brevity....]
            </xacml-context:Request>
        </xacml-samlp:XACMLAuthzDecisionQuery>
    </soap11:Body>
</soap11:Envelope>
 
//formatted for readability
```

### Recurso estructurado basado en REST {#rest-based-struct-resource}

Algunos MVPD han estandarizado en el siguiente protocolo de autorización basado en REST. Este enfoque se presenta tan completo como el enfoque XACML, pero proporciona una implementación de &quot;menor peso&quot;.

`// The MRSS is base64 encoded by Adobe Primetime authentication, and passed in that format to the REST-based Authorization endpoint.`

`https://auth.somedomain.net/mediation/1/rest/client/authz?uuID=AC82CE4&mrss=base64encodedstring&IPAddress=123.456.78.901`

<!--
>[!RELATEDINFORMATION]
>* [User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Logout](/help/authentication/usecase-mvpd-logout.md)
>* [Programmer Integration Guide: Identifying Protected Resources](/help/authentication/identify-protected-resources.md)
>* [Programmer Integration Guide: User Metadata Exchange](/help/authentication/user-metadata.md)
-->