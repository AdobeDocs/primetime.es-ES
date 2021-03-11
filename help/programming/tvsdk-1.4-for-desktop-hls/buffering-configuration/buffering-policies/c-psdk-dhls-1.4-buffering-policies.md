---
description: Para ofrecer una experiencia de visualización más fluida, TVSDK a veces almacena en el búfer el flujo de vídeo. Puede configurar el modo en que se almacena en el búfer el reproductor.
title: Políticas de tiempo de almacenamiento en búfer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---


# Políticas de tiempo de almacenamiento en búfer {#buffering-time-policies}

Para ofrecer una experiencia de visualización más fluida, TVSDK a veces almacena en el búfer el flujo de vídeo. Puede configurar el modo en que se almacena en el búfer el reproductor.

TVSDK define una duración del búfer de reproducción de al menos 30 segundos y un tiempo de búfer inicial dentro de él, antes de que el medio empiece a reproducirse, de al menos 5 segundos. Después de que la aplicación llama a `play` pero antes de que comience la reproducción, TVSDK almacena en búfer el contenido hasta el momento inicial para proporcionar un inicio suave cuando realmente comienza a reproducirse.

Puede modificar los tiempos de búfer definiendo nuevas políticas de almacenamiento en búfer.

<!--<a id="section_F6EEE15600814A70A57CCBACE20D68BD"></a>-->

Según el entorno (incluido el dispositivo, el sistema operativo o las condiciones de red), puede establecer distintas directivas de almacenamiento en búfer para el reproductor, como cambiar la duración mínima del almacenamiento en búfer inicial y del almacenamiento en búfer de reproducción continuo.

Después de llamar a `play`, el reproductor de contenidos comienza a almacenar en búfer el vídeo. Cuando el reproductor de contenido almacena en búfer la cantidad de vídeo especificada por el tiempo de búfer inicial, se inicia la reproducción. Este proceso mejora el tiempo de inicio porque el reproductor no espera a que se complete todo el búfer de reproducción antes de iniciar la reproducción. En su lugar, después de almacenar en búfer los pocos segundos iniciales, comienza la reproducción.

Mientras se representa el vídeo, TVSDK continúa almacenando en búfer nuevos fragmentos hasta que se ha almacenado en búfer la cantidad especificada por el tiempo de búfer de reproducción. Si la longitud del búfer actual cae por debajo del tiempo de búfer de reproducción, el reproductor descargará fragmentos adicionales. Una vez que la longitud del búfer actual supera el tiempo de búfer de reproducción en unos segundos, TVSDK dejará de descargar fragmentos.

>[!TIP]
>
>Si el valor del búfer inicial es alto, puede que le proporcione al usuario un tiempo de almacenamiento en búfer inicial largo antes de comenzar. Esto podría proporcionar una reproducción suave durante más tiempo; sin embargo, si las condiciones de red son deficientes, la reproducción inicial podría retrasarse.

