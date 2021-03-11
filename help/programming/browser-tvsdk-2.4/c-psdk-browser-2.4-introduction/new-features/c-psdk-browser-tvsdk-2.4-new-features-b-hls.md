---
description: El SDK de explorador admite una serie de funciones HLS que puede implementar para agregar funcionalidad a sus aplicaciones de vídeo.
title: Funciones HLS compatibles
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---


# Funciones HLS admitidas {#supported-hls-features}

El SDK de explorador admite una serie de funciones HLS que puede implementar para agregar funcionalidad a sus aplicaciones de vídeo.

* [Reproducción principal de HLS](#hls-core-playback)
* [HLS Funciones de reproducción avanzadas](#hls-advanced-playback)
* [Funciones de protección de contenido HLS](#hls-content-protection)
* [Funciones de inserción de anuncios principales de HLS](#hls-core-ad-insertion)
* [HLS Funciones avanzadas de inserción de anuncios](#hls-advanced-ad-insertion)
* [Integraciones HLS](#hls-integrations)

>[!TIP]
>
>En las tablas de matriz de características que se muestran a continuación, ![icon compatible](assets/supported15.png) significa que la función es compatible con la versión actual.

>[!TIP]
>
>En la columna de Safari &quot;Limitación de plataforma&quot; significa que el caso de uso no es compatible porque esa plataforma no permite la implementación de compatibilidad con ella. En el caso de una inserción, utilice SSAI. Si existen limitaciones de reproducción importantes para usted, fuerce la alternativa al Flash en Safari hasta que la plataforma admita el caso de uso de inserción de publicidad.

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

| Categoría | Tipo de contenido | Función | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Integraciones | VOD + Activo | Integración de VHL de Adobe Analytics | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |

## Funciones de inserción de anuncios avanzada de HLS (CSAI) {#hls-advanced-ad-insertion}

| Categoría | Tipo de contenido | Función | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD | Solo publicidad | No admitido | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Ad Insertion | VOD + Activo | Parámetros de objetivo | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Ad Insertion | VOD + Activo | Política de publicidad personalizada | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |
| Ad Insertion | VOD + Activo | Carga de publicidad diferida | ![icono admitido](assets/supported15.png) | No admitido | Limitación de plataforma |
| Ad Insertion | VOD | Anuncios Companion, Anuncios tipo titular y Anuncios en los que se puede hacer clic | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Ad Insertion | VOD | VPAID 2.0 | SWF | JavaScript | JavaScript |

## Funciones de inserción de anuncios principales de HLS (CSAI) {#hls-core-ad-insertion}

| Categoría | Tipo de contenido | Función | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD + Activo | Anuncio | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Ad Insertion | VOD + Activo | Mid-roll | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |
| Ad Insertion | VOD + Activo | Anuncio | Solo VOD | Solo VOD | Solo VOD |
| Ad Insertion | FER VOD | Resolución de anuncios y comportamientos | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |
| Ad Insertion | VOD + Activo | Política de publicidad predeterminada | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |
| Ad Insertion | VOD + Activo | VAST 2.0/3.0 | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Ad Insertion | VOD + Activo | VMAP 1.0 | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Ad Insertion | VOD + Activo | CRS v3.1 | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |

## Funciones de protección de contenido HLS {#hls-content-protection}

| Categoría | Tipo de contenido | Función | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Protección de contenido | VOD + Activo | AES-128 | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Protección de contenido | VOD + Activo | Ejemplo-AES | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Protección de contenido | VOD | DRM | Acceso a Adobe | No admitido | FairPlay |

## Funciones de reproducción avanzada de HLS {#hls-advanced-playback}

| Categoría | Tipo de contenido | Función | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reproducción | VOD | Reproducción con desplazamiento | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Reproducción | VOD | Reproducción solo de audio | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Reproducción | VOD | Reproducción complicada | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Reproducción | VOD | Suavizar juego de trucos | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |
| Reproducción | VOD + Activo | Análisis de ID3 | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | No admitido |
| Reproducción | VOD + Activo | Compatibilidad con el marcador de discontinuidad | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Reproducción | VOD + Activo | Transmisiones con token | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |
| Reproducción | VOD + Activo | Facturación | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Reproducción | VOD + Activo | Browserify | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |

## Reproducción principal de HLS {#hls-core-playback}

| Categoría | Tipo de contenido | Función | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reproducción | VOD + Activo | Reproducción general (Reproducir, Pausar, Buscar) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Reproducción | FER VOD | Reproducción general (Reproducir, Pausar, Buscar) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Reproducción | VOD + Activo | Tasa de bits adaptable | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Reproducción | VOD + Activo | Subtítulos 608/708 | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Reproducción | VOD + Activo | WebVTT | ![icono admitido](assets/supported15.png) | Solo VOD | Solo VOD |
| Reproducción | VOD + Activo | Error de manifiesto | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Reproducción | VOD + Activo | Failover avanzado | ![icono admitido](assets/supported15.png) | Solo VOD | Limitación de plataforma |
| Reproducción | VOD + Activo | Notificaciones de QoS y del reproductor | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Compatibilidad limitada con QoS |
| Reproducción | VOD + Activo | Compatibilidad con encabezados de cookie | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |
| Reproducción | VOD + Activo | Configuración de parámetros de control de búfer | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |
| Reproducción | VOD + Activo | Establecer controles de velocidad de bits adaptables | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |
| Reproducción | VOD + Activo | Etiquetas personalizadas | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |
| Reproducción | VOD + Activo | Audio de enlace tardío | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |
| Reproducción | VOD + Activo | 302 redireccionamiento | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |