---
description: Para ofrecer una experiencia de visualización más fluida, el SDK de TVSDK de navegador a veces almacena en el búfer el flujo de vídeo. Puede configurar el modo en que se almacena en el búfer el reproductor.
title: Almacenamiento en búfer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---


# Almacenamiento en búfer{#buffering}

Para ofrecer una experiencia de visualización más fluida, el SDK de TVSDK de navegador a veces almacena en el búfer el flujo de vídeo. Puede configurar el modo en que se almacena en el búfer el reproductor.

El TVSDK del explorador define una duración del búfer de reproducción de al menos 30 segundos y un tiempo de búfer inicial dentro de ese, antes de que el medio empiece a reproducirse, de al menos 2 segundos. Después de que la aplicación llama a `play` pero antes de que comience la reproducción, el SDK de TVSDK del explorador almacena en búfer el contenido hasta el momento inicial para proporcionar un inicio suave cuando realmente comienza a reproducirse.

## Establecer tiempos de almacenamiento en búfer {#section_179DA7CA865D48EBA4B03D50B6B7BC50}

MediaPlayer proporciona métodos para establecer y obtener el tiempo de almacenamiento en búfer inicial y el tiempo de almacenamiento en búfer de reproducción.

>[!TIP]
>
>Si no establece los parámetros de control de búfer antes de comenzar la reproducción, el reproductor de medios toma como valor predeterminado 2 segundos para el búfer inicial y 30 segundos para el tiempo de búfer de reproducción en curso.

* Para utilizar los parámetros de búfer, utilice el atributo `bufferControlParameters` de MediaPlayer.

   Por ejemplo, para establecer el búfer inicial en 2 segundos y el tiempo de búfer de reproducción en 30 segundos:

   ```js
   var params = new AdobePSDK.BufferControlParameters(2000, 30000);
   ```

## Políticas de tiempo de almacenamiento en búfer {#section_7EF2947931654CCC8DAB9172391FA4EB}

Según el entorno (incluido el dispositivo, el sistema operativo o las condiciones de red), puede establecer distintas directivas de almacenamiento en búfer para el reproductor, como cambiar la duración mínima del almacenamiento en búfer inicial y del almacenamiento en búfer de reproducción continuo.

Después de llamar a `play`, el reproductor de contenidos comienza a almacenar en búfer el vídeo. Cuando el reproductor de contenido almacena en búfer la cantidad de vídeo especificada por el tiempo de búfer inicial, se inicia la reproducción. Este proceso mejora el tiempo de inicio porque el reproductor no espera a que se complete todo el búfer de reproducción antes de iniciar la reproducción. En su lugar, después de almacenar en búfer los pocos segundos iniciales, comienza la reproducción.

Mientras se procesa el vídeo, el SDK de TVSDK del explorador continúa almacenando en el búfer nuevos fragmentos hasta que se ha almacenado en el búfer la cantidad especificada por el tiempo de búfer de reproducción. Si la longitud del búfer actual cae por debajo del tiempo de búfer de reproducción, el reproductor descargará fragmentos adicionales. Una vez que la longitud del búfer actual supera el tiempo de búfer de reproducción en unos segundos, el TVSDK del explorador dejará de descargar fragmentos.

>[!TIP]
>
>Si el valor del búfer inicial es alto, puede que le proporcione al usuario un tiempo de almacenamiento en búfer inicial largo antes de comenzar. Esto podría proporcionar una reproducción suave durante más tiempo; sin embargo, si las condiciones de red son deficientes, la reproducción inicial podría retrasarse.

