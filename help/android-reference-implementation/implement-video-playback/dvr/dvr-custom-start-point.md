---
description: Puede elegir un punto de partida personalizado para cuándo entrar en un flujo de DVR en lugar del comportamiento predeterminado de entrar en el flujo de DVR al principio mediante la clase ConfigProvider.
title: Elegir un punto de partida personalizado para DVR
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# Elegir un punto de partida personalizado para DVR {#choosing-a-custom-starting-point-for-dvr}

Puede elegir un punto de partida personalizado para cuándo entrar en un flujo de DVR en lugar del comportamiento predeterminado de entrar en el flujo de DVR al principio mediante la clase ConfigProvider.

Para establecer la hora de inicio a través de [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) clase:

1. Activar [isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled()).
1. Establecer la hora de inicio en [retrieveStartTimePref()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref()).
1. Compruebe que la posición de inicio personalizada esté habilitada.
