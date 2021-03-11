---
description: Esta guía proporciona información sobre cómo desarrollar aplicaciones de reproductor de vídeo mediante el TVSDK del explorador.
title: Resumen y audiencia del producto
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Resumen del producto y audiencia{#product-overview-and-audience}

Esta guía proporciona información sobre cómo desarrollar aplicaciones de reproductor de vídeo mediante el TVSDK del explorador.

## Información general del producto {#section_1C66E736CEFD4246B7C7C99AADD48118}

El Kit de desarrollo de software de Adobe Primetime (TVSDK de navegador) es un kit de herramientas que le permite añadir funcionalidad avanzada de reproducción de vídeo, protección de contenido y publicidad a sus aplicaciones de reproductor de vídeo basadas en navegador. El SDK de TVSDK de explorador proporciona API de JavaScript para crear aplicaciones de vídeo basadas en explorador e incluye compatibilidad con la reproducción en los modos siguientes:

* Solo HTML5
* HTML5 con reserva flash automática
* Flash siempre

Esta versión incluye las API de TVSDK del explorador y una implementación de referencia de ejemplo.

### Marco de IU

Para acelerar el desarrollo de la interfaz de usuario para las aplicaciones de reproductor de vídeo basadas en JavaScript para navegadores, el SDK de explorador incluye un marco de interfaz de usuario que consta de API para:

* Incluir controles predeterminados de la interfaz de usuario, como reproducción/pausa, volumen, etc.
* Añada (o elimine) fácilmente controles avanzados de la interfaz de usuario de reproducción sin manipular directamente la estructura DOM
* Configure fácilmente el comportamiento de los controles de IU asociados
* Crear controles de IU personalizados
* Diseño de la IU del reproductor según los requisitos

Para obtener más información sobre las API para el marco de IU, consulte [UI Framework for Browser TVSDK 2.4](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/index.html).

## Audiencia {#section_DFC9DECC2E30426DBBDDEA4E288E666C}

En esta guía se da por hecho que se comprende cómo desarrollar aplicaciones y reproductores de vídeo mediante JavaScript. Puede implementar un reproductor de vídeo e incorporar las funciones del SDK de TVSDK del explorador.