---
description: Puede marcar, eliminar y reemplazar intervalos de tiempo en flujos de VOD mediante diferentes combinaciones de modo de señalización de publicidad y metadatos de publicidad. Las diferentes combinaciones de modo de señalización y metadatos resultan en comportamientos diferentes.
title: Efecto en la inserción y eliminación de publicidad de las combinaciones de modo de señalización de publicidad y metadatos de publicidad
exl-id: f42a2db5-642f-4944-87f6-2d7d902a2837
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
| Eliminar, audiencia | Eliminar, audiencia | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),` <br>`PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Intervalos eliminados, anuncios insertados |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Anuncios insertados |
| Reemplazar, Audiencia | Eliminar, audiencia | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalos reemplazados |
| Marcar | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Marcar, audiencia | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados, sin anuncios insertados |

**Señales de manifiesto**

| Metadatos de anuncio | Resoluciones creadas | `PlacementInformations` created | Comportamiento resultante |
|--- |--- |--- |--- |
| Auditude | Auditude | `PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | Anuncios insertados |
| Eliminar, audiencia | Eliminar, audiencia | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)`<br>`PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | Intervalos eliminados, anuncios insertados |
| Marcar, audiencia | Marcar, audiencia | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados, sin anuncios insertados |
| Eliminar | Eliminar | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos eliminados |
| Marcar | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Reemplazar, Audiencia | Eliminar, audiencia | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalos reemplazados |

**Intervalo de tiempo personalizado**

| Metadatos de anuncio | Resoluciones creadas | `PlacementInformations` created | Comportamiento resultante |
|--- |--- |--- |--- |
| Eliminar | Eliminar | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos eliminados |
| Eliminar, audiencia | Eliminar, audiencia | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos eliminados, sin anuncios insertados |
| Auditude | Auditude | Ninguno | No hay anuncios insertados |
| Reemplazar, Audiencia | Eliminar, audiencia | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalos reemplazados por anuncios |
| Marcar | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Marcar, audiencia | Anuncio personalizado, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados, sin anuncios insertados |

**Sin configurar (predeterminado)**

| Metadatos de anuncio | Resoluciones creadas | `PlacementInformations` created | Comportamiento resultante |
|--- |--- |--- |--- |
| Eliminar | Eliminar | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalos eliminados |
| Eliminar, audiencia | Eliminar, audiencia | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Intervalos eliminados, anuncios insertados |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Anuncios insertados |
| Reemplazar, Audiencia | Eliminar, audiencia | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalos reemplazados por anuncios |
| Marcar | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
| Marcar, audiencia | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalos marcados |
