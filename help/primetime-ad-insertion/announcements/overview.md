---
title: Anuncios del Ad Insertion de Adobe Primetime
description: Anuncios sobre versiones recientes de funcionalidades y otras noticias relacionadas sobre Primetime Ad Insertion
translation-type: tm+mt
source-git-commit: d8fde0d03bea85b3fefcfa5dcbfddee76b17de03
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---


# Anuncios del Ad Insertion de Primetime

## Reducción de los errores de publicidad programática mediante tiempos de espera de resolución de publicidad

Publicado el 1 de diciembre de 2020

El Adobe se centra en ayudar a nuestros clientes Ad Insertion de Primetime a maximizar la monetización de su inventario de anuncios. Prestamos especial atención a la reducción de las complejidades de satisfacer la demanda programática, que representa más de las tres cuartas partes del gasto en publicidad de vídeo digital de EE. UU. según eMarketer. La venta mediante programación permite a los editores maximizar la demanda de su inventario de anuncios, lo que produce mayores tasas de relleno y rendimiento. Sin embargo, también aumenta la exposición a errores de publicidad, como respuestas VAST mal formadas, errores HTTP y otros que pueden provocar pérdidas de ingresos o malas experiencias del visor.

Un problema común es la lentitud de las respuestas publicitarias de los asociados programáticos. Normalmente, las transacciones publicitarias programáticas se producen en milisegundos. Sin embargo, a veces una única fuente de demanda puede tardar una cantidad excesiva de tiempo en responder. Un retraso de un solo proveedor puede afectar a todo el proceso de realización de publicidad, lo que provoca pantallas vacías temporales para el visor, ranuras de anuncios sin rellenar o, en casos extremos, la necesidad de reiniciar un flujo de vídeo. Desafortunadamente, identificar y evitar las fuentes de demanda lentas es un desafío importante.

Para solucionar este problema, Adobe ha agregado nuevas herramientas al Ad Insertion de Primetime que permiten a los clientes establecer restricciones de tiempo para la resolución de anuncios. La configuración de estas reglas hace que las fuentes de demanda lenta se omitan automáticamente, lo que garantiza que los reproductores de vídeo obtengan respuestas de publicidad de forma oportuna. Esto permite a los editores limitar en gran medida las interrupciones causadas por fuentes de demanda lenta, lo que les ayuda a maximizar las tasas de llenado de inventario y a ofrecer experiencias de visualización ininterrumpidas y de calidad de TV.

Para habilitar el tiempo de espera de resolución de publicidad en el Ad Insertion de Primetime, modifique las API de arranque para incluir el parámetro ptadtimeout (duración en milisegundos).  Las solicitudes de publicidad que no se completen antes de que expire el tiempo de espera no se vincularán (se procesarán los anuncios de reserva).