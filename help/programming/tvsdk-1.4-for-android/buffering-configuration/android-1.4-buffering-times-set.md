---
description: Para proporcionar una experiencia de visualización más fluida, TVSDK a veces almacena en búfer el flujo de vídeo. Puede configurar la forma en que el reproductor se almacena en búfer.
title: Establecer tiempos de almacenamiento en búfer
exl-id: 4542d10a-b6f8-430d-8b9a-5a358d1c0e9d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Almacenamiento en búfer {#buffering}

Para proporcionar una experiencia de visualización más fluida, TVSDK a veces almacena en búfer el flujo de vídeo. Puede configurar la forma en que el reproductor se almacena en búfer.

TVSDK define una duración del búfer de reproducción de al menos 30 segundos y un tiempo de búfer inicial en ese intervalo de tiempo, antes de que el contenido comience a reproducirse, de al menos 2 segundos. Después de que la aplicación invoque `play` pero antes de que comience la reproducción, TVSDK almacena en búfer el contenido hasta el momento inicial para proporcionar un inicio sin problemas cuando comienza a reproducirse.

Puede modificar los tiempos de almacenamiento en búfer definiendo nuevas directivas de almacenamiento en búfer y puede modificar cuándo se produce el almacenamiento en búfer inicial mediante el uso de activación instantánea.

## Establecer tiempos de almacenamiento en búfer {#set-buffering-times}

El `MediaPlayer` proporciona métodos para establecer y obtener el tiempo de almacenamiento en búfer inicial y el tiempo de almacenamiento en búfer de reproducción.

>[!TIP]
>
>Si no define los parámetros de control del búfer antes de comenzar la reproducción, el reproductor de contenido toma como valor predeterminado 2 segundos para el búfer inicial y 30 segundos para el tiempo de búfer de reproducción en curso.

1. Configure las variables `BufferControlParameters` , que encapsula los parámetros iniciales de control de tiempo del búfer de reproducción y tiempo del búfer de reproducción:

       Esta clase proporciona dos métodos de fábrica:
   
   * Para establecer el tiempo de búfer inicial igual al tiempo de búfer de reproducción:

      ```java
      public static BufferControlParameters createSimple( 
          long bufferTime)
      ```

   * Para definir los tiempos iniciales y del búfer de reproducción:

      ```java
      public static BufferControlParameters createDual( 
          long initialBuffer,   
          long bufferTime)
      ```

      Estos métodos inician un `IllegalArgumentException` si los parámetros no son válidos, como cuando:

   * El tiempo de búfer inicial es inferior a cero.
   * El tiempo de búfer inicial es bueno que el tiempo de búfer.

1. Para establecer los valores de los parámetros de búfer, utilice este `MediaPlayer` método:

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. Para obtener los valores actuales de los parámetros de búfer, utilice esta opción `MediaPlayer` método:

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

   Si el AVE no puede establecer los valores especificados, el reproductor de contenido introduce el `ERROR` estado con el código de error `SET_BUFFER_PARAMETERS_ERROR`.

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

Por ejemplo, para establecer el búfer inicial en 2 segundos y el tiempo de búfer de reproducción en 30 segundos:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(2000, 30000));
```

La implementación de referencia de Primetime muestra esta característica; utilice la configuración de la aplicación para establecer los valores del búfer.
