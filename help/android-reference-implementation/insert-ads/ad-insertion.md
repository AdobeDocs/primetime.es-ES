---
description: La implementación de referencia ilustra cómo configurar el reproductor para anuncios, lo que incluye la configuración de metadatos de vídeo para la inserción de anuncios y la resolución de los anuncios previos, medios y posteriores a la emisión en flujos de vídeo de VOD o de vídeo en directo/lineales. También ilustra cómo gestionar los anuncios en los que se puede hacer clic.
title: Inserción de publicidad
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Inserción de publicidad {#ad-insertion}

La implementación de referencia ilustra cómo configurar el reproductor para anuncios, lo que incluye la configuración de metadatos de vídeo para la inserción de anuncios y la resolución de los anuncios previos, medios y posteriores a la emisión en flujos de vídeo de VOD o de vídeo en directo/lineales. También ilustra cómo gestionar los anuncios en los que se puede hacer clic.

El proceso de configuración de un reproductor para la inserción de anuncios incluye lo siguiente:

* **Fuente de entrada:** Rellenar una fuente de entrada con metadatos de publicidad. Consulte [Formato de catálogo](../set-up-dev-environment/exploring-code/catalog-format.md).
* **Adaptador de fuente de implementación de referencia:** Analizando la fuente de entrada para rellenar un objeto de metadatos de publicidad.
* **Administrador de anuncios:** Usar el Administrador de anuncios para recuperar los metadatos de la publicidad y crear el AdProvider correspondiente.
