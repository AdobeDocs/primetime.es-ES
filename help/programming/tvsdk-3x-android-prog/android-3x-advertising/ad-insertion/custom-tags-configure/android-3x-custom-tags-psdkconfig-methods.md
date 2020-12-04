---
description: Puede configurar de forma global nombres de etiquetas personalizados en TVSDK con la clase MediaPlayerItemConfig.
seo-description: Puede configurar de forma global nombres de etiquetas personalizados en TVSDK con la clase MediaPlayerItemConfig.
seo-title: Métodos de clase Config para etiquetas
title: Métodos de clase Config para etiquetas
uuid: b75aebac-4b94-4c42-bed4-3c17ad989cd1
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Métodos de clase Config para etiquetas {#config-class-methods-for-tags}

Puede configurar de forma global nombres de etiquetas personalizados en TVSDK con la clase MediaPlayerItemConfig.

TVSDK aplica automáticamente la configuración global a cualquier flujo de medios que no especifique una configuración específica del flujo.

`MediaPlayerItemConfig` expone estos métodos para administrar las etiquetas personalizadas:

**Suscripción a etiquetas personalizadas específicas**

| <b>Método</b> | <b>Descripción</b> |
|--- |--- |
| `public final String[] getSubscribedTags` | Recupera la lista actual de las etiquetas suscritas. |
| `public final void setSubscribedTags(String[] tags);` | Establece la lista de las etiquetas suscritas que se expondrán a la aplicación.  La aplicación también se suscribe automáticamente a todas las etiquetas transmitidas a través de `setAdTags`. |

**Personalización de las etiquetas de publicidad utilizadas por el detector de oportunidades predeterminado**

| <b>Método</b> | <b>Descripción</b> |
|--- |--- |
| `public final String[] getAdTags;` | Recupera la lista actual de las etiquetas de publicidad. |
| `public final void setAdTags(String[] tags);` | Establece la lista de las etiquetas de publicidad que se utilizarán en el generador de oportunidades predeterminado. |

Recuerde lo siguiente:

* Los métodos setter no permiten que el parámetro tags contenga valores nulos.

   Si se encuentra, TVSDK emite un `IllegalArgumentException`.
* El nombre de etiqueta personalizado debe contener el prefijo `#`.

   Por ejemplo, `#EXT-X-ASSET` es un nombre de etiqueta personalizado correcto, pero `EXT-X-ASSET` es incorrecto.

* No puede cambiar la configuración después de cargar el flujo de medios.