---
description: Para ofrecer una experiencia de visualización más fluida, el SDK de TVSDK del explorador almacena en búfer en ocasiones el flujo de vídeo. Puede configurar la forma en que el reproductor se almacena en el búfer.
seo-description: Para ofrecer una experiencia de visualización más fluida, el SDK de TVSDK del explorador almacena en búfer en ocasiones el flujo de vídeo. Puede configurar la forma en que el reproductor se almacena en el búfer.
seo-title: Almacenamiento en búfer
title: Almacenamiento en búfer
uuid: 9937731d-013e-41e9-a4c9-f7a54a5e654d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Almacenamiento en búfer{#buffering}

Para ofrecer una experiencia de visualización más fluida, el SDK de TVSDK del explorador almacena en búfer en ocasiones el flujo de vídeo. Puede configurar la forma en que el reproductor se almacena en el búfer.

El SDK TVSDK del explorador define una duración del búfer de reproducción de al menos 30 segundos y un tiempo de búfer inicial dentro de él, antes de que el medio empiece a reproducirse, de al menos 2 segundos. Después de que la aplicación llama `play` pero antes de que comience la reproducción, el SDK TVSDK del explorador almacena en búfer el medio hasta el momento inicial para proporcionar un inicio suave cuando realmente comienza a reproducirse.

## Establecer horas de almacenamiento en búfer {#section_179DA7CA865D48EBA4B03D50B6B7BC50}

MediaPlayer proporciona métodos para establecer y obtener el tiempo de almacenamiento en búfer inicial y el tiempo de almacenamiento en búfer de reproducción.

>[!TIP]
>
>Si no establece los parámetros de control del búfer antes de iniciar la reproducción, el reproductor de medios toma el valor predeterminado de 2 segundos para el búfer inicial y 30 segundos para el tiempo de búfer de reproducción en curso.

* Para utilizar los parámetros de búfer, utilice el atributo `bufferControlParameters` de MediaPlayer.

   Por ejemplo, para establecer el búfer inicial en 2 segundos y el tiempo del búfer de reproducción en 30 segundos:

   ```js
   var params = new AdobePSDK.BufferControlParameters(2000, 30000);
   ```

## Políticas de tiempo de almacenamiento en búfer {#section_7EF2947931654CCC8DAB9172391FA4EB}

Según el entorno (incluido el dispositivo, el sistema operativo o las condiciones de red), puede establecer distintas directivas de almacenamiento en búfer para el reproductor, como cambiar la duración mínima para el almacenamiento en búfer inicial y para el almacenamiento en búfer continuo de la reproducción.

Después de llamar `play`, el reproductor multimedia comienza a almacenar el vídeo en el búfer. Cuando el reproductor de medios almacena en búfer la cantidad de vídeo especificada por el tiempo de búfer inicial, la reproducción comienza. Este proceso mejora el tiempo de inicio porque el reproductor no espera a que se llene todo el búfer de reproducción antes de iniciar la reproducción. En su lugar, después de almacenar en búfer los pocos segundos iniciales, comienza la reproducción.

Mientras se procesa el vídeo, el SDK de TVSDK del explorador continúa almacenando en búfer nuevos fragmentos hasta que se ha almacenado en el búfer la cantidad especificada por el tiempo de búfer de reproducción. Si la longitud del búfer actual cae por debajo del tiempo de búfer de reproducción, el reproductor descargará fragmentos adicionales. Una vez que la longitud del búfer actual está por encima del tiempo del búfer de reproducción en unos segundos, el TVSDK del explorador dejará de descargar fragmentos.

>[!TIP]
>
>Si el valor del búfer inicial es alto, puede que le proporcione al usuario un tiempo de almacenamiento inicial prolongado antes de comenzar. Esto podría proporcionar una reproducción suave durante más tiempo; sin embargo, si las condiciones de red son deficientes, la reproducción inicial podría retrasarse.

