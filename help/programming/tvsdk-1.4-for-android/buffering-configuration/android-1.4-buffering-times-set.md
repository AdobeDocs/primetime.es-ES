---
description: Para ofrecer una experiencia de visualización más fluida, TVSDK almacena en el búfer a veces el flujo de vídeo. Puede configurar la forma en que el reproductor se almacena en el búfer.
seo-description: Para ofrecer una experiencia de visualización más fluida, TVSDK almacena en el búfer a veces el flujo de vídeo. Puede configurar la forma en que el reproductor se almacena en el búfer.
seo-title: Establecer horas de almacenamiento en búfer
title: Establecer horas de almacenamiento en búfer
uuid: 5a3945a4-1935-4797-b19d-84989850a487
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# Almacenamiento en búfer {#buffering}

Para ofrecer una experiencia de visualización más fluida, TVSDK almacena en el búfer a veces el flujo de vídeo. Puede configurar la forma en que el reproductor se almacena en el búfer.

TVSDK define una duración del búfer de reproducción de al menos 30 segundos y un tiempo de búfer inicial dentro de ese tiempo, antes de que se reproduzcan los inicios de medios, de al menos 2 segundos. Después de que la aplicación llama a `play` pero antes de que comience la reproducción, TVSDK almacena en búfer el medio hasta el momento inicial para proporcionar un inicio suave cuando realmente inicio la reproducción.

Puede modificar los tiempos de búfer definiendo nuevas políticas de almacenamiento en búfer y puede alterar el momento en que se produce el almacenamiento en búfer inicial mediante el uso de la función instantánea.

## Establecer tiempos de almacenamiento en búfer {#set-buffering-times}

El `MediaPlayer` proporciona métodos para establecer y obtener el tiempo de almacenamiento en búfer inicial y el tiempo de almacenamiento en búfer de la reproducción.

>[!TIP]
>
>Si no establece los parámetros de control del búfer antes de iniciar la reproducción, el reproductor de medios toma el valor predeterminado de 2 segundos para el búfer inicial y 30 segundos para el tiempo de búfer de reproducción en curso.

1. Configure el objeto `BufferControlParameters`, que encapsula el tiempo de búfer inicial y los parámetros de control de tiempo del búfer de reproducción:

       Esta clase proporciona dos métodos de fábrica:
   
   * Para establecer el tiempo de búfer inicial igual al tiempo de búfer de reproducción:

      ```java
      public static BufferControlParameters createSimple( 
          long bufferTime)
      ```

   * Para configurar los tiempos de búfer inicial y de reproducción:

      ```java
      public static BufferControlParameters createDual( 
          long initialBuffer,   
          long bufferTime)
      ```

      Estos métodos generan un `IllegalArgumentException` si los parámetros no son válidos, como cuando:

   * El tiempo de búfer inicial es menor que cero.
   * El tiempo de búfer inicial es bueno al tiempo de búfer.

1. Para establecer los valores de los parámetros del búfer, utilice este método `MediaPlayer`:

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. Para obtener los valores de parámetro de búfer actuales, utilice este método `MediaPlayer`:

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

   Si el AVE no puede establecer los valores especificados, el reproductor multimedia introduce el estado `ERROR` con el código de error `SET_BUFFER_PARAMETERS_ERROR`.

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

Por ejemplo, para establecer el búfer inicial en 2 segundos y el tiempo del búfer de reproducción en 30 segundos:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(2000, 30000));
```

La implementación de referencia de Primetime demuestra esta función; utilice la configuración de la aplicación para establecer los valores del búfer.