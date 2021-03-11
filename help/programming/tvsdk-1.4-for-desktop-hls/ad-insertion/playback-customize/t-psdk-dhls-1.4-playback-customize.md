---
description: Puede personalizar o anular los comportamientos publicitarios.
title: Configuración de una reproducción personalizada
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Configurar la reproducción personalizada{#set-up-customized-playback}

Puede personalizar o anular los comportamientos publicitarios.

Para poder personalizar o anular los comportamientos de publicidad, registre la instancia de directiva de publicidad con .
Para personalizar los comportamientos publicitarios, realice una de las siguientes acciones:

* Implemente la interfaz `AdPolicySelector` y todos sus métodos.

   Se recomienda esta opción si necesita anular **todos** los comportamientos publicitarios predeterminados.

* Amplíe la clase `DefaultAdPolicySelector` y proporcione implementaciones solo para los comportamientos que requieren personalización.

   Esta opción se recomienda si necesita anular solo **algunos** de los comportamientos predeterminados.

Para ambas opciones, complete las siguientes tareas:

1. Implemente su propio selector de políticas de publicidad personalizado.

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

1. Registre la nueva fábrica de contenido que utilizará TVSDK en el flujo de trabajo de publicidad.

   ```
   PSDKConfig.advertisingFactory = new CustomContentFactory();
   ```

   >[!TIP]
   >
   >Si la factoría de contenido personalizado se registró para un flujo específico a través de la clase `MediaPlayerItemConfig`, se borrará cuando se desasigne la instancia `MediaPlayer`. La aplicación debe registrarla cada vez que se crea una nueva sesión de reproducción.