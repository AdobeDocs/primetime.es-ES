---
description: La clase ConfigProvider obtiene la configuración del reproductor multimedia. Debe implementar la interfaz de configuración para que los administradores de funciones puedan leer la información de configuración.
seo-description: La clase ConfigProvider obtiene la configuración del reproductor multimedia. Debe implementar la interfaz de configuración para que los administradores de funciones puedan leer la información de configuración.
seo-title: ConfigProvider
title: ConfigProvider
uuid: 2467a617-6413-4b5d-9710-894cdc751b26
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# ConfigProvider {#configprovider}

La clase ConfigProvider obtiene la configuración del reproductor multimedia. Debe implementar la interfaz de configuración para que los administradores de funciones puedan leer la información de configuración.

La clase [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) se utiliza para implementar las interfaces de configuración `ICCConfig`, `IAAConfig`, `IPlaybackConfig`, `IAdConfig` y `IQosConfig` de modo que los administradores de funciones puedan leer las configuraciones. Por ejemplo, `ICCConfig` es la interfaz para la configuración `CCManager`. Los archivos de configuración reciben los parámetros de configuración del archivo de configuración JSON.

El archivo `ConfigProvider.java` es un ejemplo de la implementación por parte del Adobe de las interfaces de configuración. Lee la configuración desde `SharedPreferences`, donde se almacena la configuración. Puede almacenar la configuración de cualquier manera que funcione para su organización. La implementación de configuración proporciona un envoltorio para el origen de configuración.