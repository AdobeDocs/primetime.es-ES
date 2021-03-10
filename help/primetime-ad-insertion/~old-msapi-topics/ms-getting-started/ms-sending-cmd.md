---
description: Utilice el comando HTTP GET para interactuar con el servidor de manifiestos.
title: Enviar un comando al servidor de manifiesto
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Enviar un comando al servidor de manifiesto {#send-a-command-to-the-manifest-server}

Utilice el comando HTTP GET para interactuar con el servidor de manifiestos.

1. Envíe una solicitud `HTTP GET` para una URL de arranque construida con el siguiente patrón:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.m3u8
    ?{query parameters}
   ```

* **** PublisherAssetIDRrequerido. ID exclusivo del editor para el contenido específico.

* **URL de** contenidoRequerido. URL del archivo M3U8 de contenido, base64 codificada para ser segura dentro de la URL del servidor de manifiestos. La dirección URL de contenido debe apuntar a un archivo M3U8 de variante, aunque solo haya un flujo de velocidad de bits.

* **Parámetros de** consultaAlgunos son obligatorios, otros opcionales. Estos constituyen la parte más variada de la solicitud. Indican al servidor de manifiesto qué tipo de cliente está realizando la solicitud y qué desea que haga el servidor de manifiesto.

   Por ejemplo:

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.m3u8?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **Solicitudes HTTP vs. HTTPS**

   El servidor de manifiesto crea direcciones URL utilizando el mismo protocolo HTTP de la solicitud del cliente. Si un reproductor realiza una solicitud HTTP (http) no segura, el servidor de manifiesto devuelve URL de manifiesto y URL de seguimiento de Auditude con el protocolo http. Si un reproductor realiza una conexión HTTP segura (https), un servidor de manifiesto, devuelve direcciones URL de manifiesto y direcciones URL de seguimiento de Auditude con el protocolo https.

   >[!NOTE]
   >
   >El servidor de manifiestos no puede cambiar el protocolo (HTTP o HTTPS) de los segmentos de contenido (.ts) y las señalizaciones de seguimiento de terceros. Debe ponerse en contacto con el contenido y los proveedores de publicidad de terceros para que configuren los protocolos deseados.