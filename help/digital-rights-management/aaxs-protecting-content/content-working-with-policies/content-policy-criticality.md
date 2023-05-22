---
title: Crítica de política
description: Crítica de política
copied-description: true
exl-id: 6c6971fe-0c0a-4998-917c-aebbf1c4a9df
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Crítica de política{#policy-criticality}

Si se utilizan nuevas reglas de uso en las directivas y estas directivas se utilizan en contenido empaquetado para servidores de licencias más antiguos (que no comprenden las nuevas reglas de uso), puede especificar cómo deben comportarse los servidores de licencias más antiguos. De forma predeterminada, la importancia de la directiva es &quot;true&quot;, lo que significa que el servidor de licencias debe comprender todas las partes de la directiva para generar una licencia con ella. Si la importancia de la directiva se establece en &quot;false&quot;, un servidor de licencias anterior puede ignorar partes de la directiva que no comprende y las licencias generadas por el servidor no contendrán las nuevas reglas de uso.

Los servidores de acceso de Adobe que utilicen la versión 2.0.2 o superior del SDK respetarán la configuración de importancia crítica de la directiva.
