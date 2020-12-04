---
seo-title: Empaquetado de contenido
title: Empaquetado de contenido
uuid: 366c8470-b7ef-4a39-83c2-151ba9be9a32
translation-type: tm+mt
source-git-commit: 1547eb3dd220fafc08df923f40504736c16a866c
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# Empaquetado de contenido{#packaging-content}

Al empaquetar contenido para el envío de claves remotas, utilice una directiva que especifique que se requiere el envío de claves remotas. La URL del servidor de claves debe incluirse en el M3U8 (archivo de manifiesto) para el contenido HLS. La URL del servidor de claves de DRM de Primetime tiene el formato:

```
https://key-server-host:port/faxsks/tenant-name/key
```

Por ejemplo, para la escucha del nombre de host [!DNL mykeyserver.com] del servidor clave en el puerto 443 y un inquilino denominado `tenant1`, la dirección URL del servidor clave que se debe especificar en M3U8 es:

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

La misma dirección URL puede usarse para clientes iOS y Xbox 360. O bien, si el servidor está configurado con inquilinos independientes para cada tipo de cliente, se pueden utilizar direcciones URL diferentes.

El mismo contenido se puede reproducir en clientes que no requieran un servidor de claves, siempre que la URL del servidor de licencias apunte a un servidor de licencias que se esté ejecutando correctamente.
