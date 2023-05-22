---
description: Utilice el comando GET HTTP para interactuar con el servidor de manifiesto.
title: Enviar un comando al servidor de manifiestos
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Enviar un comando al servidor de manifiestos {#send-a-command-to-the-manifest-server}

Utilice el comando GET HTTP para interactuar con el servidor de manifiesto.

1. Enviar un `HTTP GET` solicitud de una URL de bootstrap construida con el siguiente patrón:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.m3u8
    ?{query parameters}
   ```

* **PublisherAssetID** Requerido. ID único del publicador para el contenido específico.

* **URL de contenido** Requerido. URL del archivo de contenido M3U8, codificado en Base64 para que sea seguro dentro de la URL del servidor de manifiesto. La dirección URL de contenido debe señalar a un archivo de variante M3U8, aunque solo haya una secuencia de velocidad de bits.

* **Parámetros de consulta** Algunos son obligatorios y otros opcionales. Estos constituyen la parte más variada de la solicitud. Indican al servidor de manifiesto qué tipo de cliente realiza la solicitud y qué desea que haga el servidor de manifiesto.

   Por ejemplo:

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.m3u8?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **Solicitudes HTTP o HTTPS**

   El servidor de manifiestos crea direcciones URL utilizando el mismo protocolo HTTP de la solicitud del cliente. Si un reproductor realiza una solicitud HTTP (http) no segura, el servidor de manifiestos devuelve direcciones URL de manifiesto y direcciones URL de seguimiento de audiencia con el protocolo http. Si un reproductor realiza una conexión HTTP segura (https), un servidor de manifiesto, devuelve direcciones URL de manifiesto y direcciones URL de seguimiento de audiencia con el protocolo https.

   >[!NOTE]
   >
   >El servidor de manifiestos no puede cambiar el protocolo (HTTP o HTTPS) de los segmentos de contenido (.ts) ni las señalizaciones de seguimiento de terceros. Debe ponerse en contacto con los proveedores de contenido y de publicidad de terceros para que configuren los protocolos deseados.