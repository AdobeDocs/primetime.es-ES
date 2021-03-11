---
description: Esta guía proporciona información sobre cómo desarrollar aplicaciones de reproductor de vídeo mediante TVSDK para Android, que se implementa en Java.
title: Información general del producto, audiencia y esta guía
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# Información general {#audience}

Esta guía proporciona información sobre cómo desarrollar aplicaciones de reproductor de vídeo mediante TVSDK para Android, que se implementa en Java.

<!--<a id="section_FC24E86A2E6442B8A3769160769BBDFA"></a>-->

* Para obtener una lista de las funciones compatibles con TVSDK, consulte [Funciones de Primetime TVSDK](../../../tvsdk-3x-android-prog/android-3x-introduction/overview-prod-audience-guide/android-3x-overview-of-the-player.md).
* Para conocer los requisitos específicos de hardware y software para utilizar TVSDK, consulte [Requisitos](../../../tvsdk-3x-android-prog/android-3x-introduction/android-3x-requirements.md).
* Para obtener una lista de las API disponibles, consulte [API de Android de TVSDK](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.5/index.html).

## Información general del producto {#section_9664959F25C948878F2F7EF3D360CA95}

TVSDK incluye descripciones de API y ejemplos de código para ayudarle a integrar funciones de vídeo avanzadas, protección de contenido y publicidad en su reproductor. Java se utiliza para crear una interfaz de usuario del reproductor de vídeo. TVSDK le ayuda a conectar esa interfaz de usuario a su reproductor de medios. Esto le permite reproducir vídeos y anuncios basados en manifiestos de medios. También puede utilizar TVSDK para recuperar información sobre el vídeo, gestionar la seguridad y controlar y supervisar la reproducción.

## Audiencia {#section_527860B373734D3BA89FCF5EC1F6DC37}

En esta guía se asume que se entiende cómo desarrollar aplicaciones y reproductores de vídeo utilizando Java. Implemente la interfaz de usuario del reproductor de vídeo en Java e incorpore las funciones de TVSDK que necesite.

## Acerca de esta guía {#section_9A5B2FC506B34B5DB71CA827B307A4D0}

Esta guía proporciona información que le permite incorporar funciones de TVSDK en un reproductor de vídeo usando Java en dispositivos Android.

## Notación de área de nombres en esta guía {#section_8B866054E9ED4B5F99DCA7A681404632}

>[!TIP]
>
>El prefijo [!DNL com.adobe.mediacore] del espacio de nombres de la API de TVSDK se suele omitir para la brevedad.
>
>Se hace referencia a muchos elementos de API sin su indicador de clase principal si el contexto es claro.