---
description: Puede elegir un punto de partida personalizado para cuándo introducir un flujo DVR en lugar del comportamiento predeterminado de introducir el flujo DVR al principio mediante la clase ConfigProvider.
seo-description: Puede elegir un punto de partida personalizado para cuándo introducir un flujo DVR en lugar del comportamiento predeterminado de introducir el flujo DVR al principio mediante la clase ConfigProvider.
seo-title: Elección de un punto de partida personalizado para DVR
title: Elección de un punto de partida personalizado para DVR
uuid: a7e13865-2b86-4234-ac4c-9a5320b293db
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# Selección de un punto de partida personalizado para DVR {#choosing-a-custom-starting-point-for-dvr}

Puede elegir un punto de partida personalizado para cuándo introducir un flujo DVR en lugar del comportamiento predeterminado de introducir el flujo DVR al principio mediante la clase ConfigProvider.

Para establecer el tiempo de inicio mediante la clase [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html):

1. Habilitar [isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled()).
1. Establezca la hora de inicio en [recuperaStartTimePref()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref()).
1. Compruebe que la posición del inicio personalizado está activada.
