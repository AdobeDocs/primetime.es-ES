---
title: Objeto JSON para el ID de recurso de derecho
description: El siguiente bloque de código proporciona un ejemplo de objeto JSON cuando el ID del recurso de asignación de derechos es una cadena de texto simple.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# Objeto JSON para el ID de recurso de asignación {#json-object-for-entitlement-resource-id}

El siguiente bloque de código proporciona un ejemplo de objeto JSON cuando el ID del recurso de asignación de derechos es una cadena de texto simple. En este caso, el ID de recurso es la cadena &quot;recurso&quot;.

```
"metadata" : { 
"entitlement" : { 
"id" : "resource" 
} 
}
```

El siguiente bloque de código proporciona un ejemplo de objeto JSON cuando el ID del recurso de derechos es una cadena mRSS con codificación HTML.

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
