---
description: Aunque el escenario predeterminado del servicio de reempaquetado creativo (CRS) es utilizar una red de entrega de contenido (CDN), puede implementar recursos CRS en más de una CDN.
title: Compatibilidad con varias CDN para la entrega de anuncios CRS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# Compatibilidad con múltiples CDN para el envío de anuncios CRS {#multiple-cdn-support-for-crs-ad-delivery}

Aunque el escenario predeterminado del servicio de reempaquetado creativo (CRS) es utilizar una red de entrega de contenido (CDN), puede implementar recursos CRS en más de una CDN.

## Requisitos

Puede utilizar varias CDN por los siguientes motivos:

* Requisito de ampliación para eventos de visualización grandes
* Requisito para hacer coincidir la fuente de CDN del recurso CRS con la fuente de CDN del contenido principal.
* Requisito para utilizar una CDN diferente de la CDN predeterminada de CRS (Akamai).

Cuando el servidor de manifiestos realiza una búsqueda de solicitudes transcodificadas, utiliza una URL de arranque que contiene varios parámetros de consulta. Si ha configurado un entorno de varias CDN, la URL de arranque también tendrá que contener el parámetro `ptcdn`. El servidor de manifiesto utiliza este parámetro para identificar el servidor CDN desde el que obtener la versión transcodificada del anuncio.

Para obtener más información, consulte [Compatibilidad con varias CDN](../../~old-creative-repackaging-service/multi-cdn-supportt.md) en la documentación de CRS.
