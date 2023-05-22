---
description: CRS proporciona reempaquetado justo a tiempo (JIT) y asincrónico, y conversión de HLS a HLS. El resultado del reempaquetado es una versión con formato HLS del creativo de publicidad original. CRS coloca la versión con formato HLS en el servidor de la red de distribución de contenido (CDN) para usarla cuando sea necesario.
title: Principales usos de CRS
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Principales usos de CRS {#main-uses-of-crs}

CRS proporciona reempaquetado justo a tiempo (JIT) y asincrónico, y conversión de HLS a HLS. El resultado del reempaquetado es una versión con formato HLS del creativo de publicidad original. CRS coloca la versión con formato HLS en el servidor de la red de distribución de contenido (CDN) para usarla cuando sea necesario.

En JIT, al volver a empaquetar Adobe Primetime, la inserción de publicidad comienza el proceso de reempaquetado cuando encuentra por primera vez un creativo de publicidad que no es HLS. Esto generalmente implica la pérdida de oportunidades para ejecutar el anuncio durante el proceso de reempaquetado.

En el reempaquetado asincrónico, el creativo de la publicidad se transcodifica y almacena antes de que sea necesario, lo que puede eliminar esas oportunidades perdidas.

En la conversión de HLS a HLS, CRS vuelve a dar formato a un anuncio HLS creativo en fragmentos de tamaño adecuado para garantizar una reproducción coherente.

## Reempaquetado Just-In-Time {#section_1BA344F2300B49F291865A7461EDFEAE}

La secuencia para el reempaquetado JIT es la siguiente:

1. El servidor de manifiesto busca un anuncio.
1. Si el formato de anuncio es HLS, el servidor de manifiesto inserta el anuncio en el flujo de contenido.
1. Si el formato no es HLS (por ejemplo, MP4, FLV o WebM), el servidor de manifiesto busca una versión transcodificada en el servidor CDN. Si encuentra uno, inserta el anuncio transcodificado en el flujo de contenido.
1. Si el formato no es HLS y el servidor CDN no tiene versión transcodificada, el servidor de manifiesto pasa el anuncio a CRS, que transcodifica el creativo de publicidad y almacena el resultado en el servidor CDN para su uso posterior.
1. El servidor de manifiestos devuelve el contenido sin el anuncio.

## Reempaquetado asincrónico {#section_ACDFB43FDA4B445CB9F2A107FEB4F2F7}

Puede utilizar la API que se describe en [API de reempaquetado](../~old-creative-repackaging-service/api-repackage.md) para pretranscodificar un creativo que no sea de HLS para minimizar la pérdida de impresiones y maximizar la monetización.

## Conversión de HLS a HLS {#section_877A0E7E8FAF4C2DB086A31C24D53435}

Para evitar el almacenamiento en búfer y el retraso, un cliente descarga un vídeo en pequeños fragmentos. Si el tamaño de los fragmentos es inconsistente, la reproducción puede ser irregular. La conversión de HLS a HLS garantiza que todos los fragmentos de datos tengan la misma duración (por ejemplo, 6 segundos).

>[!NOTE]
>
>CRS produce la versión 3 de HLS, independientemente de la versión de HLS que reciba.