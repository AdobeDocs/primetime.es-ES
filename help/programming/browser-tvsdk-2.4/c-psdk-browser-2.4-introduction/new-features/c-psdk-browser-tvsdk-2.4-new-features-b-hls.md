---
description: El SDK TVSDK del explorador admite una serie de funciones HLS que se pueden implementar para agregar funcionalidad a las aplicaciones de vídeo.
seo-description: El SDK TVSDK del explorador admite una serie de funciones HLS que se pueden implementar para agregar funcionalidad a las aplicaciones de vídeo.
seo-title: Funciones HLS admitidas
title: Funciones HLS admitidas
uuid: 033d81f8-cea4-4687-b2fb-1524d9164d39
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 0%

---


# Funciones HLS admitidas {#supported-hls-features}

El SDK TVSDK del explorador admite una serie de funciones HLS que se pueden implementar para agregar funcionalidad a las aplicaciones de vídeo.

* [Reproducción de HLS Core](#hls-core-playback)
* [Funciones de reproducción avanzadas de HLS](#hls-advanced-playback)
* [Funciones de protección de contenido HLS](#hls-content-protection)
* [Funciones de inserción de anuncios principales de HLS](#hls-core-ad-insertion)
* [HLS Funciones avanzadas de inserción de anuncios](#hls-advanced-ad-insertion)
* [Integraciones HLS](#hls-integrations)

>[!TIP]
>
>En las tablas de la matriz de características que se muestran a continuación, ![icono admitido](assets/supported15.png) significa que la función se admite en la versión actual.

>[!TIP]
>
>En la columna Safari &quot;Limitación de plataforma&quot; significa que el caso de uso no se admite porque esa plataforma no permite la implementación de la compatibilidad con ella. En caso de inserción, utilice SSAI. Si existen limitaciones de reproducción importantes para usted, fuerce la alternativa a Flash en Safari hasta que la plataforma admita el caso de uso de inserción de publicidad.

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
| Integraciones | VOD + Activo | Integración con Adobe Analytics VHL | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |

## Funciones avanzadas de inserción de anuncios HLS (CSAI) {#hls-advanced-ad-insertion}

| Categoría | Tipo de contenido | Función | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD | Solo publicidad | No admitido | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Ad Insertion | VOD + Activo | Parámetros de objetivo | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Ad Insertion | VOD + Activo | Directiva de publicidad personalizada | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |
| Ad Insertion | VOD + Activo | Carga de anuncios diferida | ![icono admitido](assets/supported15.png) | No admitido | Limitación de plataforma |
| Ad Insertion | VOD | Publicidades complementarias, publicidades tipo titular y publicidades en las que se puede hacer clic | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Ad Insertion | VOD | VPAID 2.0 | SWF | JavaScript | JavaScript |

## Funciones de inserción de anuncios principales de HLS (CSAI) {#hls-core-ad-insertion}

| Categoría | Tipo de contenido | Función | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD + Activo | Anteponer | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Ad Insertion | VOD + Activo | Mid-roll | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |
| Ad Insertion | VOD + Activo | Post-roll | Solo VOD | Solo VOD | Solo VOD |
| Ad Insertion | FER VOD | Resolución y comportamientos de publicidad | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |
| Ad Insertion | VOD + Activo | Directiva de publicidad predeterminada | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |
| Ad Insertion | VOD + Activo | VAST 2.0/3.0 | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Ad Insertion | VOD + Activo | VMAP 1.0 | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Ad Insertion | VOD + Activo | CRS v3.1 | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |

## Funciones de protección de contenido HLS {#hls-content-protection}

| Categoría | Tipo de contenido | Función | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Protección del contenido | VOD + Activo | AES-128 | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Protección del contenido | VOD + Activo | Sample-AES | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Protección del contenido | VOD | DRM | Acceso a Adobe | No admitido | FairPlay |

## Funciones de reproducción avanzada de HLS {#hls-advanced-playback}

| Categoría | Tipo de contenido | Función | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reproducción | VOD | Reproducción en desplazamiento | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Reproducción | VOD | Reproducción solo de audio | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Reproducción | VOD | Juego de trucos | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Reproducción | VOD | Juego de trucos suave | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |
| Reproducción | VOD + Activo | Análisis de ID3 | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | No admitido |
| Reproducción | VOD + Activo | Compatibilidad con los marcadores de discontinuidad | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Reproducción | VOD + Activo | Flujos con autentificación | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |
| Reproducción | VOD + Activo | Facturación | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Reproducción | VOD + Activo | Explorar | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |

## Reproducción principal HLS {#hls-core-playback}

| Categoría | Tipo de contenido | Función | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Reproducción | VOD + Activo | Reproducción general (Reproducir, Pausa, Buscar) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Reproducción | FER VOD | Reproducción general (Reproducir, Pausa, Buscar) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Reproducción | VOD + Activo | Velocidad de bits adaptable | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Reproducción | VOD + Activo | Subtítulos 608/708 | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Reproducción | VOD + Activo | WebVTT | ![icono admitido](assets/supported15.png) | Solo VOD | Solo VOD |
| Reproducción | VOD + Activo | Conmutación por error de manifiesto | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) |
| Reproducción | VOD + Activo | Failover avanzado | ![icono admitido](assets/supported15.png) | Solo VOD | Limitación de plataforma |
| Reproducción | VOD + Activo | Notificaciones de QoS y reproductor | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Compatibilidad limitada con QoS |
| Reproducción | VOD + Activo | Compatibilidad con encabezados de cookie | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |
| Reproducción | VOD + Activo | Configuración de parámetros de control de búfer | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |
| Reproducción | VOD + Activo | Establecer controles de velocidad de bits adaptables | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |
| Reproducción | VOD + Activo | Etiquetas personalizadas | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |
| Reproducción | VOD + Activo | Enlace tardío de audio | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |
| Reproducción | VOD + Activo | 302 redireccionamiento | ![icono admitido](assets/supported15.png) | ![icono admitido](assets/supported15.png) | Limitación de plataforma |