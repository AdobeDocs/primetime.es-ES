---
description: TVSDK proporciona una experiencia similar a la de TV de poder unirse en medio de un anuncio en emisiones en directo.
title: Inserción parcial de pausa publicitaria
exl-id: ae260f1a-8c4a-44b9-8f74-285f93d999e4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# Inserción parcial de pausa publicitaria{#partial-ad-break-insertion}

TVSDK proporciona una experiencia similar a la de TV de poder unirse en medio de un anuncio en emisiones en directo.

La función de inserción de pausa publicitaria parcial le permite imitar una experiencia similar a una TV en la que, si el cliente inicia una emisión en directo dentro de una emisión mid-roll, comienza a reproducirse dentro de esa emisión mid-roll. Es similar a cambiar a un canal de TV y los anuncios se ejecutan sin problemas.

Por ejemplo, si un usuario se une en medio de una pausa publicitaria de 90 segundos (tres anuncios de 30 segundos), 10 segundos en el segundo anuncio (es decir, a los 40 segundos en la pausa publicitaria), el segundo anuncio se reproduce durante el tiempo restante (20 segundos) seguido del tercer anuncio.

## Seguimiento de publicidad {#section_03AFAEAA8DA44399952DC51C5E12951E}

Los rastreadores de anuncios para el anuncio parcialmente reproducido (el segundo anuncio) no se activan. En el ejemplo anterior, solo se activa el rastreador del tercer anuncio.

## Comportamiento con anuncio previo a la emisión {#section_7DFBFB12E63343D1A0C614F0CF9F1714}

La función funciona cuando se reproduce un anuncio previo a la emisión con contenido en directo. El flujo se reproduce desde el punto en directo una vez finalizado el anuncio previo a la emisión.

Se envían eventos de pausa publicitaria aunque no haya anuncios completos en esta pausa publicitaria. Un anuncio se considera parcial si se omite durante más de un segundo. Por ejemplo, si un visualizador ve un anuncio que omitió durante 800 ms, se considera un anuncio completo.
