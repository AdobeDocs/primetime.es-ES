---
title: Usar Ad Insertion en flujo en directo/lineal
description: Uso del Ad Insertion en un flujo en directo/lineal
exl-id: d56ed723-ec72-4bbd-befc-6858c7c9d800
source-git-commit: 1bc2f6c230c262babf2958c32fee31afcad04c2f
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Usar Ad Insertion en flujo en directo/lineal {#ad-insertion-live-linear-stream}

El Ad Insertion de Primetime permite a los editores gestionar situaciones de inserción de anuncios estándar y complejas que se producen durante emisiones en directo/lineales.

## Formatos de referencia admitidos {#cue-formats-supported}

El Ad Insertion de Primetime admite una amplia gama de formatos de referencia estándar y no estándar, incluidos:

* PPP SCTE-35 (marcadores de anuncios mejorados SCTE-35)

* [Especificación de señalización de inserción de programas digitales de Adobe](assets/PrimetimeDigitalProgramInsertionSignalingSpecification.pdf)

* SCTE-35 binario (tanto HLS como DASH)

* Texto SCTE-35 (HLS y GUIÓN)

Póngase en contacto con su representante de asistencia técnica de Primetime para obtener más información u otros formatos de referencia admitidos.

## Compatibilidad con pausa publicitaria parcial {#partial-ad-break-support}

Las pausas publicitarias parciales se pueden utilizar en situaciones en las que un visualizador entra en un flujo en directo/lineal después de haberse iniciado una pausa publicitaria.  Por ejemplo, si un usuario introduce una pausa publicitaria de 2 en la marca de 1, la inserción de una pausa publicitaria parcial garantiza que los anuncios se publiquen en el tiempo restante. Sin la inserción de una pausa publicitaria parcial, no se mostrará ningún anuncio a este visor durante la pausa. El Ad Insertion de Primetime permite la inserción de pausas publicitarias parciales de forma predeterminada si las etiquetas adecuadas están presentes en los flujos de medios.

## Retorno anticipado (salida anticipada del anuncio) {#early-return-early-ad-exit}

Hay casos en los que puede ser necesario volver antes de tiempo desde una pausa publicitaria en un flujo en directo/lineal, como cuando un evento deportivo vuelve repentinamente a la acción. Cada formato de decisión de anuncio contiene una etiqueta para &quot;cue-out&quot; (anuncios) o &quot;cue-in&quot; (contenido).  Si se encuentra una etiqueta de &quot;entrada&quot; antes del final de una pausa publicitaria, el Ad Insertion de Adobe Primetime aceptará la entrada.  Póngase en contacto con el empaquetador de contenido para habilitar la devolución anticipada.
