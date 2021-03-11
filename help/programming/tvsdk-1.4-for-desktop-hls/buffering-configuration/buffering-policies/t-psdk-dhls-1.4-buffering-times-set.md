---
description: MediaPlayer proporciona métodos para establecer y obtener el tiempo de almacenamiento en búfer inicial y el tiempo de almacenamiento en búfer de reproducción.
title: Establecer tiempos de almacenamiento en búfer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# Definir tiempos de almacenamiento en búfer{#set-buffering-times}

MediaPlayer proporciona métodos para establecer y obtener el tiempo de almacenamiento en búfer inicial y el tiempo de almacenamiento en búfer de reproducción.

>[!TIP]
>
>Si no establece los parámetros de control de búfer antes de comenzar la reproducción, el reproductor de medios toma como valor predeterminado 2 segundos para el búfer inicial y 30 segundos para el tiempo de búfer de reproducción en curso.

1. Configure el objeto `BufferControlParameters`, que encapsula el tiempo de búfer inicial y los parámetros de control de tiempo de búfer de reproducción:

       Esta clase proporciona los siguientes métodos de fábrica:
   
   * Para establecer el tiempo de búfer inicial igual al tiempo de búfer de reproducción:

      ```
      createSimple(bufferTime:uint):BufferControlParameters
      ```

   * Para establecer los tiempos de búfer inicial y de reproducción:

      ```
      createDual(initialBufferTime:uint, playbackBufferTime:uint):BufferControlParameters 
      ```

      Estos métodos generan un `IllegalArgumentException` si los parámetros no son válidos, como cuando:

   * El tiempo de búfer inicial es inferior a cero.
   * El tiempo de búfer inicial es bueno que el tiempo de búfer.

1. Para establecer los valores de los parámetros de búfer, utilice este método `MediaPlayer`:

   ```
   public function set bufferControlParameters(value:BufferControlParameters):void
   ```

1. Para obtener los valores de parámetro de búfer actuales, utilice este método `MediaPlayer`:

   ```
   public function get bufferControlParameters():BufferControlParameters
   ```

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

Por ejemplo, para establecer el búfer inicial en 2 segundos y el tiempo de búfer de reproducción en 30 segundos:

```
mediaPlayer.bufferControlParameters = BufferControlParameters.createDual(2000, 30000); 
```

El `psdkdemo` muestra esta función; utilice la configuración de la aplicación para establecer los valores del búfer.
