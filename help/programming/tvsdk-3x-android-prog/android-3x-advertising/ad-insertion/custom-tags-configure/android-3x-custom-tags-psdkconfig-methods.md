---
description: Puede configurar globalmente nombres de etiquetas personalizados en TVSDK con la clase MediaPlayerItemConfig.
title: Métodos de clase de configuración para etiquetas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Métodos de clase de configuración para etiquetas {#config-class-methods-for-tags}

Puede configurar globalmente nombres de etiquetas personalizados en TVSDK con la clase MediaPlayerItemConfig.

TVSDK aplica automáticamente la configuración global a cualquier flujo de medios que no especifique una configuración específica del flujo.

`MediaPlayerItemConfig` expone estos métodos para administrar las etiquetas personalizadas:

**Suscripción a etiquetas personalizadas específicas**

| <b>Método</b> | <b>Descripción</b> |
|--- |--- |
| `public final String[] getSubscribedTags` | Recupera la lista actual de etiquetas suscritas. |
| `public final void setSubscribedTags(String[] tags);` | Establece la lista de etiquetas suscritas que se expondrán a la aplicación.  Su aplicación también se suscribe automáticamente a todas las etiquetas transmitidas a través de `setAdTags`. |

**Personalizar las etiquetas de anuncio utilizadas por el detector de oportunidades predeterminado**

| <b>Método</b> | <b>Descripción</b> |
|--- |--- |
| `public final String[] getAdTags;` | Recupera la lista actual de etiquetas de publicidad. |
| `public final void setAdTags(String[] tags);` | Establece la lista de etiquetas de publicidad que se utilizarán en el generador de oportunidades predeterminado. |

Recuerde lo siguiente:

* Los métodos del establecedor no permiten que el parámetro de etiquetas contenga valores nulos.

  Si se encuentra, TVSDK genera un `IllegalArgumentException`.
* El nombre de etiqueta personalizado debe contener la variable `#` prefijo.

  Por ejemplo, `#EXT-X-ASSET` es un nombre de etiqueta personalizado correcto, pero `EXT-X-ASSET` es incorrecto.

* No puede cambiar la configuración después de cargar el flujo de medios.
