---
description: Cuando la reproducción llega a una pausa publicitaria, pasa una pausa publicitaria o termina en una pausa publicitaria, TVSDK define algún comportamiento predeterminado para la colocación del cabezal de reproducción actual.
title: Personalización de la reproducción con anuncios
exl-id: 5606c9c6-58ff-42a7-974e-3a445f3d3f28
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# Información general {#customize-playback-with-ads}

Cuando la reproducción llega a una pausa publicitaria, pasa una pausa publicitaria o termina en una pausa publicitaria, TVSDK define algún comportamiento predeterminado para la colocación del cabezal de reproducción actual.

>[!TIP]
>
>Puede anular el comportamiento predeterminado utilizando la variable `AdBreakPolicySelector` clase.

El comportamiento predeterminado varía en función de si el usuario pasa la pausa publicitaria durante la reproducción normal, buscando en un vídeo o reposicionándolo con avance rápido o rebobinado (reproducción con trucos).

Puede personalizar el comportamiento de reproducción de la publicidad de las siguientes maneras:

* Guarde la posición en la que el usuario dejó de ver el vídeo y reanude la reproducción en la misma posición en una sesión futura.
* Si se presenta una pausa publicitaria al usuario, este no mostrará anuncios adicionales durante unos minutos, aunque busque una nueva posición.
* Si el contenido no se reproduce después de unos minutos, reinicie el flujo o realice una conmutación por error a un origen diferente para el mismo contenido.

En la sesión de reproducción por error, para permitir que el usuario omita los anuncios y se reanude a la posición con error anterior, puede desactivar los anuncios previos a la emisión o los anuncios durante la emisión. TVSDK proporciona métodos para habilitar la omisión de anuncios previos a la emisión y anuncios durante la emisión.
