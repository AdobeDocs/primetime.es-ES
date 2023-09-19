---
description: Los subtítulos y subtítulos tienen algunas diferencias únicas y se habilitan de diferentes maneras.
title: Requisitos para subtítulos y subtítulos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Requisitos para subtítulos y subtítulos {#requirements-for-subtitles-and-closed-captions}

Los subtítulos y subtítulos tienen algunas diferencias únicas y se habilitan de diferentes maneras.

Las secuencias de subtítulos se ejecutan en paralelo con el contenido principal. Los subtítulos opcionales forman parte de los paquetes de datos de las transmisiones de vídeo MPEG-2.

Debe tener en cuenta los siguientes requisitos para los subtítulos y subtítulos cerrados:

* **Subtítulos opcionales**

   * Los subtítulos opcionales suelen estar en el mismo idioma que el audio y también representan sonidos de fondo como texto.
   * Los subtítulos opcionales forman parte de los paquetes de datos de los flujos de vídeo MPEG-2 en el flujo de transmisión de vídeo.
   * Los subtítulos opcionales son compatibles en la medida en que lo permita el marco de trabajo de AV Foundation.

* **Subtítulos**

   * Los subtítulos suelen estar en un idioma diferente y no incluyen sonidos de fondo.
   * Los subtítulos se encuentran en secuencias que se ejecutan en paralelo con el contenido principal.

     El `PTMediaPlayer` reproduce el contenido principal y los anuncios, donde el contenido principal puede ser en directo/lineal o VOD, y los anuncios pueden ser previos a la emisión, durante la emisión o después de la emisión.

  Estos son algunos requisitos adicionales para los subtítulos en iOS:

   * Para las marcas de tiempo, la variable `X-TIMESTAMP-MAP` , que se especifica en la sección de encabezado del `WebVTT` , debe coincidir con la marca de tiempo del vídeo.

   * Para el sistema, debe utilizar iOS 6.1 o posterior.

>[!IMPORTANT]
>
>Los requisitos para los subtítulos no se aplican a los subtítulos cerrados.
