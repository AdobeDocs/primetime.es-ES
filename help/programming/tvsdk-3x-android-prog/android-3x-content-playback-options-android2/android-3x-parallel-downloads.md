---
description: La descarga de vídeo y audio en paralelo, en lugar de en serie, reduce los retrasos de inicio.
title: Descargas paralelas
exl-id: 7cc9afbf-e495-40b0-a8ff-86d4939d1b15
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Descargas paralelas {#parallel-downloads}

La descarga de vídeo y audio en paralelo, en lugar de en serie, reduce los retrasos de inicio.

Las descargas paralelas permiten la reproducción de archivos de vídeo bajo demanda (VOD), optimizan el uso del ancho de banda disponible desde un servidor, reducen la probabilidad de entrar en situaciones de almacenamiento en búfer bajo ejecución y minimizan el retraso entre la descarga y la reproducción.

<!-- 

Removed as part of "no DASH use cases" for 2.5.1, May 31st, 2017 release.
<p>Parallel downloads allows DASH video-on-demand (VOD) files to be played, optimizes the available bandwidth usage from a server, lowers the probability of getting into buffer under-run situations, and minimizes the delay between download and playback. </p>

 -->

Sin descargas paralelas, TVSDK emite una solicitud para el segmento de vídeo y, después de cargar el segmento de vídeo, solicita uno o dos segmentos de audio. Con las descargas paralelas, los segmentos de audio y vídeo se descargan simultáneamente, no de forma secuencial. Además, como hay dos conexiones y dos solicitudes HTTP por segmento en paralelo, los datos llegan a la pantalla más rápido.

>[!NOTE]
>
>Esta función se aplica solo al contenido donde el audio y el vídeo están codificados en diferentes archivos (contenido no mezclado) y no se aplica al contenido MP4, que siempre está mezclado. El contenido HLS suele estar sin mezclar, especialmente con audio alternativo.

<!-- 

See comment above (DASH use case removed).

  This feature applies only to content where the audio and video are encoded into different files (unmuxed content) and does not apply to MP4 content, which is always muxed. Most DASH content is unmuxed, and HLS content is often unmuxed, especially with alternate audio. 
-->

La conexión HTTP puede experimentar retrasos en las siguientes fases:

* Al establecer la conexión TCP/IP con el servidor

   Aunque el cliente y el servidor han acordado comunicarse, aún no se ha producido ninguna comunicación HTTP. Este tipo de retraso depende de la infraestructura entre el cliente y el servidor. Este proceso requiere encontrar una ruta a través de Internet entre el cliente y el servidor y asegurarse de que todos los dispositivos, como enrutadores y servidores de seguridad, de la ruta acepten la transferencia de datos.
* Al enviar una solicitud HTTP para un segmento o un manifiesto a través de la conexión TCP/IP.

   El servidor recibe la solicitud, la procesa y comienza a enviar los datos de nuevo al cliente. El grado de retraso depende de la carga y la complejidad del software en el servidor y, en cierta medida, de la velocidad de conexión de carga cuando el cliente envía la solicitud.
