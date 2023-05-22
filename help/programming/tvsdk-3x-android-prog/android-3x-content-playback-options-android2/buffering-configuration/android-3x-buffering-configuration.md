---
description: Para proporcionar una experiencia de visualización más fluida, TVSDK a veces almacena en búfer el flujo de vídeo. Puede configurar el modo en que el reproductor se almacena en búfer.
title: Almacenamiento en búfer
exl-id: 3b706420-878d-487a-8db7-cff2a12c2660
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# Información general {#buffering-overview}

Para proporcionar una experiencia de visualización más fluida, TVSDK a veces almacena en búfer el flujo de vídeo. Puede configurar el modo en que el reproductor se almacena en búfer.

TVSDK define una duración del búfer de reproducción de al menos 30 segundos y un tiempo de búfer inicial de al menos 2 segundos antes de que comience la reproducción del contenido. Después de que la aplicación invoque `play`, pero antes de que comience la reproducción, TVSDK almacena en búfer el contenido hasta el momento inicial para proporcionar un inicio sin problemas cuando comienza a reproducirse.

Puede modificar los tiempos de almacenamiento en búfer mediante la definición de nuevas directivas de almacenamiento en búfer y puede modificar cuándo se produce el almacenamiento en búfer inicial mediante el uso instantáneo de.

## Políticas de tiempo de almacenamiento en búfer {#section_9B3407D52F1E4CB48E7A4836EBDA8F70}

Según el entorno (incluido el dispositivo, el sistema operativo o las condiciones de la red), puede establecer diferentes políticas de almacenamiento en búfer para el reproductor, como cambiar la duración mínima del almacenamiento en búfer inicial y del almacenamiento en búfer de reproducción continua.

Después de llamar a `play`, el reproductor multimedia comienza a almacenar el vídeo en búfer. Cuando el reproductor de contenidos ha almacenado en búfer la cantidad de vídeo especificada por el tiempo de almacenamiento en búfer inicial, comienza la reproducción. Este proceso mejora el tiempo de inicio, ya que el reproductor no espera a que se llene todo el búfer de reproducción antes de iniciar la reproducción. En su lugar, después de almacenar en búfer los segundos iniciales, comienza la reproducción.

Mientras se procesa el vídeo, TVSDK continúa almacenando en búfer nuevos fragmentos hasta que se almacena en búfer la cantidad especificada por el tiempo de búfer de reproducción. Si la longitud actual del búfer cae por debajo del tiempo del búfer de reproducción, el reproductor descargará fragmentos adicionales. Una vez que la longitud actual del búfer sea superior en unos segundos al tiempo de búfer de reproducción, TVSDK dejará de descargar fragmentos.

>[!TIP]
>
>Si el valor inicial del búfer es alto, puede proporcionar al usuario un tiempo de almacenamiento en búfer inicial largo antes de comenzar. Esto puede proporcionar una reproducción fluida durante más tiempo; sin embargo, si las condiciones de la red son deficientes, la reproducción inicial podría retrasarse.

Si habilita el encendido instantáneo llamando a `prepareBuffer`, el almacenamiento en búfer inicial comienza en ese momento, en lugar de esperar a `play`.

## Establecer tiempos de almacenamiento en búfer {#section_05CDD927869D47EBA1D2069B1416B2E4}

El `MediaPlayer` proporciona métodos para establecer y obtener el tiempo de almacenamiento en búfer inicial y el tiempo de almacenamiento en búfer de reproducción.

>[!TIP]
>
>Si no define los parámetros de control del búfer antes de comenzar la reproducción, el reproductor de contenido toma como valor predeterminado 2 segundos para el búfer inicial y 30 segundos para el tiempo de búfer de reproducción en curso.

1. Configure las variables `BufferControlParameters` , que encapsula los parámetros iniciales de control de tiempo del búfer de reproducción y tiempo del búfer de reproducción.

   Esta clase proporciona los siguientes métodos de fábrica:

   * Para establecer el tiempo de búfer inicial igual al tiempo de búfer de reproducción:

      ```
      public static BufferControlParameters createSimple(long bufferTime)
      ```

   * Para definir los tiempos iniciales y de búfer de reproducción:

      ```
      public static BufferControlParameters createDual( 
        long initialBuffer,  
        long bufferTime)
      ```
   Si los parámetros no son válidos, estos métodos activan `MediaPlayerException` con código de error `PSDKErrorCode.INVALID_ARGUMENT`, como cuando se cumplen las siguientes condiciones:

   * El tiempo de búfer inicial es inferior a cero.
   * El tiempo de búfer inicial es bueno que el tiempo de búfer.


1. Para definir los valores de los parámetros de búfer, utilice esta opción `MediaPlayer` método:

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. Para obtener los valores actuales de los parámetros de búfer, utilice esta opción `MediaPlayer` método:

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

<!--<a id="example_DE0580B3AD404635825D3301C1F096B6"></a>-->

Por ejemplo, para establecer el búfer inicial en 5 segundos y el tiempo de búfer de reproducción en 30 segundos:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(5000, 30000));
```
