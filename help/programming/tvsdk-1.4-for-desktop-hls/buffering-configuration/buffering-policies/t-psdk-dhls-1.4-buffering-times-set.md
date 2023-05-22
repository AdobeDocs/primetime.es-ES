---
description: MediaPlayer proporciona métodos para establecer y obtener el tiempo de almacenamiento en búfer inicial y el tiempo de almacenamiento en búfer de reproducción.
title: Establecer tiempos de almacenamiento en búfer
exl-id: d2fbae05-2190-4acc-ae63-561db030608a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# Establecer tiempos de almacenamiento en búfer{#set-buffering-times}

MediaPlayer proporciona métodos para establecer y obtener el tiempo de almacenamiento en búfer inicial y el tiempo de almacenamiento en búfer de reproducción.

>[!TIP]
>
>Si no define los parámetros de control del búfer antes de comenzar la reproducción, el reproductor de contenido toma como valor predeterminado 2 segundos para el búfer inicial y 30 segundos para el tiempo de búfer de reproducción en curso.

1. Configure las variables `BufferControlParameters` , que encapsula los parámetros iniciales de control de tiempo del búfer de reproducción y tiempo del búfer de reproducción:

       Esta clase proporciona los siguientes métodos de fábrica:
   
   * Para establecer el tiempo de búfer inicial igual al tiempo de búfer de reproducción:

      ```
      createSimple(bufferTime:uint):BufferControlParameters
      ```

   * Para definir los tiempos iniciales y del búfer de reproducción:

      ```
      createDual(initialBufferTime:uint, playbackBufferTime:uint):BufferControlParameters 
      ```

      Estos métodos inician un `IllegalArgumentException` si los parámetros no son válidos, como cuando:

   * El tiempo de búfer inicial es inferior a cero.
   * El tiempo de búfer inicial es bueno que el tiempo de búfer.

1. Para establecer los valores de los parámetros de búfer, utilice este `MediaPlayer` método:

   ```
   public function set bufferControlParameters(value:BufferControlParameters):void
   ```

1. Para obtener los valores actuales de los parámetros de búfer, utilice esta opción `MediaPlayer` método:

   ```
   public function get bufferControlParameters():BufferControlParameters
   ```

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

Por ejemplo, para establecer el búfer inicial en 2 segundos y el tiempo de búfer de reproducción en 30 segundos:

```
mediaPlayer.bufferControlParameters = BufferControlParameters.createDual(2000, 30000); 
```

El `psdkdemo` muestra esta característica; utilice la configuración de la aplicación para establecer los valores del búfer.
