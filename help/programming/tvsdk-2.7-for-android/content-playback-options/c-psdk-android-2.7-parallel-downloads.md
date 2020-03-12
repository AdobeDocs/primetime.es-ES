---
description: La descarga de vídeo y audio en paralelo, en lugar de en una serie, reduce los retrasos de inicio.
seo-description: La descarga de vídeo y audio en paralelo, en lugar de en una serie, reduce los retrasos de inicio.
seo-title: Descargas paralelas
title: Descargas paralelas
uuid: fa3edb50-7c24-433c-bc50-72d6cf73d834
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Descargas paralelas {#parallel-downloads}

La descarga de vídeo y audio en paralelo, en lugar de en una serie, reduce los retrasos de inicio.

Las descargas paralelas permiten reproducir archivos de vídeo a petición (VOD), optimiza el uso del ancho de banda disponible en un servidor, reduce la probabilidad de acceder a situaciones de búfer en ejecución y minimiza el retraso entre la descarga y la reproducción.

<!-- 

Removed as part of "no DASH use cases" for 2.5.1, May 31st, 2017 release.
<p>Parallel downloads allows DASH video-on-demand (VOD) files to be played, optimizes the available bandwidth usage from a server, lowers the probability of getting into buffer under-run situations, and minimizes the delay between download and playback. </p>

 -->

Sin descargas paralelas, TVSDK emite una solicitud para el segmento de vídeo y, una vez cargado, solicita uno o dos segmentos de audio. Con las descargas paralelas, los segmentos de audio y vídeo se descargan simultáneamente, no secuencialmente. Además, como hay dos conexiones y dos solicitudes HTTP por segmento en paralelo, los datos llegan a la pantalla más rápido.

>[!NOTE]
>
>Esta función solo se aplica al contenido en el que el audio y el vídeo están codificados en diferentes archivos (contenido sin muestrear) y no se aplica al contenido MP4, que siempre se multiplica. El contenido de HLS a menudo no se multiplica, especialmente con audio alternativo.

<!-- 

See comment above (DASH use case removed).
<note type="restriction">
  This feature applies only to content where the audio and video are encoded into different files (unmuxed content) and does not apply to MP4 content, which is always muxed. Most DASH content is unmuxed, and HLS content is often unmuxed, especially with alternate audio. 
</note>

 -->

La conexión HTTP puede experimentar retrasos en las siguientes etapas:

* Al establecer la conexión TCP/IP con el servidor

   Aunque el cliente y el servidor han aceptado comunicarse, aún no se ha producido ninguna comunicación HTTP. Este tipo de retraso depende de la infraestructura entre el cliente y el servidor. Este proceso requiere encontrar una ruta a través de Internet entre el cliente y el servidor y asegurarse de que todos los dispositivos, como enrutadores y servidores de seguridad, de la ruta acepten la transferencia de datos.
* Al enviar una solicitud HTTP para un segmento o un manifiesto a través de la conexión TCP/IP.

   El servidor recibe la solicitud, la procesa y comienza a enviar los datos al cliente. El grado de retraso depende de la carga y la complejidad del software en el servidor y, en cierta medida, de la velocidad de la conexión de carga cuando el cliente envía la solicitud.

