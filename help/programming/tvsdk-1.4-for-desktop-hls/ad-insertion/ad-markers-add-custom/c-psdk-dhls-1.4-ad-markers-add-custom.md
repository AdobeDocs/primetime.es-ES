---
description: Mediante los marcadores de publicidad personalizados, puede marcar secciones específicas del contenido principal como períodos de contenido relacionados con la publicidad.
seo-description: Mediante los marcadores de publicidad personalizados, puede marcar secciones específicas del contenido principal como períodos de contenido relacionados con la publicidad.
seo-title: Agregar marcadores de publicidad personalizados
title: Agregar marcadores de publicidad personalizados
uuid: 7cf76e76-965c-4ee4-a311-e28b5a3b5046
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Información general {#add-custom-ad-markers-overview}

Mediante los marcadores de publicidad personalizados, puede marcar secciones específicas del contenido principal como períodos de contenido relacionados con la publicidad.

Esta función resulta muy útil cuando se graba contenido, por ejemplo, desde un evento en directo, y el resultado de la grabación es un flujo HLS. La grabación contiene contenido principal y contenido relacionado con la publicidad en un flujo de vídeo bajo demanda (VOD) HLS. El proceso de registro no realiza un seguimiento de los segmentos relacionados con la publicidad, por lo que se pierde la información relacionada con la colocación de las publicidades en el contenido principal.

Es posible que pueda obtener la información relacionada con la colocación de los períodos de contenido de publicidad desde otras fuentes fuera de banda, como los sistemas CMS externos. Puede definir marcadores personalizados, a través de los cuales esta información fuera de banda se puede pasar al subsistema de administración de línea de tiempo. La intención es marcar las secciones de contenido que coinciden con el contenido relacionado con la publicidad especificado de manera que todos los eventos de reproducción específicos de la publicidad se activen de la misma manera que si estos puntos de publicidad personalizados se colocaran explícitamente en la línea de tiempo del reproductor.

TVSDK no gestiona internamente el seguimiento de anuncios, como cuando los anuncios se resuelven mediante Adobe Primetime y la toma de decisiones (anteriormente conocido como Auditude). Sin embargo, TVSDK proporciona las siguientes abstracciones que definen la forma en que se representa el contenido relacionado con la publicidad en la línea de tiempo:

* La pausa publicitaria

   Una pausa publicitaria es una lista ordenada de publicidades consecutivas individuales.
* Una publicidad individual

Los eventos de reproducción se activan por separado para las pausas publicitarias y las publicidades en el punto inicial y final de cada publicidad.

TVSDK distribuye eventos de seguimiento de anuncios a la aplicación, para que pueda implementar su propia lógica de seguimiento. Si establece marcadores de publicidad personalizados, recibirá los `AD_BREAK_STARTED`eventos, `AD_STARTED`, `AD_PROGRESS`, `AD_COMPLETED`y `AD_BREAK_COMPLETED` .