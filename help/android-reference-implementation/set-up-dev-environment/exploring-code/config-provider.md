---
description: La clase ConfigProvider obtiene la configuración del reproductor de medios. Debe implementar la interfaz de configuración para que los administradores de características puedan leer la información de configuración.
title: ConfigProvider
exl-id: 75613bfb-3c2b-4b53-b365-adc98f7e1164
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# ConfigProvider {#configprovider}

La clase ConfigProvider obtiene la configuración del reproductor de medios. Debe implementar la interfaz de configuración para que los administradores de características puedan leer la información de configuración.

Utilice el [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) para implementar el `ICCConfig`, `IAAConfig`, `IPlaybackConfig`, `IAdConfig`, y `IQosConfig` interfaces de configuración para que los administradores de funciones puedan leer las configuraciones. Por ejemplo, la variable `ICCConfig` es la interfaz de `CCManager` configuración. Los archivos de configuración reciben los parámetros de configuración del archivo de configuración JSON.

El `ConfigProvider.java` es un ejemplo de la implementación por parte de Adobe de las interfaces de configuración. Lee la configuración de `SharedPreferences`, donde se almacena la configuración. Puede almacenar la configuración de cualquier forma que funcione para su organización. La implementación de configuración proporciona un contenedor para el origen de la configuración.
