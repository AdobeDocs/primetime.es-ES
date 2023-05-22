---
description: Estas clases describen el reproductor de contenidos y sus recursos.
title: Clases de reproductor multimedia
exl-id: de7f7488-2026-43b4-b74d-feff67bdc69a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# Clases de reproductor multimedia {#media-player-classes}

Puede utilizar la API Objective-C del reproductor Primetime para personalizar el comportamiento del reproductor.

Estas clases describen el reproductor de contenidos y sus recursos.

<table frame="all" colsep="1" rowsep="1" id="table_bm2_wl2_2m"> 
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>Clase</b> </td> 
   <td colname="2"><b>Descripción</b> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTABRControlParameters.html" format="html" scope="external"> PTABRControlParameters</a></span> </td> 
   <td colname="2">Encapsula todos los parámetros de control de velocidad de bits adaptable. Los parámetros admitidos son: 
    <ul id="ul_pnh_hm2_2m"> 
     <li id="li_46572FE1EB514AFF8C9F731E44DAF30B"><span class="codeph"> minBitRate</span> </li> 
     <li id="li_A10C75C9A5234241A5B84A4139F4D143"><span class="codeph"> maxBitRate</span> </li> 
     <li id="li_4E77E367A2E848D2B3E1A9C52209A7B2"><span class="codeph"> initialBitRate</span> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTDefaultMediaPlayerClientFactory.html" format="html" scope="external"> PTDefaultMediaPlayerClientFactory</a></span> </td> 
   <td colname="2"> Implementación predeterminada de <span class="codeph"> PTMediaPlayerClientFactory</span> en el TVSDK. Proporciona los valores disponibles <span class="codeph"> PTOportunityResolver</span>, <span class="codeph"> PTContentResolver</span>, y <span class="codeph"> PTAdPolicySelector</span> instancias. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html" format="html" scope="external"> PTMediaPlayer</a></span> </td> 
   <td colname="2">Define el componente raíz del marco de trabajo del reproductor de Primetime. <p>Las aplicaciones crean una instancia de esta clase para reproducir un medio. Este componente envía notificaciones para que la aplicación conozca el estado del reproductor en cualquier momento. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTMediaPlayerClientFactory.html" format="html" scope="external"> PTMediaPlayerClientFactory</a></span> </td> 
   <td colname="2"> Protocolo que describe los métodos que un generador de cliente de reproductor de medios personalizado debe implementar para proporcionar los <span class="codeph"> PTOportunityResolver</span> , <span class="codeph"> PTContentResolver</span> y <span class="codeph"> PTAdPolicySelector</span> instancias. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerItem.html" format="html" scope="external"> PTMediaPlayerItem</a></span> </td> 
   <td colname="2"> Representa un medio de audio y vídeo específico. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerView.html" format="html" scope="external"> PTMediaPlayerView</a></span> </td> 
   <td colname="2"> Administra el componente de vista del marco de trabajo del reproductor de Primetime. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaProfile.html" format="html" scope="external"> PTMediaProfile</a></span> </td> 
   <td colname="2"> Representa el perfil de un solo flujo en la lista de reproducción de variante. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaSelectionOption.html" format="html" scope="external"> PTMediaSelectionOption</a></span> </td> 
   <td colname="2">Representa un recurso de medios audiovisuales para adaptarse a diferentes preferencias de idioma, requisitos de accesibilidad o configuraciones de aplicación personalizadas. Tipos de opciones válidos: 
    <ul id="ul_p2q_gn2_2m"> 
     <li id="li_46BE5AE49732481FB6D336FFF896E5AD">Subtítulos (<span class="codeph"> PTMediaSelectionOptionTypeSubtitle</span>) </li> 
     <li id="li_6CEADCA12D4A48B7AE4A539985F32119">Audio alternativo (<span class="codeph"> PTMediaSelectionOptionTypeAudio</span>) </li> 
     <li id="li_248D3D997F8A4B6E9B48869F84060D1F"> <p>Indefinido (<span class="codeph"> PTMediaSelectionOptionTypeUndefined</span>) </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTOpportunityResolver.html" format="html" scope="external"> PTOportunityResolver</a> </span> clase, <span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTOpportunityResolver.html" format="html" scope="external"> PTOportunityResolver</a> protocolo</span> </td> 
   <td colname="2"> Clase utilizada para procesar señales en manifiesto que se utilizarán como ubicaciones para el proceso de Adobe Primetime y decisiones. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTOpportunityResolverDelegate.html" format="html" scope="external"> PTOportunityResolverDelegate</a></span> </td> 
   <td colname="2"> Protocolo que describe los métodos que utiliza el solucionador de oportunidades personalizado ( <span class="codeph"> PTOportunityResolver</span> ) debe utilizar para comunicar al delegado el estado de la resolución de la oportunidad. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTSDK.html" format="html" scope="external"> PTSDK</a></span> </td> 
   <td colname="2"> Describe la versión de TVSDK y sus funcionalidades. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTSDKConfig.html" format="html" scope="external"> PTSDKConfig</a></span> </td> 
   <td colname="2"> Expone la configuración global de TVSDK y permite que una aplicación se suscriba a etiquetas HLS personalizadas. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTTextStyleRule.html" format="html" scope="external"> PTextStyleRule</a></span> </td> 
   <td colname="2"> Define constantes que representan claves de atributo de estilo de texto que forman el diccionario de reglas. </td> 
  </tr> 
 </tbody> 
</table>
