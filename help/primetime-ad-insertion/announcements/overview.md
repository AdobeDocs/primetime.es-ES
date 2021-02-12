---
title: Anuncios de Adobe Primetime Ad Insertion
seo-title: Anuncios de Adobe Primetime Ad Insertion
description: Anuncios sobre las últimas versiones de funciones y otras noticias relacionadas con Primetime Ad Insertion
seo-description: Anuncios sobre las últimas versiones de funciones y otras noticias relacionadas con Primetime Ad Insertion
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# Anuncios del Ad Insertion Primetime

## Reducción de los errores de publicidad programática mediante tiempos de espera de resolución de publicidad

Publicado el 1 de diciembre de 2000

Adobe se centra en ayudar a nuestros clientes de Primetime Ad Insertion a maximizar la monetización de su inventario de anuncios. Prestamos especial atención a la reducción de las complejidades de satisfacer la demanda programática, que representa más de las tres cuartas partes de la inversión en publicidad de vídeo digital de EE.UU. según eMarketer. La venta mediante programación permite a los editores maximizar la demanda de su inventario publicitario, lo que permite aumentar las tasas de relleno y el rendimiento. Sin embargo, también aumenta la exposición a errores de publicidad, como respuestas VAST mal formadas, errores HTTP y otros que pueden provocar pérdidas de ingresos y/o malas experiencias de visor.

Un problema común es la lentitud y las respuestas de los asociados en los programas. Generalmente, las transacciones publicitarias programáticas se producen en milisegundos. Sin embargo, a veces una única fuente de demanda puede tardar una cantidad excesiva de tiempo en responder. Un retraso de un único proveedor puede afectar a todo el proceso de despacho de la publicidad, lo que provoca pantallas vacías temporales para el visor, ranuras de anuncios sin rellenar o, en casos extremos, la necesidad de reiniciar un flujo de vídeo. Desafortunadamente, identificar y evitar las fuentes de demanda lentas es un gran desafío.

Para solucionar este problema, Adobe ha agregado nuevas herramientas al Ad Insertion Primetime que permiten a los clientes establecer restricciones de tiempo para la resolución de anuncios. La configuración de estas reglas hace que las fuentes de demanda lenta se omitan automáticamente, lo que garantiza que los reproductores de vídeo obtengan respuestas de publicidad de manera oportuna. Esto permite a los editores limitar en gran medida las interrupciones provenientes de fuentes de demanda lenta, ayudándoles a maximizar las tasas de relleno de inventario y a ofrecer experiencias de visualización ininterrumpidas de calidad de TV.

Para habilitar el tiempo de espera de resolución de publicidad en Primetime Ad Insertion, modifique las API de arranque para incluir el parámetro ptadtimeout (duración en milisegundos).  Las solicitudes de publicidad que no se completen antes de la duración del tiempo de espera no se vincularán (se procesarán las publicidades de reserva).