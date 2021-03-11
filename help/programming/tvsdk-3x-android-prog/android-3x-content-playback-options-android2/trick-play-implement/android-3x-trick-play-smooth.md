---
description: Si su sistema tiene acceso a la descodificación asistida por hardware, puede lograr una reproducción más fluida que con la implementación del software TVSDK puro mediante el uso del formato iFrame.
title: Operaciones de reproducción de trucos más suaves
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# Operaciones de reproducción de trucos más suaves {#smoother-trick-play-operations}

Si su sistema tiene acceso a la descodificación asistida por hardware, puede lograr una reproducción más fluida que con la implementación del software TVSDK puro mediante el uso del formato iFrame.

<!--<a id="section_3DBFD7A3D1C7453096D3D3885E786263"></a>-->

El uso del formato iFrame da como resultado operaciones de reproducción de trucos que no son fluidas. La operación de reproducción mediante trucos más suave utiliza un perfil normal (no iFrame), compatibilidad con la descodificación de hardware y una velocidad de fotogramas más alta. Los distintos dispositivos de descodificación asistidos por hardware tienen diferentes capacidades. La velocidad doble requiere 60 fotogramas por segundo (FPS) y la velocidad cuádruple requiere 120 FPS.

>[!IMPORTANT]
>
>Adobe recomienda limitar la reproducción a la doble velocidad en los dispositivos Android más nuevos y no utilizar la función en los dispositivos Android más antiguos.

Para lograr una reproducción más suave, establezca `ABRControlParameters.maxPlayoutRate` en el múltiplo deseado de velocidad normal (por ejemplo, 2,0 para velocidad doble). Si una llamada subsiguiente a `MediaPlayer.setRate()` tiene un argumento menor o igual que el valor establecido para `maxPlayoutRate`, TVSDK utiliza un perfil normal para lograr una reproducción engañosa más suave. De lo contrario, utiliza un perfil iFrame para la operación de reproducción de trucos.