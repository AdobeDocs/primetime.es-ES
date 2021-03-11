---
title: Crítica de las políticas de DRM
description: Crítica de las políticas de DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# Importancia de la directiva DRM{#drm-policy-criticality}

Si planea aplicar nuevas reglas de uso en una directiva DRM y si planea usar esta directiva DRM en contenido que se haya empaquetado para servidores de licencias antiguos (y, por lo tanto, no interpreta correctamente las nuevas reglas de uso), es posible que tenga que especificar cómo deben comportarse los servidores de licencias más antiguos. De forma predeterminada, la criticidad de las directivas de DRM se establece en `true`.

Esta configuración indica que el servidor de licencias debe procesar todas las partes de la directiva DRM antes de poder generar una licencia que utilice la directiva DRM especificada. Si la criticidad de la directiva DRM se establece en `false`, un servidor de licencias anterior puede ignorar las partes de la directiva DRM que no puede interpretar correctamente. Por lo tanto, las licencias que genere el servidor no incluyen ninguna regla de uso nueva.

Los servidores DRM de Primetime que admiten la versión 2.0.2 del SDK o posterior aceptan la configuración de criticidad de la directiva DRM.
