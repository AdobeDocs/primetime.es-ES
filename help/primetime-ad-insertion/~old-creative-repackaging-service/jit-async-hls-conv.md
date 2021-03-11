---
description: CRS proporciona reempaquetado justo a tiempo (JIT) y asincrónico y conversión de HLS a HLS. El resultado del reempaquetado es una versión con formato HLS del creativo de publicidad original. CRS coloca la versión con formato HLS en el servidor de red de entrega de contenido (CDN) para su uso cuando sea necesario.
title: Principales usos del CRS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Principales usos del CRS {#main-uses-of-crs}

CRS proporciona reempaquetado justo a tiempo (JIT) y asincrónico y conversión de HLS a HLS. El resultado del reempaquetado es una versión con formato HLS del creativo de publicidad original. CRS coloca la versión con formato HLS en el servidor de red de entrega de contenido (CDN) para su uso cuando sea necesario.

En JIT, el reempaquetado de Adobe Primetime y la inserción comienza el proceso de reempaquetado cuando encuentra por primera vez un creativo de publicidad que no es de HLS. Esto suele implicar la pérdida de oportunidades para ejecutar la publicidad durante el proceso de reempaquetado.

En el reempaquetado asincrónico, el creativo de publicidad se transcodifica y almacena antes de que sea necesario, lo que puede eliminar las oportunidades perdidas.

En la conversión HLS-to-HLS, CRS redistribuye un creativo de anuncios HLS a trozos de tamaño adecuado para garantizar una reproducción coherente.

## Reempaquetado Just-In-Time {#section_1BA344F2300B49F291865A7461EDFEAE}

La secuencia para el reempaquetado de JIT es la siguiente:

1. El servidor de manifiestos obtiene un anuncio.
1. Si el formato de anuncio es HLS, el servidor de manifiestos inserta el anuncio en el flujo de contenido.
1. Si el formato no es HLS (por ejemplo, MP4, FLV o WebM), el servidor de manifiestos busca una versión transcodificada en el servidor CDN. Si encuentra uno, inserta el anuncio transcodificado en el flujo de contenido.
1. Si el formato no es HLS y el servidor de CDN no tiene una versión transcodificada, el servidor de manifiestos pasa la publicidad a CRS, que transcodifica el creativo de la publicidad y almacena el resultado en el servidor de CDN para su uso posterior.
1. El servidor de manifiesto devuelve el contenido sin el anuncio.

## Reempaquetado asincrónico {#section_ACDFB43FDA4B445CB9F2A107FEB4F2F7}

Puede utilizar la API descrita en [Repackaging API](../~old-creative-repackaging-service/api-repackage.md) para pretranscodificar un elemento creativo que no sea HLS para minimizar la pérdida de impresiones y maximizar la monetización.

## Conversión de HLS a HLS {#section_877A0E7E8FAF4C2DB086A31C24D53435}

Para evitar el almacenamiento en búfer y el retraso, un cliente descarga un vídeo en pequeños fragmentos. Si los tamaños de fragmento son incoherentes, la reproducción puede ser irregular. La conversión de HLS a HLS garantiza que los fragmentos de datos tengan la misma duración (por ejemplo, 6 segundos).

>[!NOTE]
>
>CRS produce la versión 3 de HLS, independientemente de la versión de HLS que reciba.