---
description: TVSDK proporciona una experiencia parecida a la de TV de poder unirse en medio de un anuncio, en transmisiones en directo.
title: Inserción parcial de pausa publicitaria
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Inserción parcial de pausa publicitaria{#partial-ad-break-insertion}

TVSDK proporciona una experiencia parecida a la de TV de poder unirse en medio de un anuncio, en transmisiones en directo.

La función de inserción de pausa publicitaria parcial le permite imitar una experiencia parecida a un televisor en la que, si el cliente inicia una emisión en directo dentro de una emisión intermedia, comienza a reproducirse dentro de esa emisión media. Es similar a cambiar a un canal de televisión y los anuncios se ejecutan sin problemas.

Por ejemplo, si un usuario se une en medio de una pausa publicitaria de 90 segundos (tres anuncios de 30 segundos) y después de 10 segundos (es decir, a los 40 segundos de la pausa publicitaria), el segundo anuncio se reproduce durante el resto de los segundos (20 segundos) seguido del tercer anuncio.

## Seguimiento de publicidad {#section_03AFAEAA8DA44399952DC51C5E12951E}

Los rastreadores de anuncios para el anuncio reproducido parcialmente (el segundo anuncio) no se activan. En el ejemplo anterior, solo se activa el rastreador del tercer anuncio.

## Comportamiento con {#section_7DFBFB12E63343D1A0C614F0CF9F1714} pre-roll

La función funciona cuando un anuncio pre-roll se reproduce con contenido en directo. La emisión se reproduce desde el punto de lanzamiento después de que finalice el anuncio previo a la emisión.

Los eventos de pausa publicitaria se envían incluso si no hay anuncios completos en esta pausa publicitaria. Un anuncio se considera parcial si se omite durante más de un segundo. Por ejemplo, si un espectador ve un anuncio que omitió durante 800 ms, se considera un anuncio completo.
