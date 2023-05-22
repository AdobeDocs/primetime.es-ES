---
description: Puede personalizar o anular los comportamientos de los anuncios.
title: Configuración de la reproducción personalizada
exl-id: 28c28589-9e94-40de-b921-1bffc0392c29
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Configuración de la reproducción personalizada{#set-up-customized-playback}

Puede personalizar o anular los comportamientos de los anuncios.

Para poder personalizar o anular los comportamientos de los anuncios, registre la instancia de directiva de publicidad con
Para personalizar los comportamientos de los anuncios, realice una de las siguientes acciones:

* Implementación de `AdPolicySelector` y todos sus métodos.

   Esta opción se recomienda si necesita anular la **todo** los comportamientos de anuncio predeterminados.

* Ampliación de la `DefaultAdPolicySelector` y proporcionan implementaciones solo para los comportamientos que requieren personalización.

   Esta opción se recomienda si solo necesita anular la selección **algunos** de los comportamientos predeterminados.

Para ambas opciones, complete las siguientes tareas:

1. Implemente su propio selector personalizado de políticas de publicidad.

   ```
   public class CustomAdPolicySelector implements AdPolicySelector { 
       // your own customization here 
   }
   ```

1. Amplíe la fábrica de contenido para utilizar el selector personalizado de directivas de publicidad.

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

1. Registre la nueva fábrica de contenido que TVSDK utilizará en el flujo de trabajo de publicidad.

   ```
   PSDKConfig.advertisingFactory = new CustomContentFactory();
   ```

   >[!TIP]
   >
   >Si la fábrica de contenido personalizado se registró para un flujo específico a través de la `MediaPlayerItemConfig` clase, se borrará cuando la variable `MediaPlayer` La instancia de está desasignada. La aplicación debe registrarla cada vez que se cree una nueva sesión de reproducción.
