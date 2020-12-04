---
title: Usar Ad Insertion en flujo en directo/lineal
description: Uso del Ad Insertion en el flujo en directo/lineal
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# Usar Ad Insertion en flujo en directo/lineal {#ad-insertion-live-linear-stream}

Primetime Ad Insertion ofrece a los editores la capacidad de gestionar situaciones de inserción de anuncios estándar y complejas que se producen durante flujos en directo o lineales.

## Formatos de referencia admitidos {#cue-formats-supported}

Primetime Ad Insertion admite una amplia gama de formatos de señal estándar y no estándar, entre los que se incluyen:

* PPP SCTE-35 (marcadores de anuncios mejorados con SCTE-35)

* [Especificación de señalización de inserción de Programa digital de Adobe](https://www.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeDigitalProgramInsertionSignalingSpecification.pdf)

* Binary SCTE-35

Póngase en contacto con su representante de soporte técnico de Primetime para obtener más detalles u otros formatos de referencia admitidos.

## Compatibilidad con Salto de publicidad parcial {#partial-ad-break-support}

Las pausas de publicidad parciales se pueden utilizar en situaciones en las que un visor entra en un flujo en directo o lineal después de iniciarse una pausa publicitaria.  Por ejemplo: si un visor introduce una pausa publicitaria de 2:00 en la marca 1:00, la inserción de una pausa publicitaria parcial garantiza que los anuncios se mostrarán en el tiempo restante. Sin la inserción de pausa publicitaria parcial, no se enviarían anuncios a este visor durante la pausa. El Ad Insertion Primetime habilita la inserción de pausa publicitaria parcial de forma predeterminada si las etiquetas correspondientes están presentes en los flujos multimedia.

## Retorno anticipado (salida anticipada de publicidad) {#early-return-early-ad-exit}

Hay casos en los que puede ser necesario volver antes de una pausa publicitaria en un flujo en directo o lineal, como cuando un evento deportivo vuelve repentinamente a la acción. Cada formato de decisión de publicidad contiene una etiqueta para &quot;cue-out&quot; (anuncios) o &quot;cue-in&quot; (contenido). Si se encuentra una etiqueta de &quot;cue-in&quot; antes del final de una pausa publicitaria, el Ad Insertion de Adobe Primetime respetará el cue-in. Póngase en contacto con el empaquetador de contenido para activar el retorno anticipado.
