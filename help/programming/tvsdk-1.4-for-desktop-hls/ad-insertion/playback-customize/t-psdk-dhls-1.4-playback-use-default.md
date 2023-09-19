---
description: Puede elegir utilizar comportamientos de anuncio predeterminados.
title: Usar el comportamiento de reproducción predeterminado
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 0%

---

# Usar el comportamiento de reproducción predeterminado{#use-the-default-playback-behavior}

Puede elegir utilizar comportamientos de anuncio predeterminados.

Para utilizar comportamientos predeterminados:

* Si implementa los suyos propios `ContentFactory` clase, devuelva una nueva instancia de `DefaultAdPolicySelector` en la implementación de `doRetrieveAdPolicySelector`.

  ```
  public class CustomContentFactory extends ContentFactory { 
  
      //... 
      // your custom code for advertising classes 
      //... 
  
      /** 
       * @inheritDoc 
       */ 
      override protected function  
        doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector { 
          return new DefaultAdPolicySelector(item); 
      } 
  }
  ```

* Si no tiene una implementación personalizada para el `ContentFactory` clase, TVSDK utiliza `DefaultAdPolicySelector`.
