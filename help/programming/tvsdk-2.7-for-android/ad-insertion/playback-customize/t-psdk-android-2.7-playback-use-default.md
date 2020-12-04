---
description: Puede elegir usar comportamientos de publicidad predeterminados.
seo-description: Puede elegir usar comportamientos de publicidad predeterminados.
seo-title: Usar el comportamiento de reproducción predeterminado
title: Usar el comportamiento de reproducción predeterminado
uuid: 20785251-eb2f-4cc0-b919-1a88c0b1c57c
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---


# Usar el comportamiento de reproducción predeterminado {#use-the-default-playback-behavior}

Puede elegir usar comportamientos de publicidad predeterminados.

1. Para utilizar los comportamientos predeterminados, realice una de las siguientes tareas:

   * Si implementa su propia clase `AdvertisingFactory`, devuelva null para `createAdPolicySelector`.

   * Si no tiene una implementación personalizada para la clase `AdvertisingFactory`, TVSDK utiliza un selector de directivas de publicidad predeterminado.

## Configurar la reproducción personalizada {#set-up-customized-playback}

Puede personalizar o anular los comportamientos de publicidad.

Antes de personalizar o anular los comportamientos de publicidad, registre la instancia de directiva de publicidad con TVSDK.

* Implementar la interfaz `AdPolicySelector` y todos sus métodos.

   Esta opción se recomienda si necesita anular **todos** los comportamientos de publicidad predeterminados.

* Amplíe la clase `DefaultAdPolicySelector` y proporcione implementaciones solo para los comportamientos que requieren personalización.

   Esta opción se recomienda si necesita anular sólo **algunos** de los comportamientos predeterminados.

Para personalizar los comportamientos de publicidad:

1. Implementar la interfaz `AdPolicySelector` y todos sus métodos.
1. Asigne la instancia de directiva que usará TVSDK a través de la fábrica de publicidad.

   >[!NOTE]
   >
   >Las directivas de publicidad personalizadas registradas al principio de la reproducción se borran cuando se desasigna la instancia `MediaPlayer`. La aplicación debe registrar una instancia de selector de políticas cada vez que se cree una nueva sesión de reproducción.

   Por ejemplo:

   ```java
   class CustomContentFactory extends ContentFactory { 
       ... 
       @Override 
       public AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
           return new CustomAdPolicySelector(mediaPlayerItem); 
       } 
       ... 
   } 
   
   // register the custom content factory with media player 
   MediaPlayerItemConfig config =  new MediaPlayerItemConfig(); 
   config.setAdvertisingFactory(new CustomContentFactory()); 
   
   // this config will should be later passed while loading the resource 
   mediaPlayer.replaceCurrentResource(resource, config);
   ```

1. Implemente sus personalizaciones.