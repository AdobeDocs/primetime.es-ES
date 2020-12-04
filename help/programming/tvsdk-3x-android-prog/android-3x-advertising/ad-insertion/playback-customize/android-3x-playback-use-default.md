---
description: Puede elegir usar comportamientos de publicidad predeterminados.
seo-description: Puede elegir usar comportamientos de publicidad predeterminados.
seo-title: Usar el comportamiento de reproducción predeterminado
title: Usar el comportamiento de reproducción predeterminado
uuid: 36f76c42-4c6c-4620-9b47-ec97519a642a
translation-type: tm+mt
source-git-commit: 6da7d597503d98875735c54e9a794f8171ad408b
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# Usar el comportamiento de reproducción predeterminado {#use-the-default-playback-behavior}

Puede elegir usar comportamientos de publicidad predeterminados.

1. Para utilizar los comportamientos predeterminados, realice una de las siguientes tareas:

   * Si implementa su propia clase `AdvertisingFactory`, devuelva null para `createAdPolicySelector`.

   * Si no tiene una implementación personalizada para la clase `AdvertisingFactory`, TVSDK utiliza un selector de directivas de publicidad predeterminado.

## Configurar la reproducción personalizada {#set-up-customized-playback}

Puede personalizar o anular los comportamientos de publicidad.

Antes de poder personalizar o anular los comportamientos de publicidad, registre la instancia de directiva de publicidad con .
Para personalizar los comportamientos de las publicidades, realice una de las siguientes acciones:

* Implementar la interfaz `AdPolicySelector` y todos sus métodos.

   Esta opción se recomienda si necesita anular **todos** los comportamientos de publicidad predeterminados.

* Amplíe la clase `DefaultAdPolicySelector` y proporcione implementaciones solo para los comportamientos que requieren personalización.

   Esta opción se recomienda si necesita anular sólo **algunos** de los comportamientos predeterminados.

Para personalizar los comportamientos de publicidad:

1. Implementar la interfaz `AdPolicySelector` y todos sus métodos.
1. Asigne la instancia de directiva que usará TVSDK a través de la fábrica de publicidad.

   >[!NOTE]
   >
   >class CustomContentFactory extiende ContentFactory &amp;lbrace;
   >...
   >@Override
   >public AdPolicySelector recuperarAdPolicySelector>>(MediaPlayerItem mediaPlayerItem) &amp;lbrace;
   >return new CustomAdPolicySelector(mediaPlayerItem);
   >&amp;rbrace;
   >...
   >&amp;rbrace;
   >// registrar la fábrica de contenido personalizado con el reproductor de medios
   >Configuración de MediaPlayerItemConfig = new MediaPlayerItemConfig();
   >config.setAdvertisingFactory(new CustomContentFactory());
   >// esta configuración debe pasarse más tarde mientras se carga >el recurso
   >mediaPlayer.replaceCurrentResource(resource, config);

1. Implemente sus personalizaciones.
