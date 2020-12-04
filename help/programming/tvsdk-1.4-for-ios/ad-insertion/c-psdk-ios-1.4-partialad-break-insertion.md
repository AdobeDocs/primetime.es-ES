---
description: TVSDK ofrece una experiencia de tipo TV de poder unirse en medio de un anuncio, en transmisiones en directo.
seo-description: TVSDK ofrece una experiencia de tipo TV de poder unirse en medio de un anuncio, en transmisiones en directo.
seo-title: Inserción parcial de pausa publicitaria
title: Inserción parcial de pausa publicitaria
uuid: b6ee62da-c4d1-42f2-b03d-f73247f8e585
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---


# Inserción parcial de pausa publicitaria{#partial-ad-break-insertion}

TVSDK ofrece una experiencia de tipo TV de poder unirse en medio de un anuncio, en transmisiones en directo.

La función de inserción parcial de pausa publicitaria le permite imitar una experiencia parecida a un televisor en la que, si el cliente inicio un flujo en directo dentro de un ciclo intermedio, inicio la reproducción dentro de ese ciclo intermedio. Es similar a cambiar a un canal de TV y los comerciales funcionan perfectamente.

Por ejemplo: si un usuario se une en medio de una pausa publicitaria de 90 segundos (tres anuncios de 30 segundos), 10 segundos después de la segunda publicidad (es decir, a los 40 segundos de la pausa publicitaria), el segundo anuncio se reproduce durante el resto de la duración (20 segundos) seguido del tercer anuncio.

## Rastrear publicidad {#section_03AFAEAA8DA44399952DC51C5E12951E}

Los rastreadores de anuncios para el anuncio reproducido parcialmente (el segundo anuncio) no se activan. En el ejemplo anterior, solo se activa el rastreador para la tercera publicidad.

## Comportamiento con predesplazamiento {#section_7DFBFB12E63343D1A0C614F0CF9F1714}

La función funciona cuando un anuncio previo se reproduce con contenido en directo. El flujo se reproduce desde el punto activo una vez finalizado el anuncio previo.

Los eventos de pausa publicitaria se envían incluso si no hay anuncios completos en esta pausa publicitaria. Una publicidad se considera parcial si se omite durante más de un segundo. Por ejemplo, si un usuario ve un anuncio que omitió durante 800 ms, se considerará un anuncio completo.
