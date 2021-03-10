---
description: Existen varias formas de determinar la inserción y la ubicación de los anuncios.
title: Inserción y ubicación de publicidad
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---


# Inserción y colocación de anuncios{#ad-insertion-and-placement}

Existen varias formas de determinar la inserción y la ubicación de los anuncios.

## Inserción de publicidad {#section_1F7581B987704E318E064082190E8243}

A continuación se muestra una descripción general del proceso utilizado para determinar la inserción de publicidad:

1. **Detección** de oportunidades: El SDK de TVSDK utiliza la información de flujo para detectar ubicaciones posibles y deseadas para los anuncios.
1. **Resolución** del anuncio: El TVSDK se comunica con un servidor de publicidad para recuperar los anuncios que se van a insertar en el contenido.
1. **Colocación** de publicidad: El SDK de TVSDK carga los anuncios especificados y los coloca en saltos de anuncio en la cronología de contenido en las ubicaciones especificadas y vuelve a calcular la cronología virtual, si es necesario.

## Colocación de publicidad {#section_B9D63F7409A2447F9FF209289BE5D3D5}

El SDK de TVSDK puede obtener ubicaciones para la posible ubicación de la publicidad desde las siguientes fuentes:

* **Metadatos/cues de manifiesto**

   TVSDK detecta las señales, extrae la información necesaria de estas indicaciones y se comunica con un servidor de publicidad para obtener las publicidades correspondientes. Esta fuente es común para flujos en directo/lineales.

   El SDK de TVSDK suele reemplazar el contenido principal por los anuncios en la ubicación indicada por los metadatos o las señales; de lo contrario, el cliente dejaría cada vez más atrás el punto activo real.

* **El mapa del servidor de publicidad**

   Normalmente, los metadatos sobre estos flujos se registran en el servidor de publicidad antes de la reproducción. El TVSDK recupera la cronología de la publicidad y los anuncios correspondientes del servidor. Esta fuente es común para flujos de VOD.

   Normalmente, TVSDK inserta los anuncios resueltos en el contenido principal, tal como indica el mapa del servidor.

>[!NOTE]
>
>De forma predeterminada, el TVSDK utiliza señales de manifiesto para flujos en directo/lineales y mapas de servidores de publicidad para flujos de VOD. Sin embargo, para admitir la reproducción de eventos completos en eventos en directo, la aplicación debe realizar pasos adicionales.

