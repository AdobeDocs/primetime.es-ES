---
title: Generación de números aleatorios
description: Generación de números aleatorios
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---


# Generación de números aleatorios{#generating-random-numbers}

Los generadores aleatorios de hardware se pueden usar en servidores Linux para garantizar que se genere suficiente entropía. Si el equipo no puede generar suficiente entropía, las operaciones de acceso a Adobe que requieren una fuente de aleatoriedad se bloquearán mientras esperan los datos de `/dev/random`.
