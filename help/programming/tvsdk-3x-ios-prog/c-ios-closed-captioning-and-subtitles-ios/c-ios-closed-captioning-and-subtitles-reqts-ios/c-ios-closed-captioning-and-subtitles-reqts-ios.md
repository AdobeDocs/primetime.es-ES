---
description: Los subtítulos y subtítulos tienen algunas diferencias únicas y las habilita de diferentes maneras.
title: Requisitos para subtítulos y subtítulos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# Requisitos para subtítulos y subtítulos {#requirements-for-subtitles-and-closed-captions}

Los subtítulos y subtítulos tienen algunas diferencias únicas y las habilita de diferentes maneras.

Las secuencias de subtítulos se ejecutan en paralelo con el contenido principal. Los subtítulos forman parte de los paquetes de datos de los flujos de vídeo MPEG-2.

Debe tener en cuenta los siguientes requisitos para subtítulos y subtítulos cerrados:

* **Subtítulos**

   * Los subtítulos están normalmente en el mismo idioma que el audio y también representan sonidos de fondo como texto.
   * Los subtítulos son parte de los paquetes de datos de los flujos de vídeo MPEG-2 en el flujo de transmisión de vídeo.
   * Los subtítulos se admiten en la medida en que lo proporcione el marco de AV Foundation.

* **Subtítulos**

   * Los subtítulos suelen estar en un idioma distinto y no incluyen sonidos de fondo.
   * Los subtítulos se encuentran en flujos que se ejecutan en paralelo con el contenido principal.

      El `PTMediaPlayer` reproduce el contenido principal y los anuncios, donde el contenido principal puede ser en directo/lineal o VOD, y los anuncios pueden ser pre-roll, mid-roll o post-roll.
   Estos son algunos requisitos adicionales para subtítulos en iOS:

   * Para las marcas de tiempo, el valor `X-TIMESTAMP-MAP`, que se especifica en la sección del encabezado del archivo `WebVTT`, debe coincidir con la marca de tiempo del vídeo.

   * Para el sistema, debe utilizar iOS 6.1 o posterior.


>[!IMPORTANT]
>
>Los requisitos para subtítulos no se aplican a subtítulos cerrados.