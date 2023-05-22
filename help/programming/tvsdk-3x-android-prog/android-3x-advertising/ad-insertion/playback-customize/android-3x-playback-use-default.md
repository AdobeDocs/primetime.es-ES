---
description: Puede elegir utilizar comportamientos de anuncio predeterminados.
title: Usar el comportamiento de reproducción predeterminado
exl-id: 0ea3d2bb-b4d4-4090-ab5f-b6c31c1abe32
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Usar el comportamiento de reproducción predeterminado {#use-the-default-playback-behavior}

Puede elegir utilizar comportamientos de anuncio predeterminados.

1. Para utilizar comportamientos predeterminados, complete una de las siguientes tareas:

   * Si implementa los suyos propios `AdvertisingFactory` clase, devolver nulo para `createAdPolicySelector`.

   * Si no tiene una implementación personalizada para el `AdvertisingFactory` , TVSDK utiliza un selector predeterminado de directivas de publicidad.

## Configuración de la reproducción personalizada {#set-up-customized-playback}

Puede personalizar o anular los comportamientos de los anuncios.

Para poder personalizar o anular los comportamientos de los anuncios, registre la instancia de directiva de publicidad con
Para personalizar los comportamientos de los anuncios, realice una de las siguientes acciones:

* Implementación de `AdPolicySelector` y todos sus métodos.

   Esta opción se recomienda si necesita anular la **todo** los comportamientos de anuncio predeterminados.

* Ampliación de la `DefaultAdPolicySelector` y proporcionan implementaciones solo para los comportamientos que requieren personalización.

   Esta opción se recomienda si solo necesita anular la selección **algunos** de los comportamientos predeterminados.

Para personalizar los comportamientos de los anuncios:

1. Implementación de `AdPolicySelector` y todos sus métodos.
1. Asigne la instancia de directiva que utilizará TVSDK a través de la fábrica de publicidad.

   >[!NOTE]
   >
   >class CustomContentFactory amplía ContentFactory &amp;lbrace;
   >...
   >@Override
   >public AdPolicySelector retrieveAdPolicySelector>>(MediaPlayerItem mediaPlayerItem) &amp;lbrace;
   >devolver nuevo CustomAdPolicySelector(mediaPlayerItem);
   >&amp;brace;
   >...
   >&amp;brace;
   >// registre la fábrica de contenido personalizado con el reproductor de medios
   >MediaPlayerItemConfig config = new MediaPlayerItemConfig();
   >config.setAdvertisingFactory(new CustomContentFactory());
   >// esta configuración debería pasarse más adelante mientras se carga >el recurso
   >mediaPlayer.replaceCurrentResource(resource, config);

1. Implementar las personalizaciones.
