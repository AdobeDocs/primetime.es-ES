---
description: El TVSDK del explorador admite una serie de funciones HLS que puede implementar para agregar funcionalidad a las aplicaciones de vídeo.
title: Funciones HLS compatibles
exl-id: 111a6683-fb5c-4f0a-8665-5b1aab77056c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# Funciones HLS compatibles {#supported-hls-features}

El TVSDK del explorador admite una serie de funciones HLS que puede implementar para agregar funcionalidad a las aplicaciones de vídeo.

* [Reproducción principal de HLS](#hls-core-playback)
* [Funciones de reproducción avanzadas de HLS](#hls-advanced-playback)
* [Funciones de protección de contenido HLS](#hls-content-protection)
* [Funciones de inserción de publicidad principal de HLS](#hls-core-ad-insertion)
* [Funciones avanzadas de inserción de publicidad de HLS](#hls-advanced-ad-insertion)
* [Integraciones HLS](#hls-integrations)

>[!TIP]
>
>En las tablas de la matriz de características siguientes, ![icono compatible](assets/supported15.png) significa que la función es compatible con la versión actual.

>[!TIP]
>
>En la columna de Safari, &quot;Limitación de plataforma&quot; significa que el caso de uso no es compatible porque esa plataforma no permite la implementación de compatibilidad con ella. En el caso de una inserción, utilice SSAI. Si existen limitaciones de reproducción importantes para usted, force la alternativa al Flash en Safari hasta que la plataforma admita el caso de uso de inserción de publicidad.

<!--<a id="section_9FB9193D5763448CB228B96164661738"></a>-->

Se admiten las siguientes funciones:

<!-- 

Removed Nielsen row 
<table id="table_D9E2D82992554905A0A551CC71AFA189"> 
 <title>HLS integrations</title> 
 <tgroup cols="6"> 
  <colspec colnum="1" colname="col1" colwidth="*" /> 
  <colspec colnum="2" colname="col2" colwidth="*" /> 
  <colspec colnum="3" colname="col3" colwidth="*" /> 
  <colspec colnum="4" colname="col4" colwidth="*" /> 
  <colspec colnum="5" colname="col5" colwidth="*" /> 
  <colspec colnum="6" colname="col7" colwidth="*" /> 
  <thead> 
   <tr> 
    <th colname="col1" morerows="1" class="entry"> Category </th> 
    <th colname="col2" morerows="1" class="entry"> Content type </th> 
    <th colname="col3" morerows="1" class="entry"> Feature </th> 
    <th colname="col4" morerows="1" class="entry"> Flash </th> 
    <th namest="col5" nameend="col7" class="entry"> HTML5 </th> 
   </tr> 
   <tr> 
    <th colname="col5" class="entry"> FF, IE, Chrome, Android Chrome </th> 
    <th colname="col7" class="entry"> Safari, iOS Safari </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Adobe Analytics VHL integration </td> 
    <td colname="col4">![supported icon](assets/supported15.png) </td> 
    <td colname="col5">![supported icon](assets/supported15.png) </td> 
    <td colname="col7">![supported icon](assets/supported15.png) </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Nielsen support </td> 
    <td colname="col4">![supported icon](assets/supported15.png) </td> 
    <td colname="col5">![supported icon](assets/supported15.png) </td> 
    <td colname="col7">![supported icon](assets/supported15.png) </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

 -->

## Integraciones HLS {#hls-integrations}

| Categoría | Tipo de contenido | Función | Flash | HTML 5: FF, IE, Chrome, Android Chrome | HTML 5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Integraciones | VOD + Activo | Integración de VHL de Adobe Analytics | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) |

## Funciones avanzadas de inserción de publicidad de HLS (CSAI) {#hls-advanced-ad-insertion}

| Categoría | Tipo de contenido | Función | Flash | HTML 5: FF, IE, Chrome, Android Chrome | HTML 5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD | Solo anuncio | No compatible | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) |
| Ad Insertion | VOD + Activo | Parámetros de segmentación | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) |
| Ad Insertion | VOD + Activo | Política de publicidad personalizada | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | Limitación de plataforma |
| Ad Insertion | VOD + Activo | Carga diferida de publicidad | ![icono compatible](assets/supported15.png) | No compatible | Limitación de plataforma |
| Ad Insertion | VOD | Anuncios complementarios, anuncios de banner y anuncios en los que se puede hacer clic | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) |
| Ad Insertion | VOD | VPAID 2.0 | SWF | JavaScript | JavaScript |

## Funciones de inserción de anuncios principales de HLS (CSAI) {#hls-core-ad-insertion}

| Categoría | Tipo de contenido | Función | Flash | HTML 5: FF, IE, Chrome, Android Chrome | HTML 5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD + Activo | Pre-roll | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) |
| Ad Insertion | VOD + Activo | Mid-roll | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | Limitación de plataforma |
| Ad Insertion | VOD + Activo | Post-roll | Solo VOD | Solo VOD | Solo VOD |
| Ad Insertion | VOD FER | Resolución y comportamientos de anuncios | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | Limitación de plataforma |
| Ad Insertion | VOD + Activo | Política de publicidad predeterminada | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | Limitación de plataforma |
| Ad Insertion | VOD + Activo | VAST 2.0/3.0 | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) |
| Ad Insertion | VOD + Activo | VMAP 1.0 | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) |
| Ad Insertion | VOD + Activo | CRS v3.1 | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) |

