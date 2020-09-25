---
title: API de Bootstrap
description: null
translation-type: tm+mt
source-git-commit: aa43834fea161c537c448b7616c9bd8f779d1a74
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---


# API de Bootstrap {#bootstrap-api}

Parámetros requeridosGenerar un bootstrap

## Descripción del parámetro {#parameter-description}

| parámetro | description | formatos |
|---|---|---|
| pabimode | Habilita la inserción [de pausa publicitaria](ad-insertion-live-linear-stream.md#partial-ad-break-support) parcial para flujos en directo. Valores posibles:true para habilitar la deshabilitación (predeterminado deshabilitado) | HLS/DASH |
| ptadwindow | Duración (en segundos) de la ventana retrospectiva y de toma de decisiones: cuánto tiempo atrás el Ad Insertion de Primetime buscará señales publicitarias cuando un usuario de DVR se una al flujo. Un valor de cero deshabilitará la toma de decisiones de anuncio en el manifiesto inicial, y la decisión se reanudará solo después de la primera actualización. Este parámetro es útil para desactivar la inserción de anuncios en sesiones que solo pueden durar unos segundos (es decir, voltear canal). Valores posibles:cadena numérica 0-1800 (valor predeterminado 1800) | Sólo HLS |
| ptassetid | ID única del contenido que el editor asigna y mantiene.  Necesario cuando se utiliza junto con el escalador de anuncios de Akamai. | HLS/DASH |
| ptcdn | Lista de uno o más CDN para alojar recursos transcodificados. Para obtener más información, consulte Compatibilidad con [Multi CDN](multi-cdn-support.md). Valores posibles: akamai, nivel3, lnw (redes limelight), comcastDe forma predeterminada, se utilizan CDN de Ad Insertion Primetime | HLS/DASH |
| ptcueformat | Formato especificado de las etiquetas para realizar la toma de decisiones de publicidad (por ejemplo, scte35). Valores posibles: dpisimple, dpiscte35, elemental Para formatos de cue personalizados, póngase en contacto con el representante de cuentas técnicas para el valor que se usará en el caso de uso | HLS/DASH |
| ptfailover | Indica al servidor de manifiesto que identifica los flujos principales y de conmutación por error especificados en la lista de reproducción maestra y que los trata como conjuntos desunidos. Esto facilita la conmutación por error y evita errores de temporización. (Solo para dispositivos Apple HLS). Para obtener más información, consulte [Facilitación del cambio de reproductor HLS](hls-switching-to-failover.md) | Sólo HLS |
| ptmulticall | Si se habilita, se realiza una solicitud de publicidad independiente para cada valor encontrado en un recurso de VOD.  De forma predeterminada, el Ad Insertion de Primetime intentará recopilar toda la información de disponibilidad y enviarla al servidor de publicidad en una solicitud. Valores posibles:true para habilitar la deshabilitación (predeterminado deshabilitado) | HLS/DASH |
| pttagds | Permite la inyección de etiquetas EXT-X-DISCONTINUITY-SEQUENCE en encabezados HLS.Valores posibles:true para habilitar la deshabilitación (deshabilitado de forma predeterminada) | Sólo HLS |
| ptlínea | Una cadena que contiene la línea de tiempo deseada para la ubicación y el contenido de la publicidad, que anula los saltos de publicidad en el flujo de contenido. [ Consulte Formato de línea de tiempo VOD ] | HLS/DASH |
| pttoken | Habilita esquemas de protección de token de autorización de fragmento de contenido/segmento para CDNs Valores posibles: akamai, llnw (limelight), ctl (centurylink) (la tokenización predeterminada está deshabilitada) | HLS/DASH |
| pttrackingmode | Habilitar esquemas de seguimiento de anuncios:Valores posibles:sencillos para el seguimiento de anuncios en el lado del clienteSst para el seguimiento de anuncios en el lado del servidor simple para el seguimiento de anuncios híbridos en el cliente/servidor (de forma predeterminada, no se realiza ningún seguimiento de anuncios) | HLS/DASH |
| pttrackingversion |  |  |
| ptadtimeout (como en 20.9.2) |  |  |
| ptparallelstream (como en 20.9.3) |  |  |
