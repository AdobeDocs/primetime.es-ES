---
description: Para ofrecer una experiencia de visualización más fluida, TVSDK almacena en el búfer a veces el flujo de vídeo. Puede configurar cómo se almacena el reproductor en el búfer.
seo-description: Para ofrecer una experiencia de visualización más fluida, TVSDK almacena en el búfer a veces el flujo de vídeo. Puede configurar cómo se almacena el reproductor en el búfer.
seo-title: Almacenamiento en búfer
title: Almacenamiento en búfer
uuid: c84b98ed-0070-4a86-a409-d7702e5be23c
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Información general {#buffering-overview}

Para ofrecer una experiencia de visualización más fluida, TVSDK almacena en el búfer a veces el flujo de vídeo. Puede configurar cómo se almacena el reproductor en el búfer.

TVSDK define una duración del búfer de reproducción de al menos 30 segundos y un tiempo de búfer inicial antes de que el medio empiece a reproducirse, de al menos 2 segundos. Después de las llamadas de la aplicación `play`, pero antes de que comience la reproducción, TVSDK almacena en búfer el medio hasta el momento inicial para proporcionar un inicio suave cuando realmente empieza a reproducirse.

Puede modificar los tiempos de búfer definiendo nuevas políticas de almacenamiento en búfer y puede alterar el momento en que se produce el almacenamiento en búfer inicial mediante el uso de activación instantánea.

## Políticas de tiempo de almacenamiento en búfer {#section_9B3407D52F1E4CB48E7A4836EBDA8F70}

Según el entorno (incluido el dispositivo, el sistema operativo o las condiciones de red), puede establecer distintas directivas de almacenamiento en búfer para el reproductor, como cambiar la duración mínima para el almacenamiento en búfer inicial y para el almacenamiento en búfer continuo de la reproducción.

Después de llamar `play`, el reproductor multimedia comienza a almacenar el vídeo en el búfer. Cuando el reproductor de medios almacena en búfer la cantidad de vídeo especificada por el tiempo de búfer inicial, la reproducción comienza. Este proceso mejora el tiempo de inicio porque el reproductor no espera a que se llene todo el búfer de reproducción antes de iniciar la reproducción. En su lugar, después de almacenar en búfer los pocos segundos iniciales, comienza la reproducción.

Mientras se procesa el vídeo, TVSDK continúa almacenando en búfer nuevos fragmentos hasta que se ha almacenado en el búfer la cantidad especificada por el tiempo de búfer de reproducción. Si la longitud del búfer actual cae por debajo del tiempo de búfer de reproducción, el reproductor descargará fragmentos adicionales. Una vez que la longitud del búfer actual está por encima del tiempo del búfer de reproducción en unos segundos, TVSDK dejará de descargar fragmentos.

>[!TIP]
>
>Si el valor del búfer inicial es alto, puede que le proporcione al usuario un tiempo de almacenamiento inicial prolongado antes de comenzar. Esto podría proporcionar una reproducción suave durante más tiempo; sin embargo, si las condiciones de red son deficientes, la reproducción inicial podría retrasarse.

Si activa el almacenamiento instantáneo llamando `prepareBuffer`, el almacenamiento en búfer inicial comienza en ese momento, en lugar de esperar `play`.

## Establecer horas de almacenamiento en búfer {#section_05CDD927869D47EBA1D2069B1416B2E4}

El `MediaPlayer` proporciona métodos para establecer y obtener el tiempo de almacenamiento en búfer inicial y el tiempo de almacenamiento en búfer de la reproducción.

>[!TIP]
>
>Si no establece los parámetros de control del búfer antes de iniciar la reproducción, el reproductor de medios toma el valor predeterminado de 2 segundos para el búfer inicial y 30 segundos para el tiempo de búfer de reproducción en curso.

1. Configure el `BufferControlParameters` objeto, que encapsula el tiempo de búfer inicial y los parámetros de control de tiempo del búfer de reproducción.

   Esta clase proporciona los siguientes métodos de fábrica:

   * Para establecer el tiempo de búfer inicial igual al tiempo de búfer de reproducción:

      ```
      public static BufferControlParameters createSimple(long bufferTime)
      ```

   * Para configurar los tiempos de búfer inicial y de reproducción:

      ```
      public static BufferControlParameters createDual( 
        long initialBuffer,  
        long bufferTime)
      ```
   Si los parámetros no son válidos, estos métodos se emiten `MediaPlayerException` con código de error `PSDKErrorCode.INVALID_ARGUMENT`, como cuando se cumplen las siguientes condiciones:

   * El tiempo de búfer inicial es menor que cero.
   * El tiempo de búfer inicial es bueno al tiempo de búfer.


1. Para establecer los valores de los parámetros de búfer, utilice este `MediaPlayer` método:

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. Para obtener los valores de parámetro de búfer actuales, utilice este `MediaPlayer` método:

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

<!--<a id="example_DE0580B3AD404635825D3301C1F096B6"></a>-->

Por ejemplo, para establecer el búfer inicial en 5 segundos y el tiempo del búfer de reproducción en 30 segundos:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(5000, 30000));
```
