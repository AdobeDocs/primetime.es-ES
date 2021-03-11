---
description: Puede configurar nombres de etiquetas personalizados en TVSDK de forma global con la clase PTSDKConfig .
title: Métodos de clase Config para etiquetas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---


# Métodos de clase Config para etiquetas {#config-class-methods-for-tags}

Puede configurar nombres de etiquetas personalizados en TVSDK de forma global con la clase PTSDKConfig .

TVSDK aplica la configuración global automáticamente a cualquier flujo de medios que no especifique una configuración específica de flujo.

`PTSDKConfig` expone estos métodos para administrar las etiquetas personalizadas:

| **Suscripción a etiquetas personalizadas específicas** |  |
|---|---|
| `subscribedTags` | Recupera la lista actual de etiquetas suscritas. |
| `setSubscribedTags` | Establece la lista de etiquetas suscritas que se expondrán a la aplicación. |
| **Personalización de las etiquetas de publicidad utilizadas por el detector de oportunidades predeterminado** |
| `adTags` | Recupera la lista actual de etiquetas de publicidad. |
| `setAdTags` | Establece la lista de etiquetas de publicidad que utilizará el generador de oportunidades predeterminado. |


Recuerde lo siguiente:

* Los métodos de configuración no permiten que el parámetro de etiquetas contenga valores nulos.
* El nombre de etiqueta personalizado debe contener el prefijo # .

   Por ejemplo, #EXT-X-ASSET es un nombre de etiqueta personalizado correcto, pero EXT-X-ASSET es incorrecto.
* No puede cambiar la configuración después de cargar el flujo de medios.