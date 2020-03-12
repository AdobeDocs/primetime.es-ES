---
description: Puede marcar, eliminar y reemplazar intervalos de tiempo en flujos de VOD mediante diferentes modos de señalización de publicidad y combinaciones de metadatos de anuncio. Diferentes combinaciones de modo de señalización y metadatos dan como resultado comportamientos diferentes.
seo-description: Puede marcar, eliminar y reemplazar intervalos de tiempo en flujos de VOD mediante diferentes modos de señalización de publicidad y combinaciones de metadatos de anuncio. Diferentes combinaciones de modo de señalización y metadatos dan como resultado comportamientos diferentes.
seo-title: Efecto en la inserción y eliminación de publicidades en el modo de señalización de anuncios y en las combinaciones de metadatos de anuncios
title: Efecto en la inserción y eliminación de publicidades en el modo de señalización de anuncios y en las combinaciones de metadatos de anuncios
uuid: 49abab49-4e52-477d-b7ed-688ee63e7473
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Efecto en la inserción y eliminación de publicidades en el modo de señalización de anuncios y en las combinaciones de metadatos de anuncios {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Puede marcar, eliminar y reemplazar intervalos de tiempo en flujos de VOD mediante diferentes modos de señalización de publicidad y combinaciones de metadatos de anuncio. Diferentes combinaciones de modo de señalización y metadatos dan como resultado comportamientos diferentes.

>[!TIP]
>
>Cuando hay un conflicto entre los intervalos de tiempo y los modos de señalización de publicidad, TVSDK da prioridad a los intervalos de tiempo.

La tabla siguiente proporciona los detalles sobre el modo de señalización y los comportamientos de combinación de metadatos:

**Mapa del servidor**

| **Metadatos de anuncio** | **Resoluciones creadas** | **`PlacementInformations`creado ** | **Comportamiento resultante** |
|--- |--- |--- |--- |
|  | Eliminar | Eliminar | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Rangos eliminados |
| Eliminar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),` <br>`PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Rangos eliminados, publicidades insertadas |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Publicidades insertadas |
| Reemplazar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Rangos reemplazados |
| Marcar | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Marcar, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados, sin anuncios insertados |

**Señales de manifiesto**

| Metadatos de anuncio | Resoluciones creadas | `PlacementInformations` creado | Comportamiento resultante |
|--- |--- |--- |--- |
| Auditude | Auditude | `PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | Publicidades insertadas |
| Eliminar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)`<br>`PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | Rangos eliminados, publicidades insertadas |
| Marcar, Auditude | Marcar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados, sin anuncios insertados |
| Eliminar | Eliminar | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Rangos eliminados |
| Marcar | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Reemplazar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Rangos reemplazados |

**Intervalo de tiempo personalizado**

| Metadatos de anuncio | Resoluciones creadas | `PlacementInformations` creado | Comportamiento resultante |
|--- |--- |--- |--- |
| Eliminar | Eliminar | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Rangos eliminados |
| Eliminar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Rangos eliminados, sin publicidades insertadas |
| Auditude | Auditude | Ninguno | No se insertaron publicidades |
| Reemplazar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalos reemplazados por publicidades |
| Marcar | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Marcar, Auditude | Publicidad personalizada, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados, sin anuncios insertados |

**No definido (predeterminado)**

| Metadatos de anuncio | Resoluciones creadas | `PlacementInformations` creado | Comportamiento resultante |
|--- |--- |--- |--- |
| Eliminar | Eliminar | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Rangos eliminados |
| Eliminar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Rangos eliminados, publicidades insertadas |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Publicidades insertadas |
| Reemplazar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalos reemplazados por publicidades |
| Marcar | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Marcar, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |