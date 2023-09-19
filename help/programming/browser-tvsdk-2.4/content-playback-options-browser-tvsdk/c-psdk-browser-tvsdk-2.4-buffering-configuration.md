---
description: Para proporcionar una experiencia de visualización más fluida, el TVSDK del explorador a veces almacena en búfer el flujo de vídeo. Puede configurar la forma en que el reproductor se almacena en búfer.
title: Almacenamiento en búfer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Almacenamiento en búfer{#buffering}

Para proporcionar una experiencia de visualización más fluida, el TVSDK del explorador a veces almacena en búfer el flujo de vídeo. Puede configurar la forma en que el reproductor se almacena en búfer.

Browser TVSDK define una duración del búfer de reproducción de al menos 30 segundos y un tiempo de búfer inicial de al menos 2 segundos antes de que el contenido comience a reproducirse. Después de que la aplicación invoque `play` pero antes de que comience la reproducción, el TVSDK del explorador almacena en búfer el contenido hasta el momento inicial para proporcionar un inicio sin problemas cuando realmente comienza a reproducirse.

## Establecer tiempos de almacenamiento en búfer {#section_179DA7CA865D48EBA4B03D50B6B7BC50}

MediaPlayer proporciona métodos para establecer y obtener el tiempo de almacenamiento en búfer inicial y el tiempo de almacenamiento en búfer de reproducción.

>[!TIP]
>
>Si no define los parámetros de control del búfer antes de comenzar la reproducción, el reproductor de contenido toma como valor predeterminado 2 segundos para el búfer inicial y 30 segundos para el tiempo de búfer de reproducción en curso.

* Para utilizar los parámetros de búfer, utilice el `bufferControlParameters` atributo.

  Por ejemplo, para establecer el búfer inicial en 2 segundos y el tiempo de búfer de reproducción en 30 segundos:

  ```js
  var params = new AdobePSDK.BufferControlParameters(2000, 30000);
  ```

## Políticas de tiempo de almacenamiento en búfer {#section_7EF2947931654CCC8DAB9172391FA4EB}

Según el entorno (incluido el dispositivo, el sistema operativo o las condiciones de la red), puede establecer diferentes políticas de almacenamiento en búfer para el reproductor, como cambiar la duración mínima del almacenamiento en búfer inicial y del almacenamiento en búfer de reproducción continua.

Después de llamar a `play`, el reproductor multimedia comienza a almacenar el vídeo en búfer. Cuando el reproductor de contenidos ha almacenado en búfer la cantidad de vídeo especificada por el tiempo de almacenamiento en búfer inicial, comienza la reproducción. Este proceso mejora el tiempo de inicio, ya que el reproductor no espera a que se llene todo el búfer de reproducción antes de iniciar la reproducción. En su lugar, después de almacenar en búfer los segundos iniciales, comienza la reproducción.

Mientras se procesa el vídeo, el TVSDK del explorador continúa almacenando en búfer nuevos fragmentos hasta que se almacena en búfer la cantidad especificada por el tiempo de búfer de reproducción. Si la longitud actual del búfer cae por debajo del tiempo del búfer de reproducción, el reproductor descargará fragmentos adicionales. Una vez que la longitud actual del búfer sea superior en unos segundos al tiempo de búfer de reproducción, el TVSDK del explorador detendrá la descarga de fragmentos.

>[!TIP]
>
>Si el valor inicial del búfer es alto, puede proporcionar al usuario un tiempo de almacenamiento en búfer inicial largo antes de comenzar. Esto puede proporcionar una reproducción fluida durante más tiempo; sin embargo, si las condiciones de la red son deficientes, la reproducción inicial podría retrasarse.
