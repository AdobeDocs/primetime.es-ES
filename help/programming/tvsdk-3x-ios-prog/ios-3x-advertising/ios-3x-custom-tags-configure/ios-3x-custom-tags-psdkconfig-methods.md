---
description: Puede configurar los nombres de etiquetas personalizados en TVSDK globalmente con la clase PTSDKConfig.
title: Métodos de clase de configuración para etiquetas
exl-id: 017b766e-a6aa-4c14-af9a-2c88746e22c0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# Métodos de clase de configuración para etiquetas {#config-class-methods-for-tags}

Puede configurar los nombres de etiquetas personalizados en TVSDK globalmente con la clase PTSDKConfig.

TVSDK aplica la configuración global automáticamente a cualquier flujo de medios que no especifique una configuración específica del flujo.

`PTSDKConfig` expone estos métodos para administrar las etiquetas personalizadas:

| **Suscripción a etiquetas personalizadas específicas** |  |
|---|---|
| `subscribedTags` | Recupera la lista actual de etiquetas suscritas. |
| `setSubscribedTags` | Establece la lista de etiquetas suscritas que se expondrán a la aplicación. |
| **Personalizar las etiquetas de anuncio utilizadas por el detector de oportunidades predeterminado** |
| `adTags` | Recupera la lista actual de etiquetas de publicidad. |
| `setAdTags` | Establece la lista de etiquetas de publicidad que se utilizarán en el generador de oportunidades predeterminado. |


Recuerde lo siguiente:

* Los métodos del establecedor no permiten que el parámetro de etiquetas contenga valores nulos.
* El nombre de etiqueta personalizado debe contener el prefijo #.

   Por ejemplo, #EXT-X-ASSET es un nombre de etiqueta personalizado correcto, pero EXT-X-ASSET es incorrecto.
* No puede cambiar la configuración después de cargar el flujo de medios.
