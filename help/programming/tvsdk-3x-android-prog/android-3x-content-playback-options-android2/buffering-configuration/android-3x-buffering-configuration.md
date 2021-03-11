---
description: Para ofrecer una experiencia de visualización más fluida, TVSDK a veces almacena en el búfer el flujo de vídeo. Puede configurar el modo en que se almacena en búfer el reproductor.
title: Almacenamiento en búfer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---


# Información general {#buffering-overview}

Para ofrecer una experiencia de visualización más fluida, TVSDK a veces almacena en el búfer el flujo de vídeo. Puede configurar el modo en que se almacena en búfer el reproductor.

TVSDK define una duración del búfer de reproducción de al menos 30 segundos y un tiempo de búfer inicial antes de que se inicie la reproducción del contenido, de al menos 2 segundos. Después de que la aplicación llama a `play`, pero antes de que comience la reproducción, TVSDK almacena en búfer el contenido hasta el momento inicial para proporcionar un inicio suave cuando realmente comienza a reproducirse.

Puede modificar los tiempos de búfer definiendo nuevas políticas de almacenamiento en búfer y puede modificar cuando se produzca el almacenamiento en búfer inicial al utilizar la opción de activación instantánea.

## Políticas de tiempo de almacenamiento en búfer {#section_9B3407D52F1E4CB48E7A4836EBDA8F70}

Según el entorno (incluido el dispositivo, el sistema operativo o las condiciones de red), puede establecer distintas directivas de almacenamiento en búfer para el reproductor, como cambiar la duración mínima del almacenamiento en búfer inicial y del almacenamiento en búfer de reproducción continuo.

Después de llamar a `play`, el reproductor de contenidos comienza a almacenar en búfer el vídeo. Cuando el reproductor de contenido almacena en búfer la cantidad de vídeo especificada por el tiempo de búfer inicial, se inicia la reproducción. Este proceso mejora el tiempo de inicio porque el reproductor no espera a que se complete todo el búfer de reproducción antes de iniciar la reproducción. En su lugar, después de almacenar en búfer los pocos segundos iniciales, comienza la reproducción.

Mientras se representa el vídeo, TVSDK continúa almacenando en búfer nuevos fragmentos hasta que se ha almacenado en búfer la cantidad especificada por el tiempo de búfer de reproducción. Si la longitud del búfer actual cae por debajo del tiempo de búfer de reproducción, el reproductor descargará fragmentos adicionales. Una vez que la longitud del búfer actual supera el tiempo de búfer de reproducción en unos segundos, TVSDK dejará de descargar fragmentos.

>[!TIP]
>
>Si el valor del búfer inicial es alto, puede que le proporcione al usuario un tiempo de almacenamiento en búfer inicial largo antes de comenzar. Esto podría proporcionar una reproducción suave durante más tiempo; sin embargo, si las condiciones de red son deficientes, la reproducción inicial podría retrasarse.

Si activa instantáneamente llamando a `prepareBuffer`, el almacenamiento en búfer inicial comienza en ese momento, en lugar de esperar a `play`.

## Establecer tiempos de almacenamiento en búfer {#section_05CDD927869D47EBA1D2069B1416B2E4}

El `MediaPlayer` proporciona métodos para establecer y obtener el tiempo de almacenamiento en búfer inicial y el tiempo de almacenamiento en búfer de reproducción.

>[!TIP]
>
>Si no establece los parámetros de control de búfer antes de comenzar la reproducción, el reproductor de medios toma como valor predeterminado 2 segundos para el búfer inicial y 30 segundos para el tiempo de búfer de reproducción en curso.

1. Configure el objeto `BufferControlParameters`, que encapsula el tiempo de búfer inicial y los parámetros de control de tiempo del búfer de reproducción.

   Esta clase proporciona los siguientes métodos de fábrica:

   * Para establecer el tiempo de búfer inicial igual al tiempo de búfer de reproducción:

      ```
      public static BufferControlParameters createSimple(long bufferTime)
      ```

   * Para establecer los tiempos de búfer inicial y de reproducción:

      ```
      public static BufferControlParameters createDual( 
        long initialBuffer,  
        long bufferTime)
      ```
   Si los parámetros no son válidos, estos métodos arrojan `MediaPlayerException` con el código de error `PSDKErrorCode.INVALID_ARGUMENT`, como cuando se cumplen las siguientes condiciones:

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

<!--<a id="example_DE0580B3AD404635825D3301C1F096B6"></a>-->

Por ejemplo, para establecer el búfer inicial en 5 segundos y el tiempo de búfer de reproducción en 30 segundos:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(5000, 30000));
```
