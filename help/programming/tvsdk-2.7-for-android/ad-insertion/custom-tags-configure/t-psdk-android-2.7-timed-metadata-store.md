---
description: La aplicación debe utilizar los objetos TimedMetadata adecuados en los momentos apropiados.
title: Almacenar objetos de metadatos cronometrados a medida que se envían
exl-id: da7ee636-f3ac-4aac-9ca0-7075b8c910f0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Almacenar objetos de metadatos cronometrados a medida que se envían {#store-timed-metadata-objects-as-they-are-dispatched}

La aplicación debe utilizar los objetos TimedMetadata adecuados en los momentos apropiados.

Durante el análisis de contenido, que se produce antes de la reproducción, TVSDK identifica las etiquetas suscritas y notifica a la aplicación sobre estas etiquetas.

>[!TIP]
>
>La hora asociada a cada una `TimedMetadata` es la hora local en la cronología de la reproducción.

Para almacenar objetos de metadatos cronometrados a medida que se van distribuyendo:

1. Realizar un seguimiento del tiempo de reproducción actual.
1. Hacer coincidir el tiempo de reproducción actual con el tiempo de envío `TimedMetadata` objetos.

1. Utilice el `TimedMetadata` donde la hora de inicio es igual a la hora de reproducción local actual.

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
