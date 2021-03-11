---
description: Puede elegir usar comportamientos de publicidad predeterminados.
title: Uso del comportamiento de reproducción predeterminado
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 0%

---


# Utilizar el comportamiento de reproducción predeterminado{#use-the-default-playback-behavior}

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