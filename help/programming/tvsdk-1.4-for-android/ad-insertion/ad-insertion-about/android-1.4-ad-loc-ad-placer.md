---
description: Existen varias formas de determinar la inserción y la ubicación de los anuncios.
title: Inserción y colocación de publicidad
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Inserción y colocación de publicidad{#ad-insertion-and-placement}

Existen varias formas de determinar la inserción y la ubicación de los anuncios.

## Inserción de publicidad {#section_1F7581B987704E318E064082190E8243}

A continuación se muestra una descripción general del proceso utilizado para determinar la inserción de publicidad:

1. **Detección de oportunidad**: el TVSDK utiliza información de flujo para detectar posibles ubicaciones y los deseos de los anuncios.
1. **Resolución de anuncio**: el TVSDK se comunica con un servidor de publicidad para recuperar los anuncios que se van a insertar en el contenido.
1. **Ubicación del anuncio**: TVSDK carga los anuncios especificados y los coloca en pausas publicitarias en la cronología del contenido en las ubicaciones especificadas y vuelve a calcular la cronología virtual, si es necesario.

## Ubicación del anuncio {#section_B9D63F7409A2447F9FF209289BE5D3D5}

El TVSDK puede obtener ubicaciones para una posible ubicación de anuncios desde las siguientes fuentes:

* **Metadatos/señales de manifiesto**

  El TVSDK detecta las señales, extrae la información necesaria de estas señales y se comunica con un servidor de publicidad para obtener los anuncios correspondientes. Esta fuente es común para emisiones en directo/lineales.

  El TVSDK generalmente reemplaza el contenido principal con los anuncios en la ubicación indicada por los metadatos/señales; de lo contrario, el cliente dejaría cada vez más detrás del punto en directo real.

* **El mapa del servidor de publicidad**

  Normalmente, los metadatos sobre estos flujos se registran en el servidor de publicidad antes de la reproducción. TVSDK recupera la cronología de la publicidad y los anuncios correspondientes del servidor. Esta fuente es común para flujos de VOD.

  Normalmente, TVSDK inserta los anuncios resueltos en el contenido principal tal como indica el mapa del servidor.

>[!NOTE]
>
>De forma predeterminada, TVSDK utiliza señales de manifiesto para flujos lineales/activos y mapas de servidor de publicidad para flujos de VOD. Sin embargo, para admitir la reproducción de eventos completos para eventos en directo, la aplicación debe realizar pasos adicionales.
