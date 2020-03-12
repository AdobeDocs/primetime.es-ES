---
description: Cuando la reproducción llega a una pausa publicitaria, pasa una pausa publicitaria o termina en una pausa publicitaria, TVSDK define un comportamiento predeterminado para la posición del cursor de reproducción actual.
seo-description: Cuando la reproducción llega a una pausa publicitaria, pasa una pausa publicitaria o termina en una pausa publicitaria, TVSDK define un comportamiento predeterminado para la posición del cursor de reproducción actual.
seo-title: Personalización de la reproducción con anuncios
title: Personalización de la reproducción con anuncios
uuid: e7c9f4b1-15c9-43a2-be00-1ca4bfd17e43
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Información general {#customize-playback-with-ads-overview}

Cuando la reproducción llega a una pausa publicitaria, pasa una pausa publicitaria o termina en una pausa publicitaria, TVSDK define un comportamiento predeterminado para la posición del cursor de reproducción actual.

>[!TIP]
>
>Puede anular el comportamiento predeterminado mediante la `AdPolicySelector` clase.

El comportamiento predeterminado varía en función de si el usuario pasa la pausa publicitaria durante la reproducción normal o si busca en un vídeo o lo cambia de posición con un avance o rebobinado rápido (reproducción ficticia).

Puede personalizar el comportamiento de la reproducción de publicidad de las siguientes formas:

* Guarde la posición en la que el usuario dejó de ver el vídeo y reanuda la reproducción en la misma posición en una sesión futura.
* Si se presenta una pausa publicitaria al usuario, no se muestran anuncios adicionales durante un número de minutos, aunque el usuario busque una nueva posición.
* Si el contenido no se reproduce después de unos minutos, reinicie el flujo o vuelva a una fuente diferente para el mismo contenido.

   En la sesión de reproducción de conmutación por error, para permitir que el usuario omita los anuncios y vuelva a la posición de error anterior, puede desactivar los anuncios anteriores y/o medios. TVSDK proporciona métodos para permitir omitir anuncios anteriores y finales.