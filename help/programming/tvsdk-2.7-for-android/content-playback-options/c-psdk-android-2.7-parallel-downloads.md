---
description: La descarga de vídeo y audio en paralelo, en lugar de en serie, reduce los retrasos en el inicio.
title: Descargas paralelas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Descargas paralelas {#parallel-downloads}

La descarga de vídeo y audio en paralelo, en lugar de en serie, reduce los retrasos en el inicio.

Las descargas paralelas permiten reproducir archivos de vídeo bajo demanda (VOD), optimiza el uso del ancho de banda disponible desde un servidor, reduce la probabilidad de entrar en situaciones de búfer en ejecución y minimiza el retraso entre descarga y reproducción.

<!-- 

Removed as part of "no DASH use cases" for 2.5.1, May 31st, 2017 release.
<p>Parallel downloads allows DASH video-on-demand (VOD) files to be played, optimizes the available bandwidth usage from a server, lowers the probability of getting into buffer under-run situations, and minimizes the delay between download and playback. </p>

 -->

Sin descargas paralelas, TVSDK emite una solicitud para el segmento de vídeo y, una vez cargado el segmento de vídeo, solicita uno o dos segmentos de audio. Con las descargas paralelas, los segmentos de audio y vídeo se descargan simultáneamente, no secuencialmente. Además, como hay dos conexiones y dos solicitudes HTTP por segmento en paralelo, los datos llegan a la pantalla más rápido.

>[!NOTE]
>
>Esta función se aplica solo al contenido en el que el audio y el vídeo están codificados en diferentes archivos (contenido no muestreado) y no se aplica al contenido MP4, que siempre está mezclado. El contenido de HLS a menudo no se modifica, especialmente con audio alternativo.

<!-- 

See comment above (DASH use case removed).
  This feature applies only to content where the audio and video are encoded into different files (unmuxed content) and does not apply to MP4 content, which is always muxed. Most DASH content is unmuxed, and HLS content is often unmuxed, especially with alternate audio. 
-->

La conexión HTTP puede experimentar retrasos en las siguientes etapas:

* Al establecer la conexión TCP/IP con el servidor

   Aunque el cliente y el servidor han aceptado comunicarse, aún no se ha producido comunicación HTTP. Este tipo de retraso depende de la infraestructura entre el cliente y el servidor. Este proceso requiere encontrar una ruta a través de Internet entre el cliente y el servidor y asegurarse de que todos los dispositivos, como enrutadores y firewalls, en la ruta acepten la transferencia de datos.
* Al enviar una solicitud HTTP para un segmento o un manifiesto a través de la conexión TCP/IP.

   El servidor recibe la solicitud, la procesa y comienza a enviar los datos al cliente. El grado de retraso depende de la carga y la complejidad del software en el servidor y en cierta medida de la velocidad de conexión de carga cuando el cliente envía la solicitud.

