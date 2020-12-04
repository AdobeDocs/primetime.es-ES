---
description: Si su sistema tiene acceso a la descodificación asistida por hardware, puede lograr una reproducción de trucos más fluida que con la implementación de software TVSDK pura mediante el formato iFrame.
seo-description: Si su sistema tiene acceso a la descodificación asistida por hardware, puede lograr una reproducción de trucos más fluida que con la implementación de software TVSDK pura mediante el formato iFrame.
seo-title: Operaciones de reproducción de trucos más fluidas
title: Operaciones de reproducción de trucos más fluidas
uuid: 959d6c67-b64f-4666-8de7-54d247459fd1
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---


# Operaciones de reproducción de trucos más suaves {#smoother-trick-play-operations}

Si su sistema tiene acceso a la descodificación asistida por hardware, puede lograr una reproducción de trucos más fluida que con la implementación de software TVSDK pura mediante el formato iFrame.

<!--<a id="section_3DBFD7A3D1C7453096D3D3885E786263"></a>-->

El uso del formato iFrame produce operaciones de reproducción de trucos que no son suaves. Una operación de reproducción de trucos más fluida utiliza un perfil normal (no iFrame), compatibilidad con la descodificación de hardware y una velocidad de fotogramas mayor. Diferentes dispositivos de descodificación asistidos por hardware tienen diferentes capacidades. La velocidad de doble requiere 60 fotogramas por segundo (FPS) y la velocidad cuádruple requiere 120 FPS.

>[!IMPORTANT]
>
>Adobe recomienda limitar la reproducción a la velocidad de doble para dispositivos Android más nuevos y no utilizar la función para dispositivos Android más antiguos.

Para lograr una reproducción de trucos más suave, establezca `ABRControlParameters.maxPlayoutRate` en el múltiplo deseado de velocidad normal (por ejemplo, 2,0 para velocidad de doble). Si una llamada subsiguiente a `MediaPlayer.setRate()` tiene un argumento que es menor o igual al valor establecido para `maxPlayoutRate`, TVSDK utiliza un perfil normal para lograr una reproducción de trucos más fluida. En caso contrario, utiliza un perfil iFrame para la operación de reproducción de trucos.