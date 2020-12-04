---
description: Puede personalizar o anular los comportamientos de publicidad.
seo-description: Puede personalizar o anular los comportamientos de publicidad.
seo-title: Configurar la reproducción personalizada
title: Configurar la reproducción personalizada
uuid: 479ca1b0-6b3f-42fa-85e1-31d707da8730
translation-type: tm+mt
source-git-commit: a21a5fcc819a7bec58ad36e118d04f462ec3fd92
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# Configurar la reproducción personalizada{#set-up-customized-playback}

Puede personalizar o anular los comportamientos de publicidad.

Antes de poder personalizar o anular los comportamientos de publicidad, registre la instancia de directiva de publicidad con .
Para personalizar los comportamientos de las publicidades, realice una de las siguientes acciones:

* Implementar la interfaz `AdPolicySelector` y todos sus métodos.

   Esta opción se recomienda si necesita anular **todos** los comportamientos de publicidad predeterminados.

* Amplíe la clase `DefaultAdPolicySelector` y proporcione implementaciones solo para los comportamientos que requieren personalización.

   Esta opción se recomienda si necesita anular sólo **algunos** de los comportamientos predeterminados.

Para ambas opciones, complete las siguientes tareas:

1. Implemente su propio selector de directivas de publicidad personalizado.

   ```
   public class CustomAdPolicySelector implements AdPolicySelector { 
       // your own customization here 
   }
   ```

1. Amplíe la fábrica de contenido para utilizar el selector de directivas de publicidad personalizado.

   ```
   public class CustomContentFactory extends DefaultContentFactory { 
       /** 
        * @inheritDoc 
        */ 
       override protected function doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector { 
           return new CustomAdPolicySelector(item); 
       } 
   }
   ```

   ```
   psdkutils::PSDKSharedPointer<psdk::ContentFactory> factory; 
   psdkFactory->createDefaultContentFactory(&factory); 
   psdkutils::PSDKSharedPointer<psdk::AdPolicySelector> defaultAdPolicySelector; 
   factory->retrieveAdPolicySelector(item, &defaultAdPolicySelector);
   ```

1. Registre la nueva fábrica de contenido que usará TVSDK en el flujo de trabajo de publicidad.

   ```
   PSDKConfig.advertisingFactory = new CustomContentFactory();
   ```

   >[!TIP]
   >
   >Si la fábrica de contenido personalizado se registró para un flujo específico a través de la clase `MediaPlayerItemConfig`, se borrará cuando se desasigne la instancia `MediaPlayer`. La aplicación debe registrarla cada vez que se cree una nueva sesión de reproducción.