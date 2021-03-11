---
description: Puede marcar, eliminar y reemplazar intervalos de tiempo en flujos de VOD mediante el uso de diferentes modos de señalización de anuncios y combinaciones de metadatos de anuncios. Las diferentes combinaciones de modo de señalización y metadatos dan como resultado comportamientos diferentes.
title: Efecto en la inserción y eliminación de anuncios del modo de señalización de anuncios y las combinaciones de metadatos de anuncios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---


# Efecto en la inserción y eliminación de anuncios del modo de señalización de anuncios y las combinaciones de metadatos de anuncios {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Puede marcar, eliminar y reemplazar intervalos de tiempo en flujos de VOD mediante el uso de diferentes modos de señalización de anuncios y combinaciones de metadatos de anuncios. Las diferentes combinaciones de modo de señalización y metadatos dan como resultado comportamientos diferentes.

>[!TIP]
>
>Cuando hay un conflicto entre intervalos de tiempo y modos de señalización de anuncios, TVSDK da prioridad a los intervalos de tiempo.

La tabla siguiente proporciona los detalles sobre el modo de señalización y los comportamientos de combinación de metadatos:

**Mapa del servidor**

| **Metadatos de publicidad** | **Resoluciones creadas** | **`PlacementInformations`created** | **Comportamiento resultante** |
|--- |--- |--- |--- |
|  | Eliminar | Eliminar | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Rangos eliminados |
| Eliminar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),` <br>`PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Rangos eliminados, anuncios insertados |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Anuncios insertados |
| Reemplazar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Rangos reemplazados |
| Marcar | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Rangos marcados |
| Marcar, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Rangos marcados, sin anuncios insertados |

**Señales de manifiesto**

| Metadatos de publicidad | Resoluciones creadas | `PlacementInformations` created | Comportamiento resultante |
|--- |--- |--- |--- |
| Auditude | Auditude | `PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | Anuncios insertados |
| Eliminar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)`<br>`PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | Rangos eliminados, anuncios insertados |
| Marcar, Auditude | Marcar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Rangos marcados, sin anuncios insertados |
| Eliminar | Eliminar | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Rangos eliminados |
| Marcar | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Rangos marcados |
| Reemplazar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Rangos reemplazados |

**Intervalo de tiempo personalizado**

| Metadatos de publicidad | Resoluciones creadas | `PlacementInformations` created | Comportamiento resultante |
|--- |--- |--- |--- |
| Eliminar | Eliminar | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Rangos eliminados |
| Eliminar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Rangos eliminados, sin anuncios insertados |
| Auditude | Auditude | Ninguna | No se insertaron anuncios |
| Reemplazar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Rangos reemplazados por anuncios |
| Marcar | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Rangos marcados |
| Marcar, Auditude | Publicidad personalizada, audiencia | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Rangos marcados, sin anuncios insertados |

**Sin establecer (predeterminado)**

| Metadatos de publicidad | Resoluciones creadas | `PlacementInformations` created | Comportamiento resultante |
|--- |--- |--- |--- |
| Eliminar | Eliminar | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Rangos eliminados |
| Eliminar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Rangos eliminados, anuncios insertados |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Anuncios insertados |
| Reemplazar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Rangos reemplazados por anuncios |
| Marcar | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Rangos marcados |
| Marcar, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Rangos marcados |