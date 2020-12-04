---
description: Puede elegir usar comportamientos de publicidad predeterminados.
seo-description: Puede elegir usar comportamientos de publicidad predeterminados.
seo-title: Usar el comportamiento de reproducción predeterminado
title: Usar el comportamiento de reproducción predeterminado
uuid: 7139384c-167a-4cab-816a-c02fb723a5cb
translation-type: tm+mt
source-git-commit: 1985694f99c548284aad6e6b4e070bece230bdf4
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# Usar el comportamiento de reproducción predeterminado{#use-the-default-playback-behavior}

Puede elegir usar comportamientos de publicidad predeterminados.

Para utilizar comportamientos predeterminados:

* Si implementa su propia clase `ContentFactory`, devuelva una nueva instancia de `DefaultAdPolicySelector` en la implementación de `doRetrieveAdPolicySelector`.

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

* Si no tiene una implementación personalizada para la clase `ContentFactory`, TVSDK utiliza `DefaultAdPolicySelector`.