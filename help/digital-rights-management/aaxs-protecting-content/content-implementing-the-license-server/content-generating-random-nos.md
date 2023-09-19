---
title: Generación de números aleatorios
description: Generación de números aleatorios
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---

# Generación de números aleatorios{#generating-random-numbers}

Los generadores de números aleatorios de hardware se pueden utilizar en servidores Linux para garantizar que se genera una entropía suficiente. Si el equipo no puede generar suficiente entropía, las operaciones de acceso a Adobe que requieran una fuente de aleatoriedad se bloquearán mientras esperan datos de `/dev/random`.
