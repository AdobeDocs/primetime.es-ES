---
description: La aplicación debe utilizar los objetos TimedMetadata adecuados en los momentos apropiados.
title: Almacenar objetos de metadatos temporizados a medida que se envían
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---


# Almacenar objetos de metadatos temporizados a medida que se envían {#store-timed-metadata-objects-as-they-are-dispatched}

La aplicación debe utilizar los objetos TimedMetadata adecuados en los momentos apropiados.

Durante el análisis de contenido, que ocurre antes de la reproducción, TVSDK identifica las etiquetas suscritas y notifica a la aplicación sobre estas etiquetas.

>[!TIP]
>
>El tiempo asociado a cada `TimedMetadata` es la hora local en la línea de tiempo de reproducción.

Para almacenar objetos de metadatos temporizados a medida que se envían:

1. Realice un seguimiento del tiempo de reproducción actual.
1. Haga coincidir el tiempo de reproducción actual con los objetos `TimedMetadata` distribuidos.

1. Utilice el `TimedMetadata` donde la hora de inicio es igual al tiempo de reproducción local actual.

   El siguiente ejemplo muestra cómo guardar `TimedMetadata` objetos en un `ArrayList`.

   ```java
   private List<TimedMetadata> _timedMetadataList =  
     new ArrayList<TimedMetadata>(); 
   ... 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       ... 
       if (timedMetadata.getName().equalsIgnoreCase("#EXT-X-CUE"))  { 
           _timedMetadataList.add(timedMetadata); 
       } 
       ... 
   }
   ```

