---
description: Puede elegir usar comportamientos de publicidad predeterminados.
title: Uso del comportamiento de reproducción predeterminado
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Utilizar el comportamiento de reproducción predeterminado {#use-the-default-playback-behavior}

Puede elegir usar comportamientos de publicidad predeterminados.

1. Para utilizar comportamientos predeterminados, realice una de las siguientes tareas:

   * Si implementa su propia clase `AdvertisingFactory`, devuelva null para `createAdPolicySelector`.

   * Si no tiene una implementación personalizada para la clase `AdvertisingFactory` , TVSDK utiliza un selector de políticas de publicidad predeterminado.

## Configurar la reproducción personalizada {#set-up-customized-playback}

Puede personalizar o anular los comportamientos publicitarios.

Antes de personalizar o anular los comportamientos publicitarios, registre la instancia de directiva de publicidad con TVSDK.

* Implemente la interfaz `AdPolicySelector` y todos sus métodos.

   Se recomienda esta opción si necesita anular **todos** los comportamientos publicitarios predeterminados.

* Amplíe la clase `DefaultAdPolicySelector` y proporcione implementaciones solo para los comportamientos que requieren personalización.

   Esta opción se recomienda si necesita anular solo **algunos** de los comportamientos predeterminados.

Para personalizar el comportamiento de los anuncios:

1. Implemente la interfaz `AdPolicySelector` y todos sus métodos.
1. Asigne la instancia de directiva que utilizará TVSDK a través de la fábrica de publicidad.

   >[!NOTE]
   >
   >Las políticas de publicidad personalizadas que se registran al principio de la reproducción se borran cuando se desasigna la instancia `MediaPlayer` . La aplicación debe registrar una instancia de selector de políticas cada vez que se crea una nueva sesión de reproducción.

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