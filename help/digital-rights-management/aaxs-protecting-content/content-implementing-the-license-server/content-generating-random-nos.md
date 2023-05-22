---
title: Generación de números aleatorios
description: Generación de números aleatorios
copied-description: true
exl-id: 9a816570-753e-4b05-a6ea-2d4b20ffa3d4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---

# Generación de números aleatorios{#generating-random-numbers}

Los generadores de números aleatorios de hardware se pueden utilizar en servidores Linux para garantizar que se genera una entropía suficiente. Si el equipo no puede generar suficiente entropía, las operaciones de acceso a Adobe que requieran una fuente de aleatoriedad se bloquearán mientras esperan datos de `/dev/random`.
