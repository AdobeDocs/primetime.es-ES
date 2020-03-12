---
description: Existen varias formas de determinar la inserción y la colocación de las publicidades.
seo-description: Existen varias formas de determinar la inserción y la colocación de las publicidades.
seo-title: Inserción y colocación de anuncios
title: Inserción y colocación de anuncios
uuid: 1d4d6364-1c49-402b-9b72-8c185b1c94e1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Inserción y colocación de anuncios{#ad-insertion-and-placement}

Existen varias formas de determinar la inserción y la colocación de las publicidades.

## Inserción de publicidad {#section_1F7581B987704E318E064082190E8243}

A continuación se muestra una descripción general del proceso utilizado para determinar la inserción de publicidades:

1. **Detección** de oportunidades: El SDK de TVSDK utiliza la información de flujo para detectar ubicaciones posibles y deseadas de anuncios.
1. **Resolución** de publicidad: El TVSDK se comunica con un servidor de publicidad para recuperar las publicidades que se van a dividir en el contenido.
1. **Ubicación** de publicidad: El TVSDK carga las publicidades especificadas y las coloca en saltos de publicidad en la línea de tiempo de contenido en las ubicaciones especificadas y vuelve a calcular la línea de tiempo virtual, si es necesario.

## Colocación de publicidad {#section_B9D63F7409A2447F9FF209289BE5D3D5}

El TVSDK puede obtener ubicaciones para la posible colocación de publicidad desde las siguientes fuentes:

* **Metadatos/indicaciones de manifiesto**

   El TVSDK detecta las indicaciones, extrae la información necesaria de estas indicaciones y se comunica con un servidor de publicidad para obtener las publicidades correspondientes. Esta fuente es común para flujos en vivo/lineales.

   El TVSDK suele reemplazar el contenido principal por los anuncios en la ubicación indicada por los metadatos o las indicaciones; de lo contrario, el cliente dejaría cada vez más atrás el punto real.

* **El mapa del servidor de publicidad**

   Normalmente, los metadatos sobre estos flujos se registran en el servidor de publicidad antes de la reproducción. TVSDK recupera la línea de tiempo de la publicidad y las publicidades correspondientes del servidor. Esta fuente es común para los flujos de VOD.

   El TVSDK suele insertar las publicidades resueltas en el contenido principal como indica el mapa del servidor.

>[!NOTE]
>
>De forma predeterminada, TVSDK utiliza señales de manifiesto para flujos en directo/lineales y mapas de servidores de publicidad para flujos VOD. Sin embargo, para admitir la reproducción de eventos completos en eventos en directo, la aplicación debe realizar pasos adicionales.

