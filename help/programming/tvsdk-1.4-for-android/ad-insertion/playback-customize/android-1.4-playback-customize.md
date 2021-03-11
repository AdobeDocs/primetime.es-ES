---
description: Cuando la reproducción llega a una pausa publicitaria, pasa una pausa publicitaria o termina en una pausa publicitaria, TVSDK define algún comportamiento predeterminado para la posición del cabezal de reproducción actual.
title: Personalización de la reproducción con anuncios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# Información general {#customize-playback-with-ads-overview}

Cuando la reproducción llega a una pausa publicitaria, pasa una pausa publicitaria o termina en una pausa publicitaria, TVSDK define algún comportamiento predeterminado para la posición del cabezal de reproducción actual.

>[!TIP]
>
>Puede anular el comportamiento predeterminado utilizando la clase `AdBreakPolicySelector`.

El comportamiento predeterminado varía en función de si el usuario pasa la pausa publicitaria durante la reproducción normal o si busca en un vídeo o lo cambia de posición con avance o rebobinado rápidos (reproducción engañosa).

Puede personalizar el comportamiento de reproducción de publicidad de las siguientes maneras:

* Guarde la posición en la que el usuario dejó de ver el vídeo y reanudó la reproducción en la misma posición en una sesión futura.
* Si se presenta una pausa publicitaria al usuario, no se muestran anuncios adicionales durante un número de minutos, aunque el usuario busque una nueva posición.
* Si el contenido no se reproduce después de unos minutos, reinicie el flujo o realice una conmutación por error a una fuente diferente para el mismo contenido.

   En la sesión de reproducción de conmutación por error, para permitir que el usuario omita los anuncios y vuelva a la posición anterior en la que se produjo un error, puede desactivar los anuncios previos a la emisión o durante la emisión. TVSDK proporciona métodos para permitir saltar anuncios previos y mid-roll.