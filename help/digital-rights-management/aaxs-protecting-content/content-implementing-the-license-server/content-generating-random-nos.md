---
seo-title: Generación de números aleatorios
title: Generación de números aleatorios
uuid: 3ea25c48-1dbe-4039-8091-36c289702f78
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---


# Generación de números aleatorios{#generating-random-numbers}

Los generadores de números aleatorios de hardware pueden utilizarse en servidores Linux para garantizar que se genera suficiente entropía. Si la máquina no puede generar suficiente entropía, las operaciones de Adobe Access que requieren una fuente aleatoria se bloquearán mientras se esperan datos de `/dev/random`.
