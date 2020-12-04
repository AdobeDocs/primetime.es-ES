---
description: La implementación de referencia ilustra cómo configurar el reproductor para anuncios, lo que incluye configurar metadatos de vídeo para la inserción de anuncios y resolver los anuncios anteriores, medios y posteriores en VOD o flujos de vídeo en directo o lineal. También ilustra cómo manejar publicidades en las que se puede hacer clic.
seo-description: La implementación de referencia ilustra cómo configurar el reproductor para anuncios, lo que incluye configurar metadatos de vídeo para la inserción de anuncios y resolver los anuncios anteriores, medios y posteriores en VOD o flujos de vídeo en directo o lineal. También ilustra cómo manejar publicidades en las que se puede hacer clic.
seo-title: Inserción de publicidad
title: Inserción de publicidad
uuid: 75c1d77a-a7ff-4cb6-ad7f-7c83a950b7cb
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# Inserción de publicidad {#ad-insertion}

La implementación de referencia ilustra cómo configurar el reproductor para anuncios, lo que incluye configurar metadatos de vídeo para la inserción de anuncios y resolver los anuncios anteriores, medios y posteriores en VOD o flujos de vídeo en directo o lineal. También ilustra cómo manejar publicidades en las que se puede hacer clic.

El proceso de configurar un reproductor para la inserción de publicidad incluye:

* **Fuente de entrada:** Rellenado de una fuente de entrada con metadatos de anuncio. Consulte [Formato del catálogo](../set-up-dev-environment/exploring-code/catalog-format.md).
* **Adaptador de fuente de implementación de referencia:** análisis de la fuente de entrada para rellenar un objeto de metadatos de anuncio.
* **AdsManager:** Uso de AdsManager para recuperar los metadatos de la publicidad y crear el AdProvider correspondiente.