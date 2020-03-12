---
description: CRS proporciona reempaquetado justo a tiempo (JIT) y asincrónico y conversión de HLS a HLS. El resultado del reempaquetado es una versión con formato HLS del elemento creativo de publicidad original. CRS coloca la versión con formato HLS en el servidor de red de entrega de contenido (CDN) para su uso cuando sea necesario.
seo-description: CRS proporciona reempaquetado justo a tiempo (JIT) y asincrónico y conversión de HLS a HLS. El resultado del reempaquetado es una versión con formato HLS del elemento creativo de publicidad original. CRS coloca la versión con formato HLS en el servidor de red de entrega de contenido (CDN) para su uso cuando sea necesario.
seo-title: Principales usos del SIR
title: Principales usos del SIR
uuid: df2caa67-bc94-4146-9b93-14edc060c3d5
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# Principales usos del SIR {#main-uses-of-crs}

CRS proporciona reempaquetado justo a tiempo (JIT) y asincrónico y conversión de HLS a HLS. El resultado del reempaquetado es una versión con formato HLS del elemento creativo de publicidad original. CRS coloca la versión con formato HLS en el servidor de red de entrega de contenido (CDN) para su uso cuando sea necesario.

En JIT, el reempaquetado de Adobe Primetime y la inserción comienza el proceso de reempaquetado cuando se encuentra por primera vez con un elemento creativo que no es de HLS. Esto suele implicar la pérdida de oportunidades para ejecutar la publicidad durante el proceso de reempaquetado.

En el reempaquetado asincrónico, el elemento creativo de la publicidad se transcodifica y almacena antes de que sea necesario, lo que puede eliminar las oportunidades perdidas.

En la conversión de HLS a HLS, CRS reformatea un elemento creativo de anuncios HLS en fragmentos de tamaño adecuado para garantizar una reproducción coherente.

## Reempaquetado justo a tiempo {#section_1BA344F2300B49F291865A7461EDFEAE}

La secuencia para el reempaquetado JIT es la siguiente:

1. El servidor de manifiesto obtiene una publicidad.
1. Si el formato de la publicidad es HLS, el servidor de manifiesto inserta la publicidad en el flujo de contenido.
1. Si el formato no es HLS (por ejemplo, MP4, FLV o WebM), el servidor de manifiesto busca una versión transcodificada en el servidor CDN. Si encuentra uno, inserta el anuncio transcodificado en el flujo de contenido.
1. Si el formato no es HLS y el servidor CDN no tiene una versión transcodificada, el servidor de manifiesto pasa la publicidad a CRS, que transcodifica el elemento creativo de la publicidad y almacena el resultado en el servidor CDN para su uso posterior.
1. El servidor de manifiesto devuelve el contenido sin la publicidad.

## Reempaquetado asincrónico {#section_ACDFB43FDA4B445CB9F2A107FEB4F2F7}

Puede utilizar la API descrita en la API de [reempaquetado](../creative-repackaging-service/api-repackage.md) para pretranscodificar un elemento creativo que no sea HLS a fin de minimizar la pérdida de impresiones y maximizar la monetización.

## Conversión de HLS a HLS {#section_877A0E7E8FAF4C2DB086A31C24D53435}

Para evitar el almacenamiento en búfer y el retraso, un cliente descarga un vídeo en pequeños fragmentos. Si los tamaños de fragmento son incoherentes, la reproducción puede ser irregular. La conversión de HLS a HLS garantiza que los fragmentos de datos tengan la misma duración (por ejemplo, 6 segundos).

>[!NOTE]
>
>CRS produce HLS versión 3, independientemente de la versión de HLS que reciba.