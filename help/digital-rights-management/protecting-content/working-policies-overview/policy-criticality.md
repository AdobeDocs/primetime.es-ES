---
title: Crítica de política de DRM
description: Crítica de política de DRM
copied-description: true
exl-id: b9f5a095-9ec4-4ad7-8b70-9abae72d2a86
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# Crítica de política de DRM{#drm-policy-criticality}

Si tiene pensado aplicar nuevas reglas de uso en una directiva DRM y va a utilizar esta directiva DRM en contenido que se ha empaquetado para servidores de licencias anteriores (y, por lo tanto, no interpreta correctamente las nuevas reglas de uso), es posible que tenga que especificar cómo deben comportarse los servidores de licencias anteriores. De forma predeterminada, la importancia de la política de DRM se establece en `true`.

Esta configuración indica que el servidor de licencias debe procesar todas las partes de la directiva DRM para poder generar una licencia que utilice la directiva DRM especificada. Si la importancia de la política de DRM se define en `false`Sin embargo, un servidor de licencias antiguo puede ignorar aquellas partes de la directiva DRM que no puede interpretar correctamente. Por lo tanto, las licencias generadas por el servidor no incluyen nuevas reglas de uso.

Los servidores DRM de Primetime compatibles con la versión 2.0.2 o posterior del SDK aceptan la configuración de importancia crítica de la directiva DRM.
