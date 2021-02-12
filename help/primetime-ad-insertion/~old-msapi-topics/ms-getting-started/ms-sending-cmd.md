---
description: Utilice el comando GET HTTP para interactuar con el servidor de manifiesto.
seo-description: Utilice el comando GET HTTP para interactuar con el servidor de manifiesto.
seo-title: Envío de un comando al servidor de manifiesto
title: Envío de un comando al servidor de manifiesto
uuid: e9680563-d268-406d-87ce-1521a677e9ec
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Enviar un comando al servidor de manifiesto {#send-a-command-to-the-manifest-server}

Utilice el comando GET HTTP para interactuar con el servidor de manifiesto.

1. Envíe una solicitud `HTTP GET` para una URL de arranque construida con el siguiente patrón:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.m3u8
    ?{query parameters}
   ```

* **** PublisherAssetIDRrequerido. ID única del editor para el contenido específico.

* **Content** URLRequired. URL del archivo M3U8 de contenido, codificado en Base64 para ser seguro dentro de la URL del servidor de manifiesto. La dirección URL de contenido debe apuntar a un archivo M3U8 de variante, aunque solo haya un flujo de velocidad de bits.

* **Parámetros** de consultaAlgunos son obligatorios, otros opcionales. Éstas constituyen la parte más variada de la solicitud. Indican al servidor de manifiesto qué tipo de cliente realiza la solicitud y qué desea que haga el servidor de manifiesto.

   Por ejemplo:

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.m3u8?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **Peticiones HTTP vs. HTTPS**

   El servidor de manifiesto crea direcciones URL utilizando el mismo protocolo HTTP de la solicitud del cliente. Si un reproductor realiza una solicitud HTTP (http) no segura, el servidor de manifiesto devuelve direcciones URL de manifiesto y URL de seguimiento de Auditude con el protocolo http. Si un reproductor realiza una conexión HTTP (https) segura, servidor de manifiesto, devuelve direcciones URL de manifiesto y direcciones URL de seguimiento de Auditude con el protocolo https.

   >[!NOTE]
   >
   >El servidor de manifiesto no puede cambiar el protocolo (HTTP o HTTPS) de los segmentos de contenido (.ts) y las señalizaciones de seguimiento de terceros. Debe ponerse en contacto con el contenido y los proveedores de publicidad de terceros para que éstos configuren los protocolos deseados.