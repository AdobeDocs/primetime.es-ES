---
description: El SDK TVSDK del explorador admite una serie de funciones DASH que se pueden implementar para agregar funcionalidad a las aplicaciones de vídeo.
seo-description: El SDK TVSDK del explorador admite una serie de funciones DASH que se pueden implementar para agregar funcionalidad a las aplicaciones de vídeo.
seo-title: Funciones compatibles de DASH
title: Funciones compatibles de DASH
uuid: 299516a4-09ed-4b8a-b0bf-a04f204f385a
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---


# Funciones compatibles de DASH{#supported-dash-features}

El SDK TVSDK del explorador admite una serie de funciones DASH que se pueden implementar para agregar funcionalidad a las aplicaciones de vídeo.

* [Funciones de reproducción de DASH Core](#dash-core-playback)
* [Funciones de reproducción avanzadas de DASH](#dash-advanced-playback)
* [Funciones de protección de contenido DASH](#dash-content-protection)
* [Funciones de inserción de anuncios de DASH Core](#dash-core-ad-insertion)
* [Funciones avanzadas de inserción de anuncios de DASH](#dash-advanced-insertion-features)
* [Integraciones de DASH](#dash-integrations)

>[!TIP]
>
>En las tablas de características siguientes,  ![](assets/supported15.png)
>significa que la función es compatible con la versión actual.

Se admiten las siguientes funciones:

<!-- 

<table id="table_lrb_p2g_xx"> 
 <title>DASH integrations</title> 
 <tgroup cols="4"> 
  <colspec colnum="1" colname="col1" colwidth="*" /> 
  <colspec colnum="2" colname="col2" colwidth="*" /> 
  <colspec colnum="3" colname="col3" colwidth="*" /> 
  <colspec colnum="4" colname="col6" colwidth="*" /> 
  <thead> 
   <tr> 
    <th colname="col1" class="entry"> Category </th> 
    <th colname="col2" class="entry"> Content type </th> 
    <th colname="col3" class="entry"> Feature </th> 
    <th colname="col6" align="center" class="entry"> 
     <lines>
       HTML5 FF, IE, Chrome, Android Chrome
     </lines> </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Adobe Analytics VHL integration </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_14D9248BD1D8410E83AD27DB4AB3B6ED" /> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Nielsen support </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_EFA853CB763446B3B37F2CF6BCC53EE1" /> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Billing </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_B3A4E5937CEC4052977C08767219BC2B" /> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Browserify </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_3330E81B86C84AD391AEBFDFE911A47F" /> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

 -->

## Integraciones de DASH {#dash-integrations}

| Categoría | Tipo de contenido | Función | HTML5 FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| Integraciones | VOD + Activo | Integración con Adobe Analytics VHL | ![](assets/supported15.png) |
| Integraciones | VOD + Activo | Facturación | ![](assets/supported15.png) |
| Integraciones | VOD + Activo | Explorar | ![](assets/supported15.png) |

## Funciones avanzadas de inserción de anuncios DASH (CSAI) {#dash-advanced-insertion-features}

| Categoría | Tipo de contenido | Función | HTML5 FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| Ad Insertion | VOD | Solo publicidad | No admitido |
| Ad Insertion | VOD | Parámetros de objetivo | Solo VOD |
| Ad Insertion | VOD | Parámetros personalizados | Solo VOD |
| Ad Insertion | VOD + Activo | Directiva de publicidad personalizada | No admitido |
| Ad Insertion | VOD + Activo | Carga de anuncios diferida | No admitido |
| Ad Insertion | VOD | Publicidades complementarias, publicidades tipo titular y publicidades en las que se puede hacer clic | No admitido |
| Ad Insertion | VOD | VPAID 2.0 | No admitido |

## Funciones de inserción de anuncios principales de DASH (CSAI) {#dash-core-ad-insertion}

| Categoría | Tipo de contenido | Función | HTML5 FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| Ad Insertion | VOD + Activo | Anteponer | Solo VOD |
| Ad Insertion | VOD + Activo | Mid-roll | Solo VOD |
| Ad Insertion | VOD + Activo | Post-roll | Solo VOD |
| Ad Insertion | FER VOD | Resolución y comportamientos de publicidad | No admitido |
| Ad Insertion | VOD + Activo | Directiva de publicidad predeterminada | Solo VOD |
| Ad Insertion | VOD + Activo | VAST 2.0/3.0 | Solo VOD |
| Ad Insertion | VOD + Activo | VMAP 1.0 | Solo VOD |
| Ad Insertion | VOD + Activo | CRS v3.1 | Solo VOD |

## Funciones de protección de contenido DASH {#dash-content-protection}

<table id="table_hrb_p2g_xx">  
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Categoría </th> 
   <th colname="col2" class="entry"> Tipo de contenido </th> 
   <th colname="col3" class="entry"> Función </th> 
   <th colname="col6" class="entry"> HTML5 FF, IE, Chrome, Android Chrome</th>
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Protección del contenido </td> 
   <td colname="col2"> VOD + Activo </td> 
   <td colname="col3"> AES-128 </td> 
   <td colname="col6"> No admitido </td>
  </tr> 
  <tr> 
   <td colname="col1"> Protección del contenido </td> 
   <td colname="col2"> VOD + Activo </td> 
   <td colname="col3"> Sample-AES </td> 
   <td colname="col6"> No admitido </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Protección del contenido </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3"> DRM </td> 
   <td colname="col6"> 
    <ul id="ul_irb_p2g_xx"> 
     <li id="li_C4643F2978BC4C8ABDB3E6C72C75A468">Amplia en 
      <ul id="ul_7047EA49AA3F40FE8F90E0ED6C028D83"> 
       <li id="li_B575735388D74D789D56BF373A470A6D">Chrome </li> 
       <li id="li_855146E4AC3A48E69B65F0022E1C0156">Firefox 47+ </li> 
       <li id="li_BC06B0A6EAAC4FC991C713775A8BB4DA">Chromecast </li> 
      </ul> </li> 
     <li id="li_D48B51C2208F423CB85D08886C2E1C66">PlayReady en Internet Explorer en Windows 8.1 y Edge </li> 
     <li id="li_2786AC19387241A296E015EE6FD07F2D">Adobe Access para Windows Firefox (solo vídeo) </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Funciones de reproducción avanzada de DASH {#dash-advanced-playback}

| Categoría | Tipo de contenido | Función | HTML5, FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| Reproducción | VOD | Reproducción en desplazamiento | ![](assets/supported15.png) |
| Reproducción | VOD | Reproducción solo de audio | ![](assets/supported15.png) |
| Reproducción | VOD | Juego de trucos | ![](assets/supported15.png) |
| Reproducción | VOD | Reproducción suave de trucos | ![](assets/supported15.png) |
| Reproducción | VOD + Activo | Análisis de ID3 | No admitido |
| Reproducción | VOD | Compatibilidad con varios períodos | Solo VOD |
| Reproducción | VOD + Activo | Flujos con autentificación | No admitido |
| Reproducción | VOD + Activo | Facturación | ![](assets/supported15.png) |
| Reproducción | VOD + Activo | Explorar | ![](assets/supported15.png) |

## Funciones de reproducción principales de DASH {#dash-core-playback}

| Categoría | Tipo de contenido | Función | HTML5 FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| Reproducción | VOD + Activo | Reproducción general (Reproducir, Pausa, Buscar) | ![](assets/supported15.png) |
| Reproducción | FER VOD | Reproducción general (Reproducir, Pausa, Buscar) | No admitido |
| Reproducción | VOD + Activo | Velocidad de bits adaptable | ![](assets/supported15.png) |
| Reproducción | VOD + Activo | Subtítulos 608/708 | ![](assets/supported15.png) |
| Reproducción | VOD + Activo | WebVTT | Solo VOD |
| Reproducción | VOD + Activo | Conmutación por error | Solo VOD |
| Reproducción | VOD + Activo | Notificaciones de QoS y reproductor | ![](assets/supported15.png) |
| Reproducción | VOD + Activo | Compatibilidad con encabezados de cookie | ![](assets/supported15.png) |
| Reproducción | VOD + Activo | Configuración de parámetros de control de búfer | ![](assets/supported15.png) |
| Reproducción | VOD + Activo | Establecer controles de velocidad de bits adaptables | ![](assets/supported15.png) |
| Reproducción | VOD + Activo | Etiquetas personalizadas (EventStream) | Solo VOD (en línea) |
| Reproducción | VOD + Activo | Enlace tardío de audio | Solo VOD |
| Reproducción | VOD + Activo | 302 redireccionamiento | Solo VOD |