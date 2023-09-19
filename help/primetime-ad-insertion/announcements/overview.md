---
title: Anuncios de Ad Insertion de Adobe Primetime
description: Anuncios sobre versiones recientes de funcionalidades y otras noticias relacionadas sobre Primetime Ad Insertion
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Anuncios de Ad Insertion de Primetime

## Reducción de errores de publicidad programáticos mediante tiempos de espera de resolución de publicidad

Publicado el 1 de diciembre de 2020

El Adobe se centra en ayudar a nuestros clientes Ad Insertion de Primetime a maximizar la monetización de su inventario de anuncios. Prestamos especial atención a la reducción de las complejidades del cumplimiento de la demanda programática, que representa más de tres cuartas partes del gasto en publicidad digital de vídeo de EE. UU. según el experto en marketing electrónico. La venta programática permite a los editores maximizar la demanda de su inventario de anuncios, lo que conduce a mayores tasas de llenado y rendimiento. Pero también aumenta la exposición a errores de publicidad como respuestas VAST mal formadas, errores HTTP y otros que pueden llevar a la pérdida de ingresos y/o experiencias pobres del visualizador.

Un problema común es la lentitud de las respuestas publicitarias de los socios programáticos. Normalmente, las transacciones de anuncios de programación se producen en milisegundos. Sin embargo, a veces una única fuente de demanda puede tardar demasiado en responder. Un retraso de un solo proveedor puede afectar a todo el proceso de publicación de anuncios, lo que provoca pantallas en blanco temporales para el visualizador, ranuras de anuncios sin rellenar o, en casos extremos, la necesidad de reiniciar un flujo de vídeo. Desafortunadamente, identificar y evitar las fuentes de demanda lentas es un desafío importante.

Para solucionar este problema, Adobe ha agregado nuevas herramientas al Ad Insertion de Primetime que permiten a los clientes establecer restricciones temporales para la resolución de anuncios. La configuración de estas reglas provoca que las fuentes de demanda lentas se omitan automáticamente, lo que garantiza que los reproductores de vídeo obtengan respuestas publicitarias de forma oportuna. Esto permite a los editores limitar en gran medida las interrupciones de las fuentes de demanda lenta, lo que les ayuda a maximizar las tasas de llenado de inventario y ofrecer experiencias de visualización ininterrumpidas y de calidad de TV.

Para habilitar el tiempo de espera de resolución de anuncio en el Ad Insertion de Primetime, modifique las API de arranque para incluir el parámetro ptadtimeout (duration en milisegundos).  Las solicitudes de publicidad que no se completen antes de la duración del tiempo de espera no se vincularán (se procesarán los anuncios de reserva).
