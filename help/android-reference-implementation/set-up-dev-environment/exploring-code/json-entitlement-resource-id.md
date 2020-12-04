---
seo-title: Objeto JSON para el ID de recurso de asignación de derechos
title: Objeto JSON para el ID de recurso de asignación de derechos
uuid: f5b659da-1732-404c-bf00-d32a0ae39aa1
description: El siguiente bloque de código proporciona un ejemplo de un objeto JSON cuando el ID del recurso de asignación de derechos es una cadena de texto simple.
seo-description: El siguiente bloque de código proporciona un ejemplo de un objeto JSON cuando el ID del recurso de asignación de derechos es una cadena de texto simple.
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Objeto JSON para el identificador de recurso de asignación de derechos {#json-object-for-entitlement-resource-id}

El siguiente bloque de código proporciona un ejemplo de un objeto JSON cuando el ID del recurso de asignación de derechos es una cadena de texto simple. En este caso, el ID de recurso es la cadena &quot;resource&quot;.

```
"metadata" : { 
"entitlement" : { 
"id" : "resource" 
} 
}
```

El siguiente bloque de código proporciona un ejemplo de un objeto JSON cuando el ID del recurso de asignación de derechos es una cadena mRSS con codificación HTML.

```
<rss version="2.0" xmlns:media="https://search.yahoo.com/mrss/"> 
<channel> 
<title>REF_ADOBE</title> 
<item> 
<title>Adobe Primetime Reference</title> 
<guid>1234</guid> 
<media:rating scheme="urn:v-chip">TV-PG</media:rating> 
</item> 
</channel> 
</rss>
```

La siguiente cadena mRSS se utiliza como ID de recurso.

```
"metadata" : { 
    "entitlement" : { 
        "id" : "<rss version=&quot;2.0&quot; 
        xmlns:media=&quot; 
        https://search.yahoo.com/mrss/&quot; 
        ><channel><title>REF_ADOBE</title><item> 
        <title>Adobe Primetime Reference</title><guid> 
        1234</guid><media:rating scheme=&quot;urn:v-chip&quot;> 
        TV-PG</media:rating></item></channel></rss>" 
        } 
} 
```