## Funciones de protección de contenido HLS {#hls-content-protection}

| Categoría | Tipo de contenido | Función | Flash | HTML 5: FF, IE, Chrome, Android Chrome | HTML 5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Protección de contenido | VOD + Activo | AES-128 | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) |
| Protección de contenido | VOD + Activo | Sample-AES | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) |
| Protección de contenido | VOD | DRM | Acceso a Adobe | No compatible | FairPlay |

## Funciones de reproducción avanzadas de HLS {#hls-advanced-playback}

| Categoría | Tipo de contenido | Función | Flash | HTML 5: FF, IE, Chrome, Android Chrome | HTML 5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reproducción | VOD | Reproducción en offset | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) |
| Reproducción | VOD | Reproducción solo de audio | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) |
| Reproducción | VOD | Juego de trucos | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) |
| Reproducción | VOD | Jugar con trucos suaves | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | Limitación de plataforma |
| Reproducción | VOD + Activo | Análisis de ID3 | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | No compatible |
| Reproducción | VOD + Activo | Compatibilidad con marcadores de discontinuidad | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) |
| Reproducción | VOD + Activo | Flujos tokenizados | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | Limitación de plataforma |
| Reproducción | VOD + Activo | Factura | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) |
| Reproducción | VOD + Activo | Browserify | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) |

## Reproducción principal de HLS {#hls-core-playback}

| Categoría | Tipo de contenido | Función | Flash | HTML 5: FF, IE, Chrome, Android Chrome | HTML 5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reproducción | VOD + Activo | Reproducción general (reproducir, pausar, buscar) | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) |
| Reproducción | VOD FER | Reproducción general (reproducir, pausar, buscar) | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) |
| Reproducción | VOD + Activo | Velocidad de bits adaptable | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) |
| Reproducción | VOD + Activo | 608/708 subtítulos | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) |
| Reproducción | VOD + Activo | WebVTT | ![icono compatible](assets/supported15.png) | Solo VOD | Solo VOD |
| Reproducción | VOD + Activo | Conmutación por error de manifiesto | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) |
| Reproducción | VOD + Activo | Conmutación por error avanzada | ![icono compatible](assets/supported15.png) | Solo VOD | Limitación de plataforma |
| Reproducción | VOD + Activo | QoS y notificaciones del reproductor | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | Compatibilidad con QoS limitada |
| Reproducción | VOD + Activo | Compatibilidad con encabezados de cookie | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | Limitación de plataforma |
| Reproducción | VOD + Activo | Estableciendo parámetros de control de búfer | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | Limitación de plataforma |
| Reproducción | VOD + Activo | Establecer controles de velocidad de bits adaptables | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | Limitación de plataforma |
| Reproducción | VOD + Activo | Etiquetas personalizadas | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | Limitación de plataforma |
| Reproducción | VOD + Activo | Audio de enlace tardío | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | Limitación de plataforma |
| Reproducción | VOD + Activo | Redirección 302 | ![icono compatible](assets/supported15.png) | ![icono compatible](assets/supported15.png) | Limitación de plataforma |
