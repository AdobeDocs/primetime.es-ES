---
seo-title: Criticidad de las políticas
title: Criticidad de las políticas
uuid: 076f386e-ba58-4507-92a3-a190126c881e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Criticidad de las políticas{#policy-criticality}

Si se utilizan nuevas reglas de uso en las directivas y estas políticas en el contenido empaquetado para servidores de licencias antiguos (que no entienden las nuevas reglas de uso), puede especificar el comportamiento de los servidores de licencias antiguos. De forma predeterminada, la importancia de la directiva es &quot;true&quot;, lo que significa que el servidor de licencias debe comprender todas las partes de la directiva para generar una licencia mediante la directiva. Si la criticidad de la directiva se establece en &quot;false&quot;, un servidor de licencias anterior puede ignorar partes de la directiva que no comprende y las licencias generadas por el servidor no contendrán las nuevas reglas de uso.

Los servidores de Adobe Access que utilicen la versión 2.0.2 del SDK y versiones posteriores respetarán la configuración de criticidad de las políticas.
