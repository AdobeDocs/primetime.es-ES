---
description: La aplicación debe utilizar los objetos TimedMetadata adecuados en los momentos adecuados.
seo-description: La aplicación debe utilizar los objetos TimedMetadata adecuados en los momentos adecuados.
seo-title: Almacenar objetos de metadatos temporizados a medida que se distribuyen
title: Almacenar objetos de metadatos temporizados a medida que se distribuyen
uuid: 0d0ddfea-6f32-467d-91bc-f18ceadcd842
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Almacenar objetos de metadatos temporizados a medida que se distribuyen {#store-timed-metadata-objects-as-they-are-dispatched}

La aplicación debe utilizar los objetos TimedMetadata adecuados en los momentos adecuados.

Durante el análisis de contenido, que se realiza antes de la reproducción, TVSDK identifica las etiquetas suscritas y notifica a la aplicación sobre estas etiquetas.

>[!TIP]
>
>El tiempo que se asocia a cada uno `TimedMetadata` es la hora local en la línea de tiempo de reproducción.

Para almacenar objetos de metadatos temporizados a medida que se distribuyen:

1. Realice un seguimiento del tiempo de reproducción actual.
1. Haga coincidir el tiempo de reproducción actual con los objetos `TimedMetadata` enviados.

1. Utilice el `TimedMetadata` punto en el que la hora de inicio es igual al tiempo de reproducción local actual.

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

