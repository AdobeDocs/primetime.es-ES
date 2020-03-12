---
description: MediaPlayer proporciona métodos para establecer y obtener el tiempo de almacenamiento en búfer inicial y el tiempo de almacenamiento en búfer de reproducción.
seo-description: MediaPlayer proporciona métodos para establecer y obtener el tiempo de almacenamiento en búfer inicial y el tiempo de almacenamiento en búfer de reproducción.
seo-title: Establecer horas de almacenamiento en búfer
title: Establecer horas de almacenamiento en búfer
uuid: 25142b01-5381-49c9-b89a-24c858faaf13
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Establecer horas de almacenamiento en búfer{#set-buffering-times}

MediaPlayer proporciona métodos para establecer y obtener el tiempo de almacenamiento en búfer inicial y el tiempo de almacenamiento en búfer de reproducción.

>[!TIP]
>
>Si no establece los parámetros de control del búfer antes de iniciar la reproducción, el reproductor de medios toma el valor predeterminado de 2 segundos para el búfer inicial y 30 segundos para el tiempo de búfer de reproducción en curso.

1. Configure el `BufferControlParameters` objeto, que encapsula el tiempo de búfer inicial y los parámetros de control de tiempo del búfer de reproducción:

       Esta clase proporciona los siguientes métodos de fábrica:
   
   * Para establecer el tiempo de búfer inicial igual al tiempo de búfer de reproducción:

      ```
      createSimple(bufferTime:uint):BufferControlParameters
      ```

   * Para configurar los tiempos de búfer inicial y de reproducción:

      ```
      createDual(initialBufferTime:uint, playbackBufferTime:uint):BufferControlParameters 
      ```

      Estos métodos generan un error `IllegalArgumentException` si los parámetros no son válidos, como cuando:

   * El tiempo de búfer inicial es menor que cero.
   * El tiempo de búfer inicial es bueno al tiempo de búfer.

1. Para establecer los valores de los parámetros de búfer, utilice este `MediaPlayer` método:

   ```
   public function set bufferControlParameters(value:BufferControlParameters):void
   ```

1. Para obtener los valores de parámetro de búfer actuales, utilice este `MediaPlayer` método:

   ```
   public function get bufferControlParameters():BufferControlParameters
   ```

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

Por ejemplo, para establecer el búfer inicial en 2 segundos y el tiempo del búfer de reproducción en 30 segundos:

```
mediaPlayer.bufferControlParameters = BufferControlParameters.createDual(2000, 30000); 
```

La `psdkdemo` muestra esta función; utilice la configuración de la aplicación para establecer los valores del búfer.
