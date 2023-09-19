---
description: Para proporcionar una experiencia de visualización más fluida, TVSDK a veces almacena en búfer el flujo de vídeo. Puede configurar la forma en que el reproductor se almacena en búfer.
title: Políticas de tiempo de almacenamiento en búfer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# Políticas de tiempo de almacenamiento en búfer {#buffering-time-policies}

Para proporcionar una experiencia de visualización más fluida, TVSDK a veces almacena en búfer el flujo de vídeo. Puede configurar la forma en que el reproductor se almacena en búfer.

TVSDK define una duración del búfer de reproducción de al menos 30 segundos y un tiempo de búfer inicial en ese intervalo de tiempo, antes de que el contenido comience a reproducirse, de al menos 5 segundos. Después de que la aplicación invoque `play` pero antes de que comience la reproducción, TVSDK almacena en búfer el contenido hasta el momento inicial para proporcionar un inicio sin problemas cuando comienza a reproducirse.

Puede modificar los tiempos del búfer definiendo nuevas directivas de almacenamiento en búfer.

<!--<a id="section_F6EEE15600814A70A57CCBACE20D68BD"></a>-->

Según el entorno (incluido el dispositivo, el sistema operativo o las condiciones de la red), puede establecer diferentes políticas de almacenamiento en búfer para el reproductor, como cambiar la duración mínima del almacenamiento en búfer inicial y del almacenamiento en búfer de reproducción continua.

Después de llamar a `play`, el reproductor multimedia comienza a almacenar el vídeo en búfer. Cuando el reproductor de contenidos ha almacenado en búfer la cantidad de vídeo especificada por el tiempo de almacenamiento en búfer inicial, comienza la reproducción. Este proceso mejora el tiempo de inicio, ya que el reproductor no espera a que se llene todo el búfer de reproducción antes de iniciar la reproducción. En su lugar, después de almacenar en búfer los segundos iniciales, comienza la reproducción.

Mientras se procesa el vídeo, TVSDK continúa almacenando en búfer nuevos fragmentos hasta que se almacena en búfer la cantidad especificada por el tiempo de búfer de reproducción. Si la longitud actual del búfer cae por debajo del tiempo del búfer de reproducción, el reproductor descargará fragmentos adicionales. Una vez que la longitud actual del búfer sea superior en unos segundos al tiempo de búfer de reproducción, TVSDK dejará de descargar fragmentos.

>[!TIP]
>
>Si el valor inicial del búfer es alto, puede proporcionar al usuario un tiempo de almacenamiento en búfer inicial largo antes de comenzar. Esto puede proporcionar una reproducción fluida durante más tiempo; sin embargo, si las condiciones de la red son deficientes, la reproducción inicial podría retrasarse.
