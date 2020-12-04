---
seo-title: Crítica de las políticas de DRM
title: Crítica de las políticas de DRM
uuid: ddc03142-7acb-4a9f-a367-e34cfc5e78ba
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# Crítica de directivas de DRM{#drm-policy-criticality}

Si planea aplicar nuevas reglas de uso en una directiva DRM y tiene pensado utilizar esta directiva DRM en el contenido que se ha empaquetado para servidores de licencias antiguos (y por lo tanto no interpreta correctamente las nuevas reglas de uso), es posible que tenga que especificar el comportamiento de los servidores de licencias antiguos. De forma predeterminada, la criticidad de la directiva DRM se establece en `true`.

Esta configuración indica que el servidor de licencias debe procesar todas las partes de la directiva DRM para poder generar una licencia que utilice la directiva DRM especificada. Si la criticidad de la directiva DRM está establecida en `false`, un servidor de licencias anterior puede ignorar las partes de la directiva DRM que no puede interpretar correctamente. Por lo tanto, las licencias que genere el servidor no incluyen nuevas reglas de uso.

Los servidores DRM Primetime que admiten la versión 2.0.2 del SDK o posterior aceptan la configuración de criticidad de la directiva DRM.
