---
description: Puede marcar, eliminar y reemplazar intervalos de tiempo en flujos de VOD mediante diferentes combinaciones de modo de señalización de publicidad y metadatos de publicidad. Las diferentes combinaciones de modo de señalización y metadatos resultan en comportamientos diferentes.
title: Efecto en la inserción y eliminación de publicidad de las combinaciones de modo de señalización de publicidad y metadatos de publicidad
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Efecto en la inserción y eliminación de publicidad de las combinaciones de modo de señalización de publicidad y metadatos de publicidad {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Puede marcar, eliminar y reemplazar intervalos de tiempo en flujos de VOD mediante diferentes combinaciones de modo de señalización de publicidad y metadatos de publicidad. Las diferentes combinaciones de modo de señalización y metadatos resultan en comportamientos diferentes.

>[!TIP]
>
>Cuando hay un conflicto entre los intervalos de tiempo y los modos de señalización de publicidad, TVSDK da prioridad a los intervalos de tiempo.

En la tabla siguiente se proporcionan los detalles sobre el modo de señalización y los comportamientos de combinación de metadatos:

**Mapa del servidor**

| **Metadatos de anuncio** | **Resoluciones creadas** | **`PlacementInformations`created** | **Comportamiento resultante** |
|--- |--- |--- |--- |
|  | Eliminar | Eliminar | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos eliminados |
| Eliminar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),` <br>`PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Intervalos eliminados, anuncios insertados |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Anuncios insertados |
| Reemplazar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalos reemplazados |
| Marcar | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Mark, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados, sin anuncios insertados |

**Señales de manifiesto**

| Metadatos de anuncio | Resoluciones creadas | `PlacementInformations` created | Comportamiento resultante |
|--- |--- |--- |--- |
| Auditude | Auditude | `PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | Anuncios insertados |
| Eliminar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)`<br>`PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | Intervalos eliminados, anuncios insertados |
| Mark, Auditude | Mark, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados, sin anuncios insertados |
| Eliminar | Eliminar | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos eliminados |
| Marcar | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Reemplazar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalos reemplazados |

**Intervalo de tiempo personalizado**

| Metadatos de anuncio | Resoluciones creadas | `PlacementInformations` created | Comportamiento resultante |
|--- |--- |--- |--- |
| Eliminar | Eliminar | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos eliminados |
| Eliminar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos eliminados, sin anuncios insertados |
| Auditude | Auditude | Ninguno | No hay anuncios insertados |
| Reemplazar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalos reemplazados por anuncios |
| Marcar | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Mark, Auditude | Anuncio personalizado, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados, sin anuncios insertados |

**Sin configurar (predeterminado)**

| Metadatos de anuncio | Resoluciones creadas | `PlacementInformations` created | Comportamiento resultante |
|--- |--- |--- |--- |
| Eliminar | Eliminar | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos eliminados |
| Eliminar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Intervalos eliminados, anuncios insertados |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Anuncios insertados |
| Reemplazar, Auditude | Eliminar, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalos reemplazados por anuncios |
| Marcar | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Mark, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
