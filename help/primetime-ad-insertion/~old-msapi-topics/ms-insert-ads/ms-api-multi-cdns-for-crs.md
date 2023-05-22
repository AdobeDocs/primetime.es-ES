---
description: Aunque el escenario predeterminado del servicio de reempaquetado creativo (CRS) es utilizar una red de distribución de contenido (CDN), puede implementar recursos CRS en más de una CDN.
title: Compatibilidad con varias CDN para la entrega de anuncios CRS
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# Compatibilidad con varias CDN para la entrega de anuncios CRS {#multiple-cdn-support-for-crs-ad-delivery}

Aunque el escenario predeterminado del servicio de reempaquetado creativo (CRS) es utilizar una red de distribución de contenido (CDN), puede implementar recursos CRS en más de una CDN.

## Requisitos

Puede utilizar varias CDN por los siguientes motivos:

* Necesidad de ampliación para grandes eventos de visualización
* Un requisito para hacer coincidir el origen de CDN del recurso CRS con el origen de CDN del contenido principal.
* Un requisito para utilizar una CDN diferente de la CDN predeterminada CRS (Akamai).

Cuando el servidor de manifiesto realiza una búsqueda de solicitudes transcodificadas, utiliza una dirección URL de arranque que contiene varios parámetros de consulta. Si ha configurado un entorno de varias CDN, la URL de arranque también deberá contener la variable `ptcdn` parámetro. El servidor de manifiesto utiliza este parámetro para identificar el servidor CDN desde el que se obtiene la versión transcodificada del anuncio.

Para obtener más información, consulte [Compatibilidad con varias CDN](../../~old-creative-repackaging-service/multi-cdn-supportt.md) en la documentación de CRS.
