---
description: La implementación de referencia ilustra cómo configurar el reproductor para los anuncios, lo que incluye la configuración de metadatos de vídeo para la inserción de anuncios y la resolución de los anuncios previos, medios y posteriores en VOD o flujos de vídeo en directo/lineal. También ilustra cómo administrar los anuncios en los que se puede hacer clic.
title: Inserción de publicidad
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Inserción de publicidad {#ad-insertion}

La implementación de referencia ilustra cómo configurar el reproductor para los anuncios, lo que incluye la configuración de metadatos de vídeo para la inserción de anuncios y la resolución de los anuncios previos, medios y posteriores en VOD o flujos de vídeo en directo/lineal. También ilustra cómo administrar los anuncios en los que se puede hacer clic.

El proceso de configuración de un reproductor para la inserción de publicidad incluye:

* **Fuente de entrada:** Rellenado de una fuente de entrada con metadatos de anuncio. Consulte [Formato del catálogo](../set-up-dev-environment/exploring-code/catalog-format.md).
* **Adaptador de fuente de implementación de referencia:** análisis de la fuente de entrada para rellenar un objeto de metadatos de publicidad.
* **AdsManager:** usar AdsManager para recuperar los metadatos de publicidad y crear el AdProvider correspondiente.