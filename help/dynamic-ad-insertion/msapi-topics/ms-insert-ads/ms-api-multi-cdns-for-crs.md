---
description: Aunque el escenario predeterminado del servicio de reempaquetado creativo (CRS) es usar una red de Envío de contenido (CDN), puede implementar recursos CRS en más de una CDN.
seo-description: Aunque el escenario predeterminado del servicio de reempaquetado creativo (CRS) es usar una red de Envío de contenido (CDN), puede implementar recursos CRS en más de una CDN.
seo-title: Compatibilidad de varios CDN con CRS y envío
title: Compatibilidad de varios CDN con CRS y envío
uuid: c5557a38-aa49-4161-bb58-3e8dff9a4d64
translation-type: tm+mt
source-git-commit: f327b45de7e482dcb25407659846b2098f1fd49d
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# Compatibilidad con varios CDN para el envío de anuncios de CRS {#multiple-cdn-support-for-crs-ad-delivery}

Aunque el escenario predeterminado del servicio de reempaquetado creativo (CRS) es usar una red de Envío de contenido (CDN), puede implementar recursos CRS en más de una CDN.

## Requisitos

Puede utilizar varias CDN por las siguientes razones:

* Requisito de ampliación para grandes eventos de visualización
* Requisito para hacer coincidir el origen CDN del recurso CRS con el origen CDN del contenido principal.
* Requisito de usar una CDN diferente de la CDN predeterminada de CRS (Akamai).

Cuando el servidor de manifiesto realiza una búsqueda de solicitudes transcodificadas, utiliza una URL de arranque que contiene varios parámetros de consulta. Si ha configurado un entorno multi-CDN, la dirección URL de arranque también deberá contener el parámetro `ptcdn`. El servidor de manifiesto utiliza este parámetro para identificar el servidor CDN desde el que se obtiene la versión transcodificada de la publicidad.

Para obtener más información, consulte [Compatibilidad con múltiples CDN](../../creative-repackaging-service/multi-cdn-supportt.md) en la documentación de CRS.
