---
description: La aplicación debe utilizar los objetos TimedMetadata adecuados en los momentos adecuados.
seo-description: La aplicación debe utilizar los objetos TimedMetadata adecuados en los momentos adecuados.
seo-title: Almacenar objetos de metadatos temporizados a medida que se distribuyen
title: Almacenar objetos de metadatos temporizados a medida que se distribuyen
uuid: 0e6d2a42-37a8-477e-b925-66bbc23445c1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Almacenar objetos de metadatos temporizados a medida que se distribuyen {#store-timed-metadata-objects-as-they-are-dispatched}

La aplicación debe utilizar los objetos TimedMetadata adecuados en los momentos adecuados.

Durante el análisis de contenido, que se realiza antes de la reproducción, TVSDK identifica las etiquetas suscritas y notifica a la aplicación sobre estas etiquetas. El tiempo asociado a cada `TimedMetadata` es la hora local en la línea de tiempo de reproducción.

La aplicación debe completar las siguientes tareas:

1. Realice un seguimiento del tiempo de reproducción actual.
1. Haga coincidir el tiempo de reproducción actual con los objetos `TimedMetadata` enviados.

1. Utilice el `TimedMetadata` donde el tiempo de inicio es igual al tiempo de reproducción local actual.

   El siguiente ejemplo muestra cómo guardar `TimedMetadata` objetos en un `ArrayList`.

   ```java
   private List<TimedMetadata> _timedMetadataList = new ArrayList<TimedMetadata>(); 
   ... 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       ... 
       if (timedMetadata.getName().equalsIgnoreCase("#EXT-X-CUE"))  { 
           _timedMetadataList.add(timedMetadata); 
       } 
       ... 
   }
   ```

