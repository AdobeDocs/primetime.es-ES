---
description: Si el sistema tiene acceso a la descodificación asistida por hardware, puede lograr un juego de trucos más suave que con la implementación de TVSDK de software puro mediante el formato iFrame.
title: Operaciones de juego de trucos más suaves
exl-id: f69bf480-122b-474d-8f35-31655ea87c70
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Operaciones de juego de trucos más suaves {#smoother-trick-play-operations}

Si el sistema tiene acceso a la descodificación asistida por hardware, puede lograr un juego de trucos más suave que con la implementación de TVSDK de software puro mediante el formato iFrame.

<!--<a id="section_3DBFD7A3D1C7453096D3D3885E786263"></a>-->

El uso del formato iFrame da como resultado operaciones de reproducción engañosa que no son suaves. La operación de truco más suave utiliza un perfil normal (no de iFrame), soporte de descodificación de hardware y una velocidad de fotogramas aumentada. Los distintos dispositivos de descodificación asistida por hardware tienen diferentes capacidades. La velocidad doble requiere 60 fotogramas por segundo (FPS) y la velocidad cuádruple requiere 120 FPS.

>[!IMPORTANT]
>
>El Adobe recomienda limitar la reproducción a doble velocidad para los dispositivos Android más nuevos y no utilizar la función para los dispositivos Android más antiguos.

Para conseguir un juego de trucos más suave, establezca `ABRControlParameters.maxPlayoutRate` al múltiplo deseado de velocidad normal (por ejemplo, 2,0 para velocidad doble). Si hay una llamada posterior a `MediaPlayer.setRate()` tiene un argumento que es menor o igual que el valor establecido para `maxPlayoutRate`Sin embargo, TVSDK utiliza un perfil normal para lograr un juego de trucos más suave. De lo contrario, utiliza un perfil iFrame para la operación de juego de trucos.
