---
description: Cuando la reproducción llega a una pausa publicitaria, pasa una pausa publicitaria o termina en una pausa publicitaria, TVSDK define un comportamiento predeterminado para la posición del cursor de reproducción actual.
seo-description: Cuando la reproducción llega a una pausa publicitaria, pasa una pausa publicitaria o termina en una pausa publicitaria, TVSDK define un comportamiento predeterminado para la posición del cursor de reproducción actual.
seo-title: Personalización de la reproducción con anuncios
title: Personalización de la reproducción con anuncios
uuid: 20b5bfb2-83d8-4517-b821-8c542afa387d
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Información general {#customize-playback-with-ads}

Cuando la reproducción llega a una pausa publicitaria, pasa una pausa publicitaria o termina en una pausa publicitaria, TVSDK define un comportamiento predeterminado para la posición del cursor de reproducción actual.

>[!TIP]
>
>Puede anular el comportamiento predeterminado mediante la clase `AdBreakPolicySelector`.

El comportamiento predeterminado varía en función de si el usuario pasa la pausa publicitaria durante la reproducción normal o si busca en un vídeo o lo cambia de posición con un avance o rebobinado rápido (reproducción ficticia).

Puede personalizar el comportamiento de la reproducción de publicidad de las siguientes formas:

* Guarde la posición en la que el usuario dejó de ver el vídeo y reanuda la reproducción en la misma posición en una sesión futura.
* Si se presenta una pausa publicitaria al usuario, no se mostrarán anuncios adicionales durante unos minutos, aunque el usuario busque una nueva posición.
* Si el contenido no se reproduce después de unos minutos, reinicie el flujo o vuelva a una fuente diferente para el mismo contenido.

   En la sesión de reproducción de conmutación por error, para permitir que el usuario omita los anuncios y vuelva a la posición de error anterior, puede desactivar los anuncios anteriores y/o medios. TVSDK proporciona métodos para permitir omitir anuncios anteriores y finales.