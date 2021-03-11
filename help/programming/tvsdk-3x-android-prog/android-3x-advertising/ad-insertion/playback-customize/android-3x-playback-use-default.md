---
description: Puede elegir usar comportamientos de publicidad predeterminados.
title: Uso del comportamiento de reproducción predeterminado
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# Utilizar el comportamiento de reproducción predeterminado {#use-the-default-playback-behavior}

Puede elegir usar comportamientos de publicidad predeterminados.

1. Para utilizar comportamientos predeterminados, realice una de las siguientes tareas:

   * Si implementa su propia clase `AdvertisingFactory`, devuelva null para `createAdPolicySelector`.

   * Si no tiene una implementación personalizada para la clase `AdvertisingFactory` , TVSDK utiliza un selector de políticas de publicidad predeterminado.

## Configurar la reproducción personalizada {#set-up-customized-playback}

Puede personalizar o anular los comportamientos publicitarios.

Para poder personalizar o anular los comportamientos de publicidad, registre la instancia de directiva de publicidad con .
Para personalizar los comportamientos publicitarios, realice una de las siguientes acciones:

* Implemente la interfaz `AdPolicySelector` y todos sus métodos.

   Se recomienda esta opción si necesita anular **todos** los comportamientos publicitarios predeterminados.

* Amplíe la clase `DefaultAdPolicySelector` y proporcione implementaciones solo para los comportamientos que requieren personalización.

   Esta opción se recomienda si necesita anular solo **algunos** de los comportamientos predeterminados.

Para personalizar el comportamiento de los anuncios:

1. Implemente la interfaz `AdPolicySelector` y todos sus métodos.
1. Asigne la instancia de directiva que utilizará TVSDK a través de la fábrica de publicidad.

   >[!NOTE]
   >
   >Clase CustomContentFactory extiende ContentFactory &amp;lbrace;
   >...
   >@Override
   >public AdPolicySelector retrieveAdPolicySelector>>(MediaPlayerItem mediaPlayerItem) &amp;lbrace;
   >return new CustomAdPolicySelector(mediaPlayerItem);
   >&amp;llave;
   >...
   >&amp;llave;
   >// registrar la fábrica de contenido personalizado con reproductor de medios
   >Configuración de MediaPlayerItemConfig = new MediaPlayerItemConfig();
   >config.setAdvertisingFactory(new CustomContentFactory());
   >// esta configuración debe pasarse más tarde mientras se carga >el recurso
   >mediaPlayer.replaceCurrentResource(resource, config);

1. Implemente sus personalizaciones.
