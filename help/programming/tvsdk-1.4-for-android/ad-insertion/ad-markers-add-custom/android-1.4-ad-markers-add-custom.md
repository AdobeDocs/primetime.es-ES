---
description: Mediante marcadores de anuncios personalizados, puede marcar secciones específicas del contenido principal como períodos de contenido relacionado con la publicidad.
title: Agregar marcadores de anuncios personalizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Información general {#add-custom-ad-markers-overview}

Mediante marcadores de anuncios personalizados, puede marcar secciones específicas del contenido principal como períodos de contenido relacionado con la publicidad.

Esta función resulta muy útil cuando se registra contenido, por ejemplo, desde un evento en directo, y el resultado de la grabación es un flujo HLS. La grabación contiene contenido principal y contenido relacionado con la publicidad en un flujo de vídeo bajo demanda (VOD) de HLS. El proceso de grabación no realiza un seguimiento de los segmentos relacionados con la publicidad, por lo que se pierde la información relacionada con la colocación de los anuncios en el contenido principal.

Es posible que pueda obtener la información relacionada con la colocación de los periodos de contenido publicitario de otras fuentes fuera de banda, como sistemas CMS externos. Puede definir marcadores personalizados, a través de los cuales esta información fuera de banda se puede pasar al subsistema del administrador de cronologías. La intención es marcar las secciones de contenido que coinciden con el contenido relacionado con la publicidad especificado de manera que todos los eventos de reproducción específicos de la publicidad se activen del mismo modo que si estos períodos de anuncios personalizados se colocaran explícitamente en la cronología del reproductor.

El seguimiento de anuncios no se administra internamente por TVSDK, como cuando los anuncios se resuelven mediante la toma de decisiones de anuncios de Adobe Primetime (anteriormente conocido como Auditude). Sin embargo, TVSDK proporciona las siguientes abstracciones que definen la forma en que se representa el contenido relacionado con los anuncios en la cronología:

* La pausa publicitaria

   Una pausa publicitaria es una lista ordenada de anuncios consecutivos individuales.
* Un anuncio individual

Los eventos de reproducción se activan por separado para las pausas publicitarias y los anuncios en el punto inicial y final de cada anuncio.

TVSDK envía eventos de seguimiento de anuncios a su aplicación, por lo que puede implementar su propia lógica de seguimiento. Si establece marcadores de publicidad personalizados, recibirá los eventos `onAdBreakStart`, `onAdStart`, `onAdProgress`, `onAdComplete` y `onAdBreakComplete`.
