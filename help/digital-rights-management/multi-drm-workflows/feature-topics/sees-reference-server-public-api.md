---
description: La solicitud de asignación de derechos y la respuesta se pasan a través de una conexión SSL mutuamente autenticada entre el servidor de licencias y el servicio de asignación de derechos del cliente.
seo-description: La solicitud de asignación de derechos y la respuesta se pasan a través de una conexión SSL mutuamente autenticada entre el servidor de licencias y el servicio de asignación de derechos del cliente.
seo-title: SEIS Public API
title: SEIS Public API
uuid: f3a17d61-04ee-4bdb-9d64-a98066c6d1c8
translation-type: tm+mt
source-git-commit: 15403abbd53486e1faa2146cda83f41bd8116632
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# SEES Public API {#sees-public-api}

La solicitud de asignación de derechos y la respuesta se pasan a través de una conexión SSL mutuamente autenticada entre el servidor de licencias y el servicio de asignación de derechos del cliente.

El esquema de URI HTTPS ( [https://tools.ietf.org/html/rfc7230#section-2.7.2](https://tools.ietf.org/html/rfc7230#section-2.7.2)) se utiliza para definir el extremo de asignación de derechos y el método de solicitud de POST HTTP ( [https://tools.ietf.org/html/rfc7231#section-4.3.3](https://tools.ietf.org/html/rfc7231#section-4.3.3)) se utiliza para la solicitud. El extremo de asignación de derechos, así como un indicador que indica la asignación de derechos en el back-end, son obligatorios y deben incluirse en la directiva en el momento del empaquetado.

## Solicitud de asignación de derechos {#section_BFBFEF0795CA46D6842C479256B95F95}

El cuerpo de la solicitud de asignación de derechos será un objeto JSON definido como se muestra a continuación.

**Definición de objeto de solicitud de asignación de derechos JSON**

```
{ 
 "title" : "Entitlement Request", 
 "type" : "object", 
 "properties" : { 
  "messageID" : { 
   "type" : "string", 
   "description" : "Unique ID for this message (GUID).  Used to confirm that the subsequent response is actually for this request." 
  }, 
  "version" : { 
   "type" : "integer", 
   "description" : "Version number of the protocol, currently 1." 
  }, 
  "requestType" : { 
   "type" : "integer", 
   "description" : "Request type. 1 - time based entitlement request, 2 - device registration entitlement request 3 - device bound entitlement request." 
  }, 
  "contentID" : { 
   "type" : "string", 
   "description" : "Content ID (GUID) that was given to the content during packaging time." 
  }, 
  "customerCookie" : { 
   "type" : "string", 
   "description" : "Customer cookie. Cookie is just arbitrary string up to 32 characters long." 
  } 
    }, 
 "required" : ["messageID", "version", "contentID"] 
}
```

## Respuesta de asignación de derechos {#section_F15A9FD6BAD946B3B4C5C14612F90154}

El cuerpo de la respuesta de asignación de derechos es un objeto JSON.

**Definición de objeto de respuesta de asignación de derechos JSON**

```
{ 
  "title" : "Entitlement Response", 
  "type" : "object", 
  "properties" : { 
    "messageID" : { 
    "type" : "string", 
    "description" : "Unique ID from the Entitlement Request message.   
      Must match, or entitlement will be denied." 
  }, 
  "version" : { 
    "type" : "integer", 
    "description" : "Version number of the protocol; must be <= the version number  
      from the Entitlement Request message." 
  }, 
  "isAllowed" : { 
    "type" : "boolean", 
    "description" : "Grant the license or not." 
  }, 
  "epTokenURL" : { 
    "type" : "string", 
    "description" : "ExpressPlay Token URL" 
  }, 
  "error" : { 
    "type" : "integer", 
    "description" : "An error number produced by the entitlement server.  
      Will be passed to the client as the 'code' field of the server error response." 
  }, 
  "errorText" : { 
    "type" : "string", 
    "description" : "Additional error information produced by the entitlement server.  
      Will be passed to the client as the 'text' field of the server error response." 
  }, 
  "required" : ["messageID", "version", "isAllowed", "epTokenURL"] 
}
```
