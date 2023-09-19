---
description: Puede elegir utilizar comportamientos de anuncio predeterminados.
title: Usar el comportamiento de reproducción predeterminado
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Usar el comportamiento de reproducción predeterminado  {#use-the-default-playback-behavior}

Puede elegir utilizar comportamientos de anuncio predeterminados.

1. Para utilizar comportamientos predeterminados, complete una de las siguientes tareas:

   * Si implementa los suyos propios `AdvertisingFactory` clase, devolver nulo para `createAdPolicySelector`.

   * Si no tiene una implementación personalizada para el `AdvertisingFactory` , TVSDK utiliza un selector predeterminado de directivas de publicidad.

## Configuración de la reproducción personalizada {#set-up-customized-playback}

Puede personalizar o anular los comportamientos de los anuncios.

Antes de personalizar o anular los comportamientos de anuncio, registre la instancia de directiva de publicidad con TVSDK.

* Implementación de `AdPolicySelector` y todos sus métodos.

  Esta opción se recomienda si necesita anular la **todo** los comportamientos de anuncio predeterminados.

* Ampliación de la `DefaultAdPolicySelector` y proporcionan implementaciones solo para los comportamientos que requieren personalización.

  Esta opción se recomienda si solo necesita anular la selección **algunos** de los comportamientos predeterminados.

Para personalizar los comportamientos de los anuncios:

1. Implementación de `AdPolicySelector` y todos sus métodos.
1. Asigne la instancia de directiva que utilizará TVSDK a través de la fábrica de publicidad.

   >[!NOTE]
   >
   >Las políticas de publicidad personalizadas que se registran al principio de la reproducción se borran cuando `MediaPlayer` La instancia de está desasignada. La aplicación debe registrar una instancia de selector de directivas cada vez que se cree una nueva sesión de reproducción.

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

1. Implementar las personalizaciones.
