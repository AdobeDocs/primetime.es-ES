---
cloud: experience-cloud
product: adobe primetime
audience: end-user
user-guide-title: Ayuda de Ad Insertion dinámico de Primetime
user-guide-description: Explains how to monetize content by inserting user-targeted dynamic ads on the server and engage audience with personalized ads.
translation-type: tm+mt
source-git-commit: 23a48208ac1d3625ae7d925ab6bfba8f2a980766
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Ayuda de Ad Insertion dinámico {#ad-insertion}

+ [Información general de Ad Insertion dinámico](home.md)
+ [Notas de la versión de Ad Insertion dinámico](https://docs.adobe.com/content/help/en/primetime/release-notes/ptai/ptai-19x-release-notes.html)
+ [Herramienta de depuración del servidor de manifiesto](manifest-server-debugging-tool.md)

<!-- + [Server Side Ad Insertion debugging dashboard](ssai-debugging-dashboard.md)-->
+ API de servidor de manifiesto para Ad Insertion {#manifest-server}
   + [Información general sobre las interacciones del servidor de manifiesto](msapi-topics/ms-overview.md)
   + Introducción a Manifest Server {#get-started}
      + [Envío de un comando al servidor de manifiesto](msapi-topics/ms-getting-started/ms-sending-cmd.md)
      + [Parámetros de consulta del servidor de manifiesto](msapi-topics/ms-getting-started/ms-api-query-params.md)
   + Solicitudes de inserción de publicidad {#ad-insert}
      + [Solicitudes de inserción de anuncios](msapi-topics/ms-insert-ads/ms-ad-insert.md)
      + [Parámetros de consulta opcionales por cliente y situación](msapi-topics/ms-insert-ads/ms-api-query-param-situation.md)
      + [Facilitación del cambio del reproductor HLS a flujos de failover/backup](msapi-topics/ms-insert-ads/hls-switching-to-failover.md)
      + [Varios flujos de velocidad de bits](msapi-topics/ms-insert-ads/ms-api-mbr-streams.md)
      + [Inserción parcial de pausa publicitaria](msapi-topics/ms-insert-ads/partial-ad-break-insetion.md)
      + [Compatibilidad de varios CDN con CRS y envío](msapi-topics/ms-insert-ads/ms-api-multi-cdns-for-crs.md)
   + Reemplazar líneas de tiempo de VOD {#replace-vod}
      + [Cambios en VOD](msapi-topics/ms-changes-vod-timeline/ms-replace-vod-timeline.md)
      + [Formato de línea de tiempo VOD](msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md)
      + [Reemplazar una línea de tiempo de VOD](msapi-topics/ms-changes-vod-timeline/t-ms-replace-vod-timeline.md)
   + Seguimiento de la eficacia de la publicidad {#ad}
      + [Seguimiento de publicidades](msapi-topics/ms-at-effectiveness/ms-at-overview.md)
      + [Habilitar el seguimiento de publicidades de cliente](msapi-topics/ms-at-effectiveness/ms-enable-client-side-ad-tracking.md)
      + [Información general sobre el seguimiento del cliente que no es TVSDK](msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md)
      + [API para que los reproductores interactúen con el servidor de manifiesto](msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md)
      + [Directiva EXT-X-MARKER](msapi-topics/ms-at-effectiveness/ms-api-playlists.md)
   + [Cookies](msapi-topics/ms-cookies.md)
   + [Compatibilidad con subtítulos WebVTT](msapi-topics/ms-webvtt-captions.md)
   + Lista de los formatos de archivo {#list}
      + [Formatos de archivo](msapi-topics/ms-list-file-formats/ms-api-file-formats.md)
      + [Formato JSON para URL para solicitar lista de reproducción de manifiesto de variante](msapi-topics/ms-list-file-formats/ms-json-m3u8.md)
      + [Formatos JSON para rastrear direcciones URL](msapi-topics/ms-list-file-formats/notvsdk-csat-sidecar.md)
      + [Formato VMAP para rastrear direcciones URL](msapi-topics/ms-list-file-formats/notvsdk-csat-vmap.md)
   + [Requisitos del reproductor de vídeo](msapi-topics/ms-player-req.md)
+ Servicio de reempaquetado creativo Primetime {#crs}
   + [Descripción general de CRS](creative-repackaging-service/crs-overview.md)
   + [Principales usos del SIR](creative-repackaging-service/jit-async-hls-conv.md)
   + [Compatibilidad con varios CDN](creative-repackaging-service/multi-cdn-supportt.md)
   + [Flujos de trabajo detallados para el reempaquetado JIT](creative-repackaging-service/jit-repackage.md)
   + [Uso de CRS para insertar etiquetas de metadatos temporizados ID3](creative-repackaging-service/inject-id3.md)
   + [API de reempaquetado](creative-repackaging-service/api-repackage.md)
