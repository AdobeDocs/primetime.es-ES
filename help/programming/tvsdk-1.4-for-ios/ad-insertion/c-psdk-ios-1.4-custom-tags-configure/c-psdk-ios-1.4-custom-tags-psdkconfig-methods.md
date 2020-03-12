---
description: Puede configurar nombres de etiquetas personalizados en TVSDK de forma global con la clase PTSDKConfig.
seo-description: Puede configurar nombres de etiquetas personalizados en TVSDK de forma global con la clase PTSDKConfig.
seo-title: Métodos de clase Config para etiquetas
title: Métodos de clase Config para etiquetas
uuid: 1d3651a0-3b70-4d3a-8ced-663a9dad7205
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Métodos de clase Config para etiquetas{#config-class-methods-for-tags}

Puede configurar nombres de etiquetas personalizados en TVSDK de forma global con la clase PTSDKConfig.

TVSDK aplica la configuración global automáticamente a cualquier flujo de medios que no especifique una configuración específica del flujo.

`PTSDKConfig` expone estos métodos para administrar las etiquetas personalizadas:

| **Suscripción a etiquetas personalizadas específicas** |
|---|
| `subscribedTags` | Recupera la lista actual de etiquetas suscritas. |
| `setSubscribedTags` | Establece la lista de etiquetas suscritas que se expondrán a la aplicación. |
| **Personalización de las etiquetas de publicidad utilizadas por el detector de oportunidades predeterminado** |
| `adTags` | Recupera la lista actual de etiquetas de publicidad. |
| `setAdTags` | Establece la lista de etiquetas de publicidad que usará el generador de oportunidades predeterminado. |

Recuerde lo siguiente:

* Los métodos setter no permiten que el parámetro tags contenga valores nulos.
* El nombre de etiqueta personalizado debe contener el prefijo #.

   Por ejemplo, #EXT-X-ASSET es un nombre de etiqueta personalizado correcto, pero EXT-X-ASSET es incorrecto.
* No puede cambiar la configuración después de cargar el flujo de medios.

