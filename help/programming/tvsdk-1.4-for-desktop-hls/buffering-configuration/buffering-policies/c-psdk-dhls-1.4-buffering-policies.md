---
description: Para ofrecer una experiencia de visualización más fluida, TVSDK almacena en el búfer a veces el flujo de vídeo. Puede configurar la forma en que el reproductor se almacena en el búfer.
seo-description: Para ofrecer una experiencia de visualización más fluida, TVSDK almacena en el búfer a veces el flujo de vídeo. Puede configurar la forma en que el reproductor se almacena en el búfer.
seo-title: Políticas de tiempo de almacenamiento en búfer
title: Políticas de tiempo de almacenamiento en búfer
uuid: 8d3ce9be-cca4-485e-ba66-d2f2aa6822dd
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Políticas de tiempo de almacenamiento en búfer {#buffering-time-policies}

Para ofrecer una experiencia de visualización más fluida, TVSDK almacena en el búfer a veces el flujo de vídeo. Puede configurar la forma en que el reproductor se almacena en el búfer.

TVSDK define una duración del búfer de reproducción de al menos 30 segundos y un tiempo de búfer inicial dentro de él, antes de que el medio empiece a reproducirse, de al menos 5 segundos. Después de que la aplicación llama `play` pero antes de que comience la reproducción, TVSDK almacena en búfer el medio hasta el momento inicial para proporcionar un inicio suave cuando realmente comienza a reproducirse.

Puede modificar los tiempos de búfer definiendo nuevas políticas de almacenamiento en búfer.

<!--<a id="section_F6EEE15600814A70A57CCBACE20D68BD"></a>-->

Según el entorno (incluido el dispositivo, el sistema operativo o las condiciones de red), puede establecer distintas directivas de almacenamiento en búfer para el reproductor, como cambiar la duración mínima para el almacenamiento en búfer inicial y para el almacenamiento en búfer continuo de la reproducción.

Después de llamar `play`, el reproductor multimedia comienza a almacenar el vídeo en el búfer. Cuando el reproductor de medios almacena en búfer la cantidad de vídeo especificada por el tiempo de búfer inicial, la reproducción comienza. Este proceso mejora el tiempo de inicio porque el reproductor no espera a que se llene todo el búfer de reproducción antes de iniciar la reproducción. En su lugar, después de almacenar en búfer los pocos segundos iniciales, comienza la reproducción.

Mientras se procesa el vídeo, TVSDK continúa almacenando en búfer nuevos fragmentos hasta que se ha almacenado en el búfer la cantidad especificada por el tiempo de búfer de reproducción. Si la longitud del búfer actual cae por debajo del tiempo de búfer de reproducción, el reproductor descargará fragmentos adicionales. Una vez que la longitud del búfer actual está por encima del tiempo del búfer de reproducción en unos segundos, TVSDK dejará de descargar fragmentos.

>[!TIP]
>
>Si el valor del búfer inicial es alto, puede que le proporcione al usuario un tiempo de almacenamiento inicial prolongado antes de comenzar. Esto podría proporcionar una reproducción suave durante más tiempo; sin embargo, si las condiciones de red son deficientes, la reproducción inicial podría retrasarse.

