---
description: Puede elegir un punto de partida personalizado para cuándo entrar en un flujo de DVR en lugar del comportamiento predeterminado de entrar en el flujo de DVR al principio mediante la clase ConfigProvider.
title: Elegir un punto de partida personalizado para DVR
exl-id: 9813bf60-a91d-4376-a5fe-02311b73e8a0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
