---
description: Para ofrecer una experiencia de visualización más fluida, TVSDK a veces almacena en el búfer el flujo de vídeo. Puede configurar el modo en que se almacena en el búfer el reproductor.
title: Establecer tiempos de almacenamiento en búfer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---


# Almacenamiento en búfer {#buffering}

Para ofrecer una experiencia de visualización más fluida, TVSDK a veces almacena en el búfer el flujo de vídeo. Puede configurar el modo en que se almacena en el búfer el reproductor.

TVSDK define una duración del búfer de reproducción de al menos 30 segundos y un tiempo de búfer inicial dentro de él, antes de que el medio empiece a reproducirse, de al menos 2 segundos. Después de que la aplicación llama a `play` pero antes de que comience la reproducción, TVSDK almacena en búfer el contenido hasta el momento inicial para proporcionar un inicio suave cuando realmente comienza a reproducirse.

Puede modificar los tiempos de almacenamiento en búfer definiendo nuevas políticas de almacenamiento en búfer y puede modificar cuando se produzca el almacenamiento en búfer inicial mediante el uso de la función instantáneo.

## Establecer tiempos de almacenamiento en búfer {#set-buffering-times}

El `MediaPlayer` proporciona métodos para establecer y obtener el tiempo de almacenamiento en búfer inicial y el tiempo de almacenamiento en búfer de reproducción.

>[!TIP]
>
>Si no establece los parámetros de control de búfer antes de comenzar la reproducción, el reproductor de medios toma como valor predeterminado 2 segundos para el búfer inicial y 30 segundos para el tiempo de búfer de reproducción en curso.

1. Configure el objeto `BufferControlParameters`, que encapsula el tiempo de búfer inicial y los parámetros de control de tiempo de búfer de reproducción:

       Esta clase proporciona dos métodos de fábrica:
   
   * Para establecer el tiempo de búfer inicial igual al tiempo de búfer de reproducción:

      ```java
      public static BufferControlParameters createSimple( 
          long bufferTime)
      ```

   * Para establecer los tiempos de búfer inicial y de reproducción:

      ```java
      public static BufferControlParameters createDual( 
          long initialBuffer,   
          long bufferTime)
      ```

      Estos métodos generan un `IllegalArgumentException` si los parámetros no son válidos, como cuando:

   * El tiempo de búfer inicial es inferior a cero.
   * El tiempo de búfer inicial es bueno que el tiempo de búfer.

1. Para establecer los valores de los parámetros de búfer, utilice este método `MediaPlayer`:

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. Para obtener los valores de parámetro de búfer actuales, utilice este método `MediaPlayer`:

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

   Si el AVE no puede establecer los valores especificados, el reproductor de medios introduce el estado `ERROR` con el código de error `SET_BUFFER_PARAMETERS_ERROR`.

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

Por ejemplo, para establecer el búfer inicial en 2 segundos y el tiempo de búfer de reproducción en 30 segundos:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(2000, 30000));
```

La implementación de referencia de Primetime muestra esta función; utilice la configuración de la aplicación para establecer los valores del búfer.