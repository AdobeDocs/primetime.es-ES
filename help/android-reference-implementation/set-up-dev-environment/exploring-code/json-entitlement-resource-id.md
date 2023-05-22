---
title: Objeto JSON para ID de recurso de derecho
description: El siguiente bloque de código proporciona un ejemplo de un objeto JSON cuando el ID del recurso de derecho es una cadena de texto simple.
exl-id: 396c43e7-404a-40f5-8113-a720e2c834e7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# Objeto JSON para ID de recurso de derecho {#json-object-for-entitlement-resource-id}

El siguiente bloque de código proporciona un ejemplo de un objeto JSON cuando el ID del recurso de derecho es una cadena de texto simple. En este caso, el ID del recurso es la cadena &quot;resource&quot;.

```
"metadata" : { 
"entitlement" : { 
"id" : "resource" 
} 
}
```

El siguiente bloque de código proporciona un ejemplo de un objeto JSON cuando el ID del recurso de derecho es una cadena mRSS con codificación de HTML.

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
