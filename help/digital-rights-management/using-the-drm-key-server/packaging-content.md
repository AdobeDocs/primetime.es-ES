---
title: Contenido del paquete
description: Contenido del paquete
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# Contenido del paquete{#packaging-content}

Al empaquetar contenido para la entrega de claves remotas, utilice una directiva que especifique que la entrega de claves remotas es obligatoria. La URL del servidor de claves debe incluirse en el M3U8 (archivo de manifiesto) para el contenido HLS. La URL del servidor de claves DRM de Primetime tiene el formato:

```
https://key-server-host:port/faxsks/tenant-name/key
```

Por ejemplo, para la escucha del nombre de host [!DNL mykeyserver.com] del servidor clave en el puerto 443 y un inquilino llamado `tenant1`, la URL del servidor clave que se debe especificar en el M3U8 es:

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

Se puede usar la misma dirección URL para clientes iOS y Xbox 360. O bien, si el servidor está configurado con inquilinos separados para cada tipo de cliente, se pueden utilizar direcciones URL diferentes.

El mismo contenido se puede reproducir en clientes que no requieran un servidor de claves, siempre que la URL del servidor de licencias apunte a un servidor de licencias en ejecución correctamente configurado.
