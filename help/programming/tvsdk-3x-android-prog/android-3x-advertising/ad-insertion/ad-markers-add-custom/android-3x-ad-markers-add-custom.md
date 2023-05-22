---
description: Mediante marcadores de anuncio personalizados, puede marcar secciones específicas del contenido principal como periodos de contenido relacionados con anuncios.
title: Añadir marcadores de publicidad personalizados
exl-id: f60d3b1e-42e8-40ca-a35c-300d1a580ece
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Información general {#add-custom-ad-markers-overview}

Mediante marcadores de anuncio personalizados, puede marcar secciones específicas del contenido principal como periodos de contenido relacionados con anuncios.

Esta función es muy útil cuando el contenido se está grabando, por ejemplo, desde un evento en directo, y el resultado de la grabación es una emisión HLS. La grabación contiene el contenido principal y el contenido relacionado con la publicidad en un flujo de vídeo bajo demanda (VOD) de HLS. El proceso de grabación no realiza un seguimiento de los segmentos relacionados con el anuncio, por lo que se pierde la información relacionada con el posicionamiento de los anuncios en el contenido principal.

Es posible que pueda obtener la información relacionada con el posicionamiento de los periodos de contenido de la publicidad de otras fuentes fuera de banda, como sistemas CMS externos. Puede definir marcadores personalizados, a través de los cuales se puede pasar esta información fuera de banda al subsistema del administrador de la línea de tiempo. La intención es marcar las secciones de contenido que coincidan con el contenido especificado relacionado con el anuncio de forma que todos los eventos de reproducción específicos del anuncio se activen de la misma manera que si estos periodos de publicidad personalizados se colocaran explícitamente en la cronología del reproductor.

El seguimiento de anuncios no se gestiona internamente mediante TVSDK, como cuando los anuncios se resuelven mediante Adobe Primetime ad decisioning. Sin embargo, TVSDK proporciona las siguientes abstracciones que definen la forma en que el contenido relacionado con anuncios se representa en la cronología:

* La pausa publicitaria

   Una pausa publicitaria es una lista ordenada de anuncios consecutivos individuales.
* Un anuncio individual

Los eventos de reproducción se activan por separado para las pausas publicitarias y los anuncios en los puntos de inicio y finalización de cada anuncio.

TVSDK envía y rastrea eventos a su aplicación, para que pueda implementar su propia lógica de seguimiento. Si establece marcadores de publicidad personalizados, recibirá la variable `onAdBreakStart`, `onAdStart`, `onAdProgress`, `onAdComplete`, y `onAdBreakComplete` eventos.
