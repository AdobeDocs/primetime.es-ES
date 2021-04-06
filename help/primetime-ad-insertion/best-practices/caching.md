---
title: Almacenamiento en caché
description: Almacenamiento en caché
copied-description: true
exl-id: c12c2345-db55-468a-b4b5-5a9e1364a46d
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Almacenamiento en caché HTTP {#caching}

De forma predeterminada, el Ad Insertion de Primetime respeta los encabezados de control de caché HTTP al recuperar los elementos creativos y el contenido de los anuncios.  Esto puede reducir drásticamente la cantidad de solicitudes de red necesarias para que Primetime Ad Insertion realice a la CDN en todos los clientes.  Para el almacenamiento en caché, Adobe recomienda la siguiente configuración y implica enviar el encabezado HTTP `max-age` desde su CDN.  Póngase en contacto con su representante de CDN para habilitar estos encabezados en sus flujos de vídeo y flujos de anuncios.

## Para contenido en directo/lineal {#caching-live-linear-content}

* Manifiesto maestro: 24 horas, o Cache-Control: max-age=86400
* Manifiesto de contenidos: 1 segundo, o Cache-Control: max-age=1

## Para contenido de VOD {#caching-vod-content}

* Manifiesto maestro: 24 horas, o Cache-Control: max-age=86400
* Manifiesto de contenidos: 24 horas, o Cache-Control: max-age=86400
