---
description: Los subtítulos y subtítulos cerrados tienen algunas diferencias únicas y se activan de diferentes maneras.
seo-description: Los subtítulos y subtítulos cerrados tienen algunas diferencias únicas y se activan de diferentes maneras.
seo-title: Requisitos para subtítulos y subtítulos opcionales
title: Requisitos para subtítulos y subtítulos opcionales
uuid: 18ed6ac1-4b25-4590-8c61-3ffb0464d093
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# Requisitos para subtítulos y subtítulos opcionales {#requirements-for-subtitles-and-closed-captions}

Los subtítulos y subtítulos cerrados tienen algunas diferencias únicas y se activan de diferentes maneras.

Los flujos de subtítulos se ejecutan en paralelo con el contenido principal. Los subtítulos cerrados forman parte de los paquetes de datos de los flujos de vídeo MPEG-2.

Debe tener en cuenta los siguientes requisitos para subtítulos y subtítulos cerrados:

* **Subtítulos opcionales**

   * Los subtítulos cerrados suelen estar en el mismo idioma que el audio y también representan sonidos de fondo como texto.
   * Los subtítulos cerrados forman parte de los paquetes de datos de los flujos de vídeo MPEG-2 en el flujo de transmisión de vídeo.
   * Los subtítulos opcionales se admiten en la medida en que lo proporcione el marco de la Fundación AV.

* **Subtítulos**

   * Los subtítulos suelen estar en un idioma diferente y no incluyen sonidos de fondo.
   * Los subtítulos están en flujos que se ejecutan en paralelo con el contenido principal.

      El `PTMediaPlayer` reproduce el contenido principal y las publicidades, donde el contenido principal puede ser activo/lineal o VOD, y las publicidades pueden ser anteriores, intermedias o posteriores.
   Estos son algunos requisitos adicionales para los subtítulos en iOS:

   * Para las marcas de hora, el valor `X-TIMESTAMP-MAP`, que se especifica en la sección del encabezado del archivo `WebVTT`, debe coincidir con la marca de hora del vídeo.

   * Para el sistema, debe utilizar iOS 6.1 o posterior.


>[!IMPORTANT]
>
>Los requisitos para los subtítulos no se aplican a los subtítulos cerrados.