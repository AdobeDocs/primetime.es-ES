---
description: Puede elegir un punto de partida personalizado para el momento en que se debe introducir un flujo DVR en lugar del comportamiento predeterminado de entrar en el flujo DVR al principio con la clase ConfigProvider.
title: Elección de un punto de partida personalizado para DVR
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# Elección de un punto de partida personalizado para DVR {#choosing-a-custom-starting-point-for-dvr}

Puede elegir un punto de partida personalizado para el momento en que se debe introducir un flujo DVR en lugar del comportamiento predeterminado de entrar en el flujo DVR al principio con la clase ConfigProvider.

Para establecer la hora de inicio mediante la clase [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html):

1. Habilitar [isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled()).
1. Establezca la hora de inicio en [retrieveStartTimePref()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref()).
1. Compruebe que la posición de inicio personalizada esté habilitada.
