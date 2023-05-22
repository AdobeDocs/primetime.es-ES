---
description: Puede elegir utilizar comportamientos de anuncio predeterminados.
title: Usar el comportamiento de reproducción predeterminado
exl-id: 8d25e076-4335-49c8-b6b8-f2694b1b9074
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
