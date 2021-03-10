---
title: Crítica de las políticas
description: Crítica de las políticas
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Criticidad de las políticas{#policy-criticality}

Si se utilizan nuevas reglas de uso en las directivas y estas políticas se utilizan en el contenido empaquetado para servidores de licencias más antiguos (que no comprenden las nuevas reglas de uso), puede especificar cómo deben comportarse los servidores de licencias más antiguos. De forma predeterminada, la importancia de la directiva es &quot;true&quot;, lo que significa que el servidor de licencias debe comprender todas las partes de la directiva para generar una licencia utilizando la directiva . Si la criticidad de la directiva se establece en &quot;false&quot;, un servidor de licencias anterior puede ignorar partes de la directiva que no comprende, y las licencias generadas por el servidor no contendrán las nuevas reglas de uso.

Los servidores de acceso a Adobe que utilicen la versión 2.0.2 del SDK y posteriores respetarán la configuración de criticidad de las directivas.
