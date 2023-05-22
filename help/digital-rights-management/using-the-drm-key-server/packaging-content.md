---
title: Empaquetando contenido
description: Empaquetando contenido
copied-description: true
exl-id: d408889c-f96d-43d3-af50-62cb5ecc2e28
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Empaquetando contenido{#packaging-content}

Al empaquetar contenido para la entrega de claves remotas, utilice una directiva que especifique que se requiere la entrega de claves remotas. La URL del servidor de claves debe incluirse en el M3U8 (archivo de manifiesto) para el contenido HLS. La URL del servidor de claves DRM de Primetime tiene el formato:

```
https://key-server-host:port/faxsks/tenant-name/key
```

Por ejemplo, para el nombre de host del servidor de claves [!DNL mykeyserver.com] escuchando en el puerto 443 y un inquilino llamado `tenant1`, la URL del servidor clave que se debe especificar en el M3U8 es:

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

La misma dirección URL se puede utilizar para clientes iOS y Xbox 360. O bien, si el servidor está configurado con inquilinos independientes para cada tipo de cliente, se pueden utilizar distintas direcciones URL.

El mismo contenido puede reproducirse en clientes que no requieran un servidor de claves, siempre que la URL del servidor de licencias apunte a un servidor de licencias en ejecución correctamente configurado.
