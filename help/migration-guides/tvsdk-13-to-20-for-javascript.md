---
title: 'Conversión de TVSDK: 1.3 a 2.0 para JavaScript'
description: Muchas firmas de método y nombres de elementos de API han cambiado para 2.0. Revise estas tablas para ver todos los detalles del cambio de API.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: migration
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '5034'
ht-degree: 0%

---

# Conversión de TVSDK: 1.3 a 2.0 para JavaScript {#tvsdk-conversion-to-for-javascript}

Muchas firmas de método y nombres de elementos de API han cambiado para 2.0. Revise estas tablas para ver todos los detalles del cambio de API.

## Implementación de funciones de devolución de llamada en JavaScript {#implement-callback-functions-in-javascript}

Los comentarios de la documentación del método sugieren la firma de las llamadas de retorno que debe implementar.

Para JavaScript, la sintaxis de la API se basa en el ID web. Para una interfaz TVSDK, se llama a los nombres de método *methodName*(B). Para que la aplicación implemente métodos, un atributo de lectura y escritura denominado *methodName* CallbackFunc se agrega a la interfaz y la aplicación debe establecerla para que apunte a una función que implemente el método. Por ejemplo:

```shell
// An app implementable interface
interface ContentFactory
{
    /*
     * AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem item);
     */
    attribute Object retrieveAdPolicySelectorCallbackFunc;
 
    /*
     * ContentResolverList retrieveResolvers(MediaPlayerItem item);
     */
    attribute Object retrieveResolversCallbackFunc;
 
    /*
     * OpportunityGeneratorList retrieveGenerators(MediaPlayerItem item);
     */
    attribute Object retrieveGeneratorsCallbackFunc;
};

// this is how to implement it
var factory = new AdobePSDK.ContentFactory();
factory.retrieveAdPolicySelectorCallbackFunc = function(item)
{
    // return your adPolicySelector according to the item
    return adPolicySelector;
}
 
mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig ();
playerConfig.adFactory = factory;
// Use this config to load new MediaResource
```

## Cambios en el elemento de API del flujo de trabajo de publicidad para 2.0 {#advertising-workflow-api-element-changes-for}

Estas tablas comparan los elementos de la API del flujo de trabajo de publicidad para el TVSDK de JavaScript entre las versiones 1.3 y 2.0.

Tablas de este tema:

* TimedMetadata
* AdSignalingMode
* AdvertisingMetadata
* CustomRangeMetadata
* ReplaceTimeRange
* Ubicación
* Oportunidad
* Reserva
* Cronología / TimelineItem / TimelineMarker
* AdBreak
* Ad/AdAsset/AdClick/AdList/AdAssetList/AdBannerAsset
* AdBreakTimelineItem / AdTimelineItem
* AdBreakPolicy / AdBreakWatchedPolicy / AdPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector
* TimelineOperation
* AdBreakPlacement
* AuditudeSettings

### TimedMetadata {#timedmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p> <strong>TimedMetadata</strong>: interfaz TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0 ; <br /> const unsigned short METADATA_TYPE_ID3 = 1 ; <br /> atributo readonly tipo corto sin signo; <br /> atributo de solo lectura long time;<br /> id de DomString de atributo de solo lectura;<br /> nombre DomString del atributo de solo lectura;<br /> contenido DomString de atributo de solo lectura; <br /> readonly attribute Metadatos de objeto;<br /> }; </p> </td> 
   <td><p>interfaz TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0 ;<br /> const unsigned short METADATA_TYPE_ID3 = 1 ;<br /> readonly attribute unsigned short metadataType;<br /> atributo de solo lectura long time;<br /> id largo de atributo de solo lectura;<br /> nombre DomString del atributo de solo lectura;<br /> <br /> readonly attribute Metadatos de objeto;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetadataList</strong>: (sin cambios para 2.0)</td> 
   <td><p>interfaz TimedMetadataList {<br /> atributo readonly de larga longitud sin signo;<br /> getter TimedMetadata(índice largo sin signo);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AdSignalingMode {#adsignalingmode}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Interfaz AdSignalingMode { <br /> const unsigned short MODE_DEFAULT, <br /> const unsigned short MODE_MANIFEST_CUES , <br /> const unsigned short MODE_SERVER_MAP , <br /> const unsigned short MODE_CUSTOM_RANGES <br /> };</p> </td> 
   <td>Esto reemplaza la clave MetadataKeys::MANIFEST_CUES.</td> 
  </tr> 
 </tbody> 
</table>

### AdvertisingMetadata {#advertisingmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Metadatos de publicidad de interfaz { <br /> atributo modo AdSignalingMode; <br /> atributo AdBreakWatchedPolicy adBreakAsWatched; <br /> attribute boolean livePereroll; <br /> atributo booleano delayAdLoading ; <br /> };</p> </td> 
   <td>Esta funcionalidad fue proporcionada por<p>MetadataKeys::ADVERTISING_METADATA</p> clave.</td> 
  </tr> 
 </tbody> 
</table>

### CustomRangeMetadata {#customrangemetadata}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Interfaz de CustomRangeMetadata { <br /> const unsigned short TYPE_MARK_RANGE; <br /> const unsigned short TYPE_DELETE_RANGE; <br /> const unsigned short TYPE_REPLACE_RANGE; <br /> atributo tipo corto sin signo; <br /> atributo booleano adjustSeekPosition; <br /> atributo TimeRangeList timeRangeList; <br /> };</p> </td> 
   <td>(Nuevo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### ReplaceTimeRange {#replacetimerange}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface ReplaceTimeRange { <br /> atributo de inicio largo sin signo; <br /> atributo readonly de extremo largo sin signo; <br /> atributo de larga duración sin signo; <br /> attribute unsigned long replaceDuration; <br /> };</p> </td> 
   <td>(Nuevo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### Ubicación {#placement}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Ubicación de interfaz { <br /> const unsigned short TYPE_MID_ROLL; <br /> const unsigned short TYPE_PRE_ROLL; <br /> const unsigned short TYPE_POST_ROLL; <br /> const unsigned short TYPE_SERVER_MAP; <br /> const unsigned short TYPE_CUSTOM_RANGE;<br /> atributo readonly tipo corto sin signo; <br /> atributo de solo lectura long time; <br /> atributo de solo lectura de larga duración; <br /> const unsigned short MODE_DEFAULT; <br /> const unsigned short MODE_INSERT; <br /> const unsigned short MODE_REPLACE; <br /> const unsigned short MODE_DELETE; <br /> const unsigned short MODE_MARK; <br /> const unsigned short MODE_FREE_REPLACE; <br /> atributo readonly modo corto sin signo; <br /> Rango TimeRange de atributo de solo lectura; <br /> };</p> </td> 
   <td>(Nuevo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### Oportunidad {#opportunity}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>oportunidad de interfaz { <br /> id de DomString de atributo de solo lectura; <br /> ubicación de ubicación de atributo de solo lectura; <br /> atributo de solo lectura Configuración de objetos; <br /> readonly attribute Objeto customParameters; <br /> }; </p> </td> 
   <td>(Nuevo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### Reserva {#reservation}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Interfaz Reserva { <br /> Rango TimeRange de atributo de solo lectura; <br /> atributo de solo lectura de larga espera; <br /> }; </p> </td> 
   <td> (Nuevo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### Cronología / TimelineItem / TimelineMarker {#timeline-timelineitem-timelinemarker}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p><strong>Cronología</strong>: línea de tiempo de interfaz <br /> { readonly atributo TimelineMarkerList timelineMarkers; <br /> atributo readonly TimelineItemList timelineItems; <br /> double convertToLocalTime( hora doble); <br /> double convertToVirtualTime( hora doble); <br /> };</p> </td> 
   <td><p>línea de tiempo de interfaz {<br /> atributo readonly TimelineMarkerList timelineMarkers;<br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>TimelineItem</strong>: interfaz TimelineItem :<br /> Marcador de cronología {<br /> id largo de atributo de solo lectura; <br /> atributo de solo lectura TimeRange virtualRange; <br /> atributo de solo lectura TimeRange localRange; <br /> atributo de solo lectura booleano visto; <br /> atributo de solo lectura booleano temporary; <br /> }; </p> </td> 
   <td>(Nuevo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><strong>TimelineMarker</strong>: (sin cambios para 2.0)</td> 
   <td><p>interfaz TimelineMarker {<br /> atributo de solo lectura doble vez;<br /> duración doble del atributo readonly;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AdBreak {#adbreak}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Interfaz AdBreak {<br /> <br /> <br /> <br /> duración doble del atributo readonly;<br /> anuncios de AdList de atributo de solo lectura;<br /> <br /> <br /> atributo de solo lectura AdInsertionType insertionType;<br /> }; </p> </td> 
   <td><p>Interfaz AdBreak {<br /> atributo de solo lectura doble vez;<br /> atributo de solo lectura double replaceDuration;<br /> <br /> duración doble del atributo readonly;<br /> atributo de solo lectura AdList adList;<br /> <br /> datos DomString de atributo de solo lectura;<br /> <br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### Ad/AdAsset/AdClick/AdList/AdAssetList/AdBannerAsset {#ad-adasset-adclick-adlist-adassetlist-adbannerasset}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p> <strong>Anuncio</strong>: Anuncio de interfaz {<br /> atributo de solo lectura AdAsset primaryAsset;<br /> atributo de solo lectura AdAssetList companionAssets;<br /> <br /> duración doble del atributo readonly;<br /> id de DomString de atributo de solo lectura;<br /> const unsigned short ADTYPE_LINEAR = 0 ;<br /> const unsigned short ADTYPE_NONLINEAR = 1 ;<br /> <br /> readonly attribute unsigned short adType;<br /> atributo de solo lectura AdInsertionType adInsertionType; <br /> <br /> readonly attribute boolean clickable; <br /> el atributo booleano de solo lectura isCustomAdMarker;<br /> }; </p> </td> 
   <td><p>Anuncio de interfaz {<br /> atributo de solo lectura AdAsset primaryAsset;<br /> atributo de solo lectura AdAssetList companionAssets;<br /> <br /> duración doble del atributo readonly;<br /> id de DomString de atributo de solo lectura;<br /> const unsigned short ADTYPE_LINEAR = 0 ;<br /> const unsigned short ADTYPE_NONLINEAR = 1 ;<br /> <br /> atributo readonly tipo corto sin signo;<br /> atributo de solo lectura AdInsertionType insertionType; <br /> atributo readonly Rastreador de objetos;<br /> <br /> <br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>: (sin cambios para 2.0)</td> 
   <td><p>Interfaz de AdAsset {<br /> id de DomString de atributo de solo lectura;<br /> duración doble del atributo readonly;<br /> atributo de solo lectura MediaResource;<br /> atributo de solo lectura AdClick adClick;<br /> readonly attribute Metadatos de objeto;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>: (sin cambios para 2.0)</td> 
   <td><p>Interfaz AdClick {<br /> id de DomString de atributo de solo lectura;<br /> readonly attribute DomString title;<br /> url de DomString de atributo de solo lectura;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdList</strong>: (sin cambios para 2.0)</td> 
   <td><p>interfaz AdList {<br /> atributo readonly de larga longitud sin signo;<br /> getter Ad(índice largo sin signo);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>: (sin cambios para 2.0)</td> 
   <td><p>interfaz AdAssetList {<br /> atributo readonly de larga longitud sin signo;<br /> getter AdAsset(índice largo sin signo);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>: interfaz AdBannerAsset : AdAsset<br /> {<br /> atributo de solo lectura int width;<br /> atributo de solo lectura int height;<br /> atributo de solo lectura DomString staticUrl;<br /> el atributo de solo lectura DomString height;<br /> anchura del atributo DomString de solo lectura;<br /> };</p> </td> 
   <td> Novedades en 2.0</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakTimelineItem / AdTimelineItem {#adbreaktimelineitem-adtimelineitem}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p> <strong>AdBreakTimelineItem</strong>: interfaz AdBreakTimelineItem : TimelineItem { <br /> atributo de solo lectura AdBreak adBreak; <br /> atributo de solo lectura Elementos AdTimelineItemList; <br /> }; </p> </td> 
   <td> (Nuevo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimelineItem</strong>: interfaz AdTimelineItem : TimelineItem { <br /> atributo de solo lectura AdBreak adBreak; <br /> anuncio de anuncio de atributo de solo lectura; <br /> }; </p> </td> 
   <td> (Nuevo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>: interfaz AdBreakTimelineItemList { <br /> atributo readonly de larga longitud sin signo; <br /> getter AdBreakTimelineItem (índice log ng sin signo); <br /> };</p> </td> 
   <td> (Nuevo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakPolicy / AdBreakWatchedPolicy / AdPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector {#adbreakpolicy-adbreakwatchedpolicy-adpolicy-adpolicymode-adpolicyinfo-adpolicyselector}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaz AdBreakPolicy {<br /> atributo readonly short AD_BREAK_POLICY_SKIP;<br /> atributo readonly short AD_BREAK_POLICY_PLAY;<br /> atributo readonly short AD_BREAK_POLICY_REMOVE;<br /> atributo readonly short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;<br /> };</p> </td> 
   <td><p> interfaz AdPolicyConstants {<br /> atributo readonly short AD_BREAK_POLICY_SKIP;<br /> atributo readonly short AD_BREAK_POLICY_PLAY;<br /> atributo readonly short AD_BREAK_POLICY_REMOVE;<br /> atributo readonly short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;}<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p> interfaz AdBreakWatchedPolicy {<br /> atributo readonly short AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> atributo readonly short AD_BREAK_AS_WATCHED_ON_END;<br /> atributo readonly short AD_BREAK_AS_WATCHED_NEVER;<br /> }; </p> </td> 
   <td><p> ...<br /> atributo readonly short AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> atributo readonly short AD_BREAK_AS_WATCHED_ON_END;<br /> atributo readonly short AD_BREAK_AS_WATCHED_NEVER;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaz AdPolicy {<br /> atributo readonly short AD_POLICY_PLAY;<br /> atributo readonly short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> atributo readonly short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN; atributo readonly short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> <br /> atributo readonly short AD_POLICY_SKIP_AD_BREAK;<br /> };</p> </td> 
   <td><p> ... <br /> atributo readonly short AD_POLICY_PLAY;<br /> atributo readonly short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> atributo readonly short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;<br /> atributo readonly short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> atributo readonly short AD_POLICY_SKIP_AD_BREAK;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaz AdPolicyMode {<br /> atributo readonly short AD_POLICY_MODE_PLAY;<br /> atributo readonly short AD_POLICY_MODE_SEEK;<br /> atributo readonly short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
   <td><p> ...<br /> {readonly attribute short AD_POLICY_MODE_PLAY;<br /> atributo readonly short AD_POLICY_MODE_SEEK;<br /> atributo readonly short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaz AdPolicyInfo {<br /> atributo de solo lectura AdBreakTimelineItemList <br /> adBreakTimelineItems;<br /> atributo de solo lectura AdTimelineItem adTimelineItem;<br /> atributo readonly double currentTime;<br /> atributo de solo lectura double seekToTime;<br /> tasa doble de atributo de solo lectura;<br /> modo corto de atributo de solo lectura; //AdPolicyMode<br /> };</p> </td> 
   <td><p>interfaz AdPolicyInfo {<br /> atributo de solo lectura AdBreakPlacementList <br /> adBreakPlacements;<br /> anuncio de anuncio de atributo de solo lectura;<br /> atributo readonly double currentTime;<br /> atributo de solo lectura double seekToTime;<br /> tasa doble de atributo de solo lectura;<br /> modo corto de atributo de solo lectura; //AdPolicyMode<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaz AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo (adPolicyInfo);<br /> */<br /> attribute Objeto selectPolicyForAdBreakCallbackFunc;<br /> /**<br /> * AdBreakTimelineItemList selectAdBreaksToPlay(<br /> * AdPolicyInfo (adPolicyInfo);<br /> */<br /> attribute Objeto selectAdBreaksToPlayCallbackFunc;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute Objeto selectPolicyForSeekIntoAdCallbackFunc; <br /> /**<br /> * AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo (adPolicyInfo);<br /> */<br /> attribute Objeto selectWatchedPolicyForAdBreakCallbackFunc;<br /> };</p> </td> 
   <td><p>interfaz AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo (adPolicyInfo);<br /> */<br /> attribute Objeto selectPolicyForAdBreakFuncCallback;<br /> /**<br /> * AdBreakPlacementList selectAdBreaksToPlay(<br /> * AdPolicyInfo (adPolicyInfo);<br /> */<br /> attribute Objeto selectAdBreaksToPlayCallback;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute Objeto selectPolicyForSeekIntoAdCallback; <br /> /**<br /> * AdBreakAsWatched selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo (adPolicyInfo);<br /> */<br /> attribute Objeto selectWatchedPolicyForAdBreakCallback;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TimelineOperation {#timelineoperation}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaz TimelineOperation { <br /> ubicación de ubicación de atributo de solo lectura ; <br /> };</p> </td> 
   <td> (Nuevo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakPlacement {#adbreakplacement}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaz AdBreakPlacement : TimelineOperation {<br /> atributo de solo lectura AdBreak adBreak;<br /> atributo de solo lectura Colocación; // From TimelineOperation<br /> atributo de solo lectura doble vez;<br /> duración doble del atributo readonly;<br /> };</p> </td> 
   <td><p>interfaz AdBreakPlacement {<br /> atributo de solo lectura AdBreak adBreak;<br /> ubicación de ubicación de atributo de solo lectura;<br /> atributo de solo lectura doble vez;<br /> duración doble del atributo readonly;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AuditudeSettings {#auditudesettings}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaz AuditudeSettings : AdvertisingMetadata { <br /> atributo DomString zoneId; <br /> atributo DomString mediaId; <br /> atributo DomString defaultMediaId ; <br /> atributo dominio DomString ; <br /> attribute Objeto targetingInfo ; <br /> attribute Objeto customParameters ; <br /> attribute Boolean creativePackageEnabled ;<br /> atributo Boolean showStaticBanners ;<br /> };</p> </td> 
   <td>La clave MetadataKeys::AUDITUDE_METADATA_KEY proporcionó funcionalidad.</td> 
  </tr> 
 </tbody> 
</table>

## Cambios en los elementos de la API de personalización para 2.0 {#customization-api-element-changes-for}

En estas tablas se comparan los elementos de la API de personalización del TVSDK de JavaScript entre las versiones 1.3 y 2.0.

Tablas de este tema:

* MediaPlayerItemConfig
* ContentFactory
* NetworkConfiguration

### MediaPlayerItemConfig {#mediaplayeritemconfig}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaz MediaPlayerItemConfig {<br /> atributo ContentFactory adFactory;<br /> attribute StringList subscribeTags;<br /> <br /> atributo StringList adTags;<br /> <br /> <br /> atributo AdSignalingMode adSignalingMode;<br /> attribute CustomRangeMetadata customRangeMetadata;<br /> atributo NetworkConfiguration networkConfiguration;<br /> attribute AdvertisingMetadata advertisingMetadata;<br /> atributo Boolean useHardwareDecoder;<br /> };</p> </td> 
   <td><p>interfaz MediaPlayerConfig {<br /> <br /> <br /> <br /> atributo StringList adTags;<br /> atributo StringList subscribedTags;<br /> atributo MediaPlayerClientFactory clientFactory;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### ContentFactory {#contentfactory}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaz ContentFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector()<br /> * Elemento MediaPlayerItem);<br /> */<br /> attribute Objeto retrieveAdPolicySelectorCallbackFunc;<br /> };</p> </td> 
   <td><p>interfaz MediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector()<br /> * Elemento MediaPlayerItem);<br /> */<br /> attribute Objeto retrieveAdPolicySelectorFunc;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### NetworkConfiguration {#networkconfiguration}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaz NetworkConfiguration<br /> {<br /> atributo boolean forceNativeNetworking;<br /> atributo booleano useRedirectUrl;<br /> attribute Objeto cookieHeader;<br /> atributo booleano readSetCookieHeader;<br /> attribute int masterUpdateInterval; <br /> atributo booleano useCookieHeaderForAllRequests;<br /> attribute int readLimit;<br /> };</p> </td> 
   <td>En la versión 1.3, MetadataKeys proporcionaba algunas de estas funcionalidades</td> 
  </tr> 
 </tbody> 
</table>

## Cambios en los elementos de la API de DRM para 2.0 {#drm-api-element-changes-for}

Estas tablas comparan los elementos de la API de DRM para el TVSDK de JavaScript entre las versiones 1.3 y 2.0.

Tablas de este tema:

* Inicialización del flujo de trabajo DRM
* DRMAcquireLicenseSettings / DRMAuthenticationMethod
* Metadatos DRM
* DRMPlaybackTimeWindow
* DRMLicense
* DRMLicenseDomain
* DRMPolicy
* Administrador de DRS

### Inicialización del flujo de trabajo DRM {#drm-workflow-initialization}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>La aplicación debe llamar a AdobePSDK.startDRMWorkflow para iniciar el flujo de trabajo de DRM. Sin esta llamada, los vídeos DRM no se reproducirán.<p>interfaz AdobePSDK<br /> {<br /> void startDRMWorkFlow(<br /> DomString appStoratePath, <br /> DomString publisherId, <br /> DomString appId, <br /> DomString appVersion, <br /> boolean privacyModeOn);<br /> };</p> </td> 
   <td>La inicialización se realizó internamente y no se requirió una llamada explícita.</td> 
  </tr> 
 </tbody> 
</table>

### DRMAcquireLicenseSettings/DRMAuthenticationMethod {#drmacquirelicensesettings-drmauthenticationmethod}

| API 2.0 | API 1.3 |
|--- |--- |
| **DRMAcquireLicenseSettings** |  |
| Sin cambios para 2.0. | enum DRMAcquireLicenseSettings <br>{<br> const unsigned int FORCE_REFRESH = 0;<br> const unsigned int LOCAL_ONLY = 1;<br> const unsigned int ALLOW_SERVER = 2;<br> }; |
| **DRMAuthenticationMethod** |  |
| Sin cambios para 2.0. | enum DRMAuthenticationMethod <br>{<br> const unsigned int DESCONOCIDO = 0;<br> const unsigned int ANONYMOUS = 1;<br> const unsigned int USERNAME_AND_PASSWORD = 2;<br> } |

### Metadatos DRM {#drmmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0.</td> 
   <td><p>Interfaz de metadatos DRM<br /> {<br /> atributo de solo lectura DomString serverUrl;<br /> atributo de solo lectura DomString licenseId;<br /> atributo de solo lectura DRMPolicyArray policies; <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPlaybackTimeWindow {#drmplaybacktimewindow}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaz DRMPlaybackTimeWindow {<br /> atributo readonly en playbackPeriodInSeconds;<br /> atributo readonly long playbackStartDate;<br /> atributo readonly long playbackEndDate;<br /> };</p> </td> 
   <td><p>interfaz DRMPlaybackTimeWindow {<br /> atributo de solo lectura int periodInSeconds;<br /> atributo readonly int startDate;<br /> atributo de solo lectura int endDate;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMLicense {#drmlicense}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0.</td> 
   <td><p>interfaz DRMLicense {<br /> atributo readonly Uint8Array bytes;<br /> atributo readonly Date licenseStartDate;<br /> atributo readonly Date licenseEndDate;<br /> atributo de solo lectura Date offlineStorageStartDate;<br /> atributo de solo lectura Date offlineStorageEndDate; <br /> atributo de solo lectura DomString serverUrl;<br /> atributo de solo lectura DomString licenseID;<br /> atributo de solo lectura DomString policyID;<br /> atributo readonly DRMPlaybackTimeWindow playbackTimeWindow;<br /> readonly attribute Objeto customProperties;<br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMLicenseDomain {#drmlicensedomain}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaz DRMLicenseDomain {<br /> atributo de solo lectura DomString authenticationDomain;<br /> atributo de solo lectura DRMAuthenticationMethod authenticationMethod; <br /> atributo de solo lectura DomString serverUrl;<br /> };</p> </td> 
   <td><p>interfaz DRMLicenseDomain {<br /> atributo de solo lectura DomString authDomain;<br /> atributo readonly DRMAuthenticationMethod authMethod; <br /> atributo de solo lectura DomString serverURL;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPolicy {#drmpolicy}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaz DRMPolicy<br /> {<br /> atributo de solo lectura DomString authenticationDomain;<br /> atributo de solo lectura DRMAuthenticationMethod authenticationMethod;<br /> <br /> atributo de solo lectura DomString displayName;<br /> atributo readonly DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
   <td><p>interfaz DRMPolicy<br /> {<br /> atributo de solo lectura DomString authDomain;<br /> atributo readonly DRMAuthenticationMethod authMethod;<br /> atributo de solo lectura DomString dispName;<br /> atributo readonly DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Administrador de DRS {#drmmanager}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaz DRManager : EventTarget {<br /> void acquisitionLicense(metadatos de metadatos DRM, <br /> Configuración de DRMAcquireLicenseSettings, <br /> DRMAquireLicenseListener (agente de escucha);<br /> void acquisitionPreviewLicense(DRMetadata metadata, <br /> DRMAquireLicenseListener (agente de escucha);<br /> void authenticate(metadatos de metadatos DRM, <br /> URL de DomString,<br /> DomString &amp;authenticationDomain, <br /> usuario DomString, <br /> Contraseña de DomString, <br /> DRMAuthenticateListener (listener);<br /> <br /> Metadatos de DRM createMetadataFromBytes(<br /> matriz Uint8Array, detector DRMErrorListener);<br /> void initialize(DRMOperationCompleteListener listener);<br /> attribute long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> forceRefresh booleano, <br /> DRMOperationCompleteListener (listener);<br /> void leftLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> DRMOperationCompleteListener (listener);<br /> <br /> void resetDRM(DRMOperationCompleteListener listener);<br /> void returnLicense(DomString serverURL, <br /> ID de licencia de DomString, <br /> policyID de DomString, <br /> commitInmediatamente booleano,<br /> DRMReturnLicenseListener (detector);<br /> void setAuthenticationToken(<br /> Metadatos de metadatos de DRM, <br /> AuthenticationDomain de DomString, <br /> Token Uint8Array, <br /> DRMOperationCompleteListener (listener);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> DRMOperationCompleteListener (listener);<br /> };</p> </td> 
   <td><p>interfaz DRManager : EventTarget {<br /> void acquisitionLicense(metadatos de metadatos DRM, <br /> Configuración de DRMAcquireLicenseSettings, <br /> EventContext (eventContext);<br /> void acquisitionPreviewLicense(DRMetadata metadata, <br /> EventContext (eventContext);<br /> void authenticate(metadatos de metadatos DRM, <br /> URL de DomString,<br /> DomString &amp;authenticationDomain, <br /> usuario DomString, <br /> Contraseña de DomString, <br /> EventContext (eventContext);<br /> <br /> Metadatos de DRM createMetadataFromBytes(<br /> matriz Uint8Array, EventContext (eventContext);<br /> void initialize(EventContext eventContext);<br /> attribute long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> forceRefresh booleano, <br /> EventContext (eventContext);<br /> void leftLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> EventContext (eventContext);<br /> <br /> void resetDRM(EventContext eventContext);<br /> void returnLicense(DomString serverURL, <br /> ID de licencia de DomString,<br /> policyID de DomString, <br /> commitInmediatamente booleano,<br /> EventContext (eventContext);<br /> void setAuthenticationToken(<br /> Metadatos de metadatos de DRM, <br /> AuthenticationDomain de DomString, <br /> Token Uint8Array, <br /> EventContext (eventContext);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> EventContext (eventContext);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>clase DRMErrorListener : <br /> public psdkutils::PSDKInterfaceWithUserData {<br /> público:<br /> void virtual onDRMError(uint32_t principal, <br /> uint32_t minor, <br /> const psdkutils:: PSDKString&amp; errorString, <br /> const psdkutils::PSDKString&amp; errorServerUrl) = 0;<br /> <br /> protegido:<br /> virtual ~DRMErrorListener() {}<br /> }</p> </td> 
   <td>Evento / Interfaz / Descripción 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>Cuando se produce un error durante uno de los métodos asincrónicos de DRManger.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>clase DRMOperationCompleteListener : <br /> public DRMErrorListener {<br /> público:<br /> void virtual onDRMOperationComplete() = 0;<br /> <br /> protegido:<br /> virtual ~DRMOperationCompleteListener() {}<br /> };</p> </td> 
   <td>Evento / Interfaz / Descripción 
    <ul> 
     <li>kEventDRMInitializationComplete<p>/ PSDKEvent</p> <p>Cuando la inicialización de DRM haya finalizado.</p> </li> 
     <li>kEventDRMJoinLicenseDomainComplete<p>/ PSDKEvent</p> <p>Cuando la acción joinLicenseDomain() se complete correctamente.</p> </li> 
     <li>kEventDRMLeaveLicenseDomainComplete<p>/ PSDKEvent</p> <p>Cuando la acción leaveLicenseDomain() se complete correctamente.</p> </li> 
     <li>kEventDRMResetCompletePSDKEvent<p>/ PSDKEvent</p> <p>Cuando la acción resetDRM() se complete correctamente.</p> </li> 
     <li>kEventDRMAuthenticationTokenSet<p>/ PSDKEvent</p> <p>Cuando la acción setAuthenticationTokenSet() se complete correctamente.</p> </li> 
     <li>kEventDRMLicenseStored<p>/ PSDKEvent</p> <p>Cuando la acción storeLicenseBytes() se complete correctamente.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>clase DRMAuthenticateListener : <br /> public DRMErrorListener {<br /> público:<br /> virtual void onAuthenticationComplete(<br /> psdkutils::PSDKImmutableByteArray* <br /> authenticationToken) = 0;<br /> <br /> protegido:<br /> virtual ~DRMAuthenticateListener() {}<br /> }</p> </td> 
   <td>Evento / Interfaz / Descripción 
    <ul> 
     <li>kEventDRMAuthenticationComplete<p>/ DRMAuthenticationCompleteEvent</p> <p>Cuando la llamada al método DRManager::authenticate se realiza correctamente.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>clase DRMAquireLicenseListener: <br /> public DRMErrorListener {<br /> público:<br /> void virtual onLicenseAcquired(const DRMLicense*) = 0;<br /> <br /> protegido:<br /> virtual ~DRMAquireLicenseListener() {}<br /> };</p> </td> 
   <td>Evento / Interfaz / Descripción 
    <ul> 
     <li>kEventDRMPreviewLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>Cuando la llamada al método DRManager::acquisitionPreviewLicense se realiza correctamente.</p> </li> 
     <li>kEventDRMLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>Cuando la llamada al método DRManager::acquierLicense se realiza correctamente.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>clase DRMReturnLicenseListener: <br /> public DRMErrorListener {<br /> público:<br /> void virtual onLicenseReturnComplete(uint32_t numReturned ) = 0;<br /> <br /> protegido:<br /> virtual ~DRMReturnLicenseListener() {}<br /> };</p> </td> 
   <td>Evento / Interfaz / Descripción 
    <ul> 
     <li>kEventDRMLicenseReturnComplete<p>/ DRMLicenseReturnCompleteEvent</p> <p>Cuando la llamada al método DRManager::returnLicense se realiza correctamente.</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Cambios en los elementos de la API de reproducción genérica para 2.0 {#generic-playback-api-element-changes-for}

Estas tablas comparan los elementos genéricos de la API de reproducción entre JavaScript TVSDK 1.3 y 2.0.

Tablas de este tema:

* MediaResource
* MediaPlayer
* ABRControlParameters
* BufferControlParameters
* TextFormat
* MediaPlayerItemLoader

### MediaResource {#mediaresource}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaz MediaResource {<br /> atributo DomString url; <br /> atributo tipo corto sin signo;<br /> attribute Metadatos de objeto;<br /> const unsigned short TYPE_HLS;<br /> const short sin firmar TYPE_HDS;<br /> const unsigned short TYPE_DASH;<br /> const unsigned short TYPE_CUSTOM;<br /> const unsigned short TYPE_UNKNOWN;<br /> };</p> </td> 
   <td><p>interfaz MediaResource {<br /> atributo DomString url;<br /> atributo DomString type;<br /> attribute Metadatos de objeto;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### MediaPlayer {#mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaz MediaPlayer : EventTarget<br /> {<br /> void prepareToPlay( posición doble);<br /> void play();<br /> void pause();<br /> void seek( doble posición);<br /> void seekToLocal( doble posición);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem(elemento MediaPlayerItem);<br /> void replaceCurrentResource(MediaResource, <br /> MediaPlayerItemConfig (configuración); <br /> void suspender();<br /> void restore();<br /> void notifyClick();<br /> <br /> atributo de solo lectura TimeRange playbackRange;<br /> atributo de solo lectura TimeRange seekableRange;<br /> atributo readonly double currentTime;<br /> atributo readonly double localTime;<br /> atributo de solo lectura TimeRange bufferedRange;<br /> atributo de solo lectura DRManager drmManager;<br /> atributo de solo lectura MediaPlayerItem currentItem;<br /> <br /> // PlayerStatus<br /> <br /> <br /> const unsigned short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEEKING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /> <br /> atributo readonly de estado corto sin signo;<br /> <br /> atribuir volumen corto sin firmar;<br /> atributo ABRControlParameters abrControlParameters;<br /> atributo BufferControlParameters bufferControlParameters;<br /> <br /> const unsigned short VISIBLE; //Para visibilidad CC<br /> const unsigned short INVISIBLE; //Para visibilidad CC<br /> atributo short ccVisibility sin firmar;<br /> atributo TextFormat ccStyle;<br /> atributo de solo lectura PlaybackMetrics playbackMetrics;<br /> <br /> tasa doble de atributo;<br /> atributo MediaPlayerView view;<br /> readonly attribute Cronología cronología;<br /> atributo double currentTimeUpdateInterval; <br /> // No se admitirá la configuración para 2.0<br /> };</p> </td> 
   <td><p>interfaz MediaPlayer : EventTarget<br /> {<br /> void prepareToPlay( int position);<br /> void play();<br /> void pause();<br /> void seek( int position);<br /> void seekToLocalTime( int position);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem(MediaResource source);<br /> <br /> <br /> <br /> <br /> <br /> <br /> atributo de solo lectura TimeRange playbackRange;<br /> atributo de solo lectura TimeRange seekableRange;<br /> atributo readonly double currentTime;<br /> atributo readonly double localTime;<br /> atributo de solo lectura TimeRange bufferedRange;<br /> atributo de solo lectura DRManager drmManager;<br /> atributo de solo lectura MediaPlayerItem currentItem;<br /> <br /> // PlayerState<br /> const unsigned short PLAYER_STATE_IDLE;<br /> const unsigned short PLAYER_STATE_INITIALIZING;<br /> const unsigned short PLAYER_STATE_INITIALIZED;<br /> const unsigned short PLAYER_STATE_PREPARING;<br /> const unsigned short PLAYER_STATE_PREPARED;<br /> const unsigned short PLAYER_STATE_PLAYING;<br /> const unsigned short PLAYER_STATE_PAUSED;<br /> const unsigned short PLAYER_STATE_SEEKING;<br /> const unsigned short PLAYER_STATE_COMPLETE;<br /> const unsigned short PLAYER_STATE_ERROR;<br /> const unsigned short PLAYER_STATE_RELEASED;<br /> const unsigned short PLAYER_STATUS_SUSPENDED;<br /> atributo readonly estado corto sin firmar;<br /> <br /> atribuir volumen corto sin firmar;<br /> atributo ABRControlParameters abrControlParameters;<br /> atributo BufferControlParameters bufferControlParameters;<br /> <br /> readonly unsigned short VISIBLE; //Para visibilidad CC<br /> readonly unsigned short INVISIBLE; //Para visibilidad CC<br /> atributo short ccVisibility sin firmar;<br /> atributo TextFormat ccStyle;<br /> atributo de solo lectura PlaybackMetrics playbackMetrics;<br /> atributo MediaPlayerConfig mediaPlayerConfig;<br /> tasa doble de atributo;<br /> atributo MediaPlayerView view;<br /> readonly attribute Cronología cronología;<br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaz MediaPlayerStatus<br /> {<br /> // PlayerStatus<br /> const unsigned short PLAYER_STATUS_IDLE;<br /> const unsigned short PLAYER_STATUS_INITIALIZING;<br /> const unsigned short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEEKING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /> const unsigned short PLAYER_STATUS_SUSPENDED;<br /> };</p> </td> 
   <td>(Nuevo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

#### Eventos admitidos por MediaPlayer {#events-supported-by-mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>Nombre del evento 2.0</th> 
   <th>Interfaz de 2.0</th> 
   <th> </th> 
   <th>1.3 Nombre del evento</th> 
   <th>Interfaz de 1.3</th> 
  </tr> 
  <tr> 
   <td><p>(eliminado para 2.0)</p> </td> 
   <td> </td> 
   <td> </td> 
   <td>preparado</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td><p>itemUpdated</p> <p>Cuando se actualiza un elemento del reproductor de contenidos.</p> </td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>actualizado</p> <p>Cuando el reproductor de contenidos haya actualizado correctamente los contenidos.</p> </td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>timedMetadataAvailable</td> 
   <td>TimedMetadataEvent</td> 
   <td> </td> 
   <td>TimedMetadata</td> 
   <td>TimedMetadataEvent</td> 
  </tr> 
  <tr> 
   <td>timelineUpdated</td> 
   <td>Evento</td> 
   <td> </td> 
   <td>TimelineUpdated</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>Eliminado en 2.0</td> 
   <td> </td> 
   <td> </td> 
   <td>playStart</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>Eliminado para 2.0</td> 
   <td> </td> 
   <td> </td> 
   <td>playComplete</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>statusChanged</td> 
   <td>StatusEvent</td> 
   <td> </td> 
   <td>stateChanged</td> 
   <td>StateEvent</td> 
  </tr> 
  <tr> 
   <td>sizeAvailable</td> 
   <td>SizeEvent</td> 
   <td> </td> 
   <td>talla</td> 
   <td>SizeEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakStarted</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakStart</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>adStarted</td> 
   <td>AdEvent</td> 
   <td> </td> 
   <td>adStart</td> 
   <td>AdEvent</td> 
  </tr> 
  <tr> 
   <td>adProgress</td> 
   <td>AdProgressEvent</td> 
   <td> </td> 
   <td>adProgress</td> 
   <td>AdProgressEvent</td> 
  </tr> 
  <tr> 
   <td>adCompleted</td> 
   <td>AdEvent</td> 
   <td> </td> 
   <td>adComplete</td> 
   <td>AdEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakCompleted</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakComplete</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>timeChanged</td> 
   <td>TimeEvent</td> 
   <td> </td> 
   <td>progreso</td> 
   <td>ProgressEvent</td> 
  </tr> 
  <tr> 
   <td>bufferingBegin</td> 
   <td>Evento</td> 
   <td> </td> 
   <td>amortiguador</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>bufferingEnd</td> 
   <td>Evento</td> 
   <td> </td> 
   <td>bufferComplete</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>seekBegin</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td>seekStart</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>seekEnd</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td>seekComplete</td> 
   <td>TimeEvent</td> 
  </tr> 
  <tr> 
   <td>loadInformationAvailable</td> 
   <td>LoadInformationEvent</td> 
   <td> </td> 
   <td>loadInfo</td> 
   <td>LoadInfoEvent</td> 
  </tr> 
  <tr> 
   <td>operationFailed</td> 
   <td>NotificationEvent</td> 
   <td> </td> 
   <td>operationFailed</td> 
   <td>ErrorEvent</td> 
  </tr> 
  <tr> 
   <td>drmMetadataInfoAvailable</td> 
   <td>DTMetadataEvent</td> 
   <td> </td> 
   <td>drmMetadata</td> 
   <td>DTMetadataEvent</td> 
  </tr> 
  <tr> 
   <td>reservationReached</td> 
   <td>ReservationEvent</td> 
   <td> </td> 
   <td>timelineHolderReached</td> 
   <td>TimelineHolderEvent</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>bitrateChanged</td> 
   <td>BitrateChangedEvent</td> 
  </tr> 
  <tr> 
   <td>rateSelected</td> 
   <td>PlaybackRateEvent</td> 
   <td> </td> 
   <td>rateSelected</td> 
   <td>PlaybackRateEvent</td> 
  </tr> 
  <tr> 
   <td>ratePlaying</td> 
   <td>PlaybackRateEvent</td> 
   <td> </td> 
   <td>ratePlaying</td> 
   <td>PlaybackRateEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakSkipped</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakSkipped</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>adClicked<br /> Cuando el usuario hace clic en un anuncio.</td> 
   <td>AdClickedEvent</td> 
   <td> </td> 
   <td><p>Novedades en 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>profileChanged<br /> Cuando cambie el perfil de reproducción.</td> 
   <td>ProfileEvent</td> 
   <td> </td> 
   <td><p>Novedades en 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>seekPositionAdjusted<br /> Cuando la posición de búsqueda se ajusta debido a reglas internas o externas.</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td><p>Novedades en 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>audioUpdated<br /> Cuando se actualiza un elemento del reproductor de contenidos. Para determinados flujos que contienen pistas de audio detectables solo en el tiempo de reproducción, este evento se activa cuando hay nuevas pistas de audio disponibles.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novedades en 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>captionsUpdated <br /> Cuando se actualiza un elemento del reproductor de contenidos. Para los flujos en directo/lineales, el cliente debe actualizar periódicamente el recurso de medios para detectar el nuevo contenido disponible. Cuando esto sucede, algunas características de los medios pueden cambiar.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novedades en 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>masterUpdated <br /> Cuando se actualiza un elemento del reproductor de contenidos. Para los flujos en directo/lineales, el cliente debe actualizar periódicamente el recurso de medios para detectar el nuevo contenido disponible. Cuando esto sucede, algunas características de los medios pueden cambiar.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novedades en 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>playbackRangeUpdated<br /> Cuando se actualiza un elemento del reproductor de contenidos. Para los flujos en directo/lineales, el cliente debe actualizar periódicamente el recurso de medios para detectar el nuevo contenido disponible. Cuando esto sucede, algunas características de los medios pueden cambiar.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novedades en 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>timedEvent<br /> Se envía cuando se generan eventos temporizados.</td> 
   <td>TimedEvent</td> 
   <td> </td> 
   <td><p>Novedades en 2.0</p> </td> 
  </tr> 
 </tbody> 
</table>

### ABRControlParameters {#abrcontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaz ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ;<br /> const short sin signo ABR_POLICY_MODERATE = 1 ;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> attribute unsigned short abrPolicy;<br /> atributo unsigned int initialBitRate;<br /> atributo unsigned int minBitRate;<br /> atributo unsigned int maxBitRate;<br /> const unsigned short DEFAULT_ABR_INITIAL_BITRATE;<br /> const unsigned short DEFAULT_ABR_MIN_BITRATE;<br /> const unsigned short DEFAULT_ABR_MAX_BITRATE;<br /> const ABRPolicy DEFAULT_ABR_POLICY;<br /> };</p> </td> 
   <td><p>interfaz ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ;<br /> const short sin signo ABR_POLICY_MODERATE = 1 ;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> attribute unsigned short abrPolicy;<br /> atributo unsigned int initialBitRate;<br /> atributo unsigned int minBitRate;<br /> atributo unsigned int maxBitRate;<br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### BufferControlParameters {#buffercontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaz BufferControlParameters<br /> {<br /> attribute double initialBufferTime;<br /> attribute double playBufferTime;<br /> const double DEFAULT_INITIAL_BUFFER_TIME;<br /> const double DEFAULT_PLAY_BUFFER_TIME;<br /> };</p> </td> 
   <td><p>interfaz BufferControlParameters<br /> {<br /> attribute double initialBufferTime;<br /> attribute double playBufferTime;<br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TextFormat {#textformat}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0</td> 
   <td><p>interfaz TextFormat<br /> {<br /> // Color<br /> const unsigned short COLOR_DEFAULT = 0 ;<br /> const unsigned short COLOR_BLACK = 1 ;<br /> const unsigned short COLOR_GRAY = 2 ;<br /> const unsigned short COLOR_WHITE = 3 ;<br /> const short sin signo COLOR_BRIGHT_WHITE = 4 ;<br /> const unsigned short COLOR_DARK_RED = 5 ;<br /> const unsigned short COLOR_RED = 6 ;<br /> const unsigned short COLOR_BRIGHT_RED = 7 ;<br /> const unsigned short COLOR_DARK_GREEN = 8 ;<br /> const unsigned short COLOR_GREEN = 9 ;<br /> const unsigned short COLOR_BRIGHT_GREEN = 10 ;<br /> const short sin signo COLOR_DARK_BLUE = 11 ;<br /> const short sin signo COLOR_BLUE = 12 ;<br /> const unsigned short COLOR_BRIGHT_BLUE = 13 ;<br /> const unsigned short COLOR_DARK_YELLOW = 14 ;<br /> const unsigned short COLOR_YELLOW = 15 ;<br /> const unsigned short COLOR_BRIGHT_YELLOW = 16 ;<br /> const unsigned short COLOR_DARK_MAGENTA = 17 ;<br /> const unsigned short COLOR_MAGENTA = 18 ;<br /> const unsigned short COLOR_BRIGHT_MAGENTA = 19 ;<br /> const unsigned short COLOR_DARK_CYAN = 20 ;<br /> const unsigned short COLOR_CYAN = 21 ;<br /> const unsigned short COLOR_BRIGHT_CYAN = 22 ;<br /> <br /> readonly attribute unsigned short fontColor;<br /> readonly attribute unsigned short backgroundColor;<br /> readonly attribute unsigned short fillColor;<br /> atributo readonly unsigned short edgeColor;<br /> <br /> // Tamaño<br /> const unsigned short SIZE_DEFAULT = 0 ;<br /> const unsigned short SIZE_SMALL = 1 ;<br /> const unsigned short SIZE_MEDIUM = 2 ;<br /> const unsigned short SIZE_LARGE = 3 ;<br /> <br /> atributo readonly de tamaño corto sin signo;<br /> <br /> // FontEdge<br /> const unsigned short FONT_EDGE_DEFAULT = 0 ;<br /> const unsigned short FONT_EDGE_NONE = 1 ;<br /> const unsigned short FONT_EDGE_RAISED = 2 ;<br /> const unsigned short FONT_EDGE_DEPRESSED = 3 ;<br /> const unsigned short FONT_EDGE_UNIFORM = 4 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_LEFT = 5 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_RIGHT = 6 ;<br /> readonly attribute unsigned short fontEdge;<br /> <br /> // Fuente<br /> const unsigned short FONT_DEFAULT = 0 ;<br /> const unsigned short FONT_MONOSPACED_WITH_SERIFS = 1 ;<br /> const unsigned short FONT_PROPORTIONAL_WITH_SERIFS = 2 ;<br /> const unsigned short FONT_MONSPACED_WITHOUT_SERIFS = 3 ;<br /> const unsigned short FONT_CASUAL = 4 ;<br /> const unsigned short FONT_CURSIVE = 5 ;<br /> const unsigned short FONT_SMALL_CAPITALS = 6 ;<br /> fuente corta sin signo de atributo readonly;<br /> readonly attribute unsigned short fontOpacity;<br /> readonly attribute unsigned short backgroundOpacity;<br /> readonly attribute unsigned short fillOpacity;<br /> atributo readonly sin signo short DEFAULT_OPACITY;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### MediaPlayerItemLoader {#mediaplayeritemloader}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaz MediaPlayerItemLoader:<br /> {<br /> void load(Recurso MediaResource, resourceId largo,<br /> Listener ItemLoaderListener, <br /> MediaPlayerItemConfig (configuración) ;<br /> void cancel();<br /> atributo de solo lectura MediaPlayerItem currentItem;<br /> };</p> </td> 
   <td>Nuevo para 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interfaz ItemLoaderListener<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc;<br /> //onErrorCallbackFunc(PSDKErrorCode)<br /> var onErrorCallbackFunc;<br /> }</p> </td> 
   <td>Nuevo para 2.0</td> 
  </tr> 
 </tbody> 
</table>

## Cambios en el elemento de API de características de medios para 2.0 {#media-characteristics-api-element-changes-for}

Estas tablas comparan los elementos de API característicos de medios para el TVSDK de C++ entre las versiones 1.3 y 2.0.

Tablas de este tema:

* MediaPlayerItem
* Pista, Pista de audio, Pista de subtítulos
* Perfil
* DTMetadataInfo

### MediaPlayerItem {#mediaplayeritem}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaz MediaPlayerItem {<br /> atributo de solo lectura MediaResource;<br /> resourceId largo de atributo de solo lectura;<br /> read only attribute boolean live;<br /> <br /> el atributo booleano de solo lectura hasAlternateAudio;<br /> atributo de solo lectura AudioTrackList audioTracks;<br /> atributo de solo lectura AudioTrack selectedAudioTrack;<br /> void selectAudioTrack(AudioTrack track); <br /> <br /> atributo booleano de solo lectura hasClosedCaptions;<br /> atributo de solo lectura ClosedCaptionsTrackList closedCaptionsTracks;<br /> atributo de solo lectura ClosedCaptionsTrack selectedClosedCaptionsTrack;<br /> void selectClosedCaptionsTrack(<br /> ClosedCaptions (Track track); <br /> <br /> atributo booleano de solo lectura hasTimedMetadata;<br /> atributo de solo lectura TimedMetadataList timedMetadata;<br /> atributo de solo lectura dinámico booleano;<br /> <br /> atributo de solo lectura booleano isProtected;<br /> atributo readonly DRmMetadataInfoList drmMetadataInfos;<br /> atributo de solo lectura ProfileList profiles;<br /> atributo de solo lectura Profile selectedProfile;<br /> <br /> atributo de solo lectura booleano trickPlaySupported;<br /> atributo de solo lectura FloatArray availablePlaybackRates;<br /> atributo readonly float selectedPlaybackRate;<br /> <br /> <br /> atributo de solo lectura MediaPlayer mediaPlayer;<br /> atributo de solo lectura MediaPlayerItemConfig config;<br /> };</p> </td> 
   <td><p>interfaz MediaPlayerItem {<br /> atributo de solo lectura MediaResource;<br /> resourceId largo de atributo de solo lectura;<br /> read only attribute boolean live;<br /> <br /> el atributo booleano de solo lectura hasAlternateAudio;<br /> atributo de solo lectura AudioTrackList audioTracks;<br /> attribute AudioTrack selectedAudioTrack;<br /> <br /> <br /> atributo booleano de solo lectura hasClosedCaptions;<br /> atributo de solo lectura ClosedCaptionsTrackList ccTracks;<br /> attribute ClosedCaptionsTrack selectedCCTrack;<br /> <br /> <br /> <br /> atributo booleano de solo lectura hasTimedMetadata;<br /> atributo de solo lectura TimedMetadataList timedMetadata;<br /> atributo de solo lectura dinámico booleano;<br /> <br /> atributo de solo lectura booleano isProtected;<br /> atributo readonly DRmMetadataInfoList drmMetadataInfos;<br /> atributo de solo lectura ProfileList profiles;<br /> <br /> <br /> atributo de solo lectura booleano trickPlaySupported;<br /> atributo readonly Int32Array availablePlaybackRates;<br /> <br /> atributo de solo lectura StringList adTags;<br /> <br /> atributo de solo lectura MediaPlayer mediaPlayer;<br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Seguimiento / AudioTrack / ClosedCaptionsTrack {#track-audiotrack-closedcaptionstrack}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Pista de interfaz<br /> {<br /> nombre DomString del atributo de solo lectura;<br /> lenguaje DomString de atributo readonly;<br /> atributo de solo lectura booleano predeterminado;<br /> atributo de solo lectura booleano autoSelect;<br /> }; </p> </td> 
   <td>Nuevo para 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interfaz AudioTrack : Track<br /> {<br /> nombre de DomString de atributo de solo lectura; //FromTrack<br /> atributo de solo lectura DomString language;//FromTrack<br /> atributo de solo lectura booleano predeterminado; // From Track<br /> atributo de solo lectura booleano autoSelect;//FromTrack<br /> <br /> atributo readonly sin signo int pid;<br /> };</p> </td> 
   <td><p>interfaz AudioTrack<br /> {<br /> nombre DomString del atributo de solo lectura;<br /> lenguaje DomString de atributo readonly; <br /> atributo de solo lectura booleano predeterminado;<br /> atributo de solo lectura booleano autoSelect;<br /> atributo booleano de solo lectura forzado;<br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0</td> 
   <td><p>interfaz AudioTrackList<br /> {<br /> atributo readonly de larga longitud sin signo;<br /> getter AudioTrack (índice largo sin signo);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface ClosedCaptionsTrack : Track<br /> {<br /> nombre de DomString de atributo de solo lectura; //FromTrack<br /> atributo de solo lectura DomString language;//FromTrack<br /> atributo de solo lectura booleano predeterminado; // FromTrack<br /> atributo de solo lectura booleano autoSelect;//FromTrack<br /> <br /> <br /> const unsigned short SERVICE_608_CAPTIONS = 0;<br /> const unsigned short SERVICE_708_CAPTIONS = 1;<br /> const unsigned short SERVICE_WEB_VTT_CAPTIONS = 2;<br /> readonly attribute unsigned short serviceType;<br /> atributo booleano de solo lectura forzado;<br /> };</p> </td> 
   <td><p>interfaz ClosedCaptionsTrack<br /> {<br /> nombre DomString del atributo de solo lectura;<br /> lenguaje DomString de atributo readonly;<br /> atributo de solo lectura booleano predeterminado;<br /> <br /> <br /> atributo de solo lectura booleano activo;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0</td> 
   <td><p>interfaz ClosedCaptionsTrackList<br /> {<br /> atributo readonly de larga longitud sin signo;<br /> getter ClosedCaptionsTrack(índice largo sin signo);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Perfil {#profile}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>Perfil: sin cambios para 2.0</td> 
   <td><p>Perfil de interfaz<br /> {<br /> atributo readonly ancho int sin firmar;<br /> atributo readonly sin signo int height;<br /> atributo de solo lectura unsigned int bitRate;<br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td>ProfileList: sin cambios para 2.0</td> 
   <td><p>interfaz ProfileList<br /> {<br /> atributo readonly de larga longitud sin signo;<br /> getter Profile(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DTMetadataInfo {#drmmetadatainfo}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><strong>DTMetadataInfo</strong>: Sin cambios para 2.0</td> 
   <td><p>interfaz DRMMetadataInfo<br /> { <br /> atributo de solo lectura metadatos DRMMetadata;<br /> atributo de solo lectura long prefetchTimestamp;<br /> atributo de solo lectura TimeRange timeRange;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DTMetadataInfoList</strong>: Sin cambios para 2.0</td> 
   <td><p>interfaz DRMMetadataInfoList<br /> {<br /> atributo readonly de larga longitud sin signo;<br /> getter DRMMetadataInfo(índice largo sin signo);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## Asignar errores de C++ a excepciones en diferentes idiomas {#mapping-c-errors-to-exceptions-in-different-languages}

Puede asignar códigos de error de C++ a excepciones en diferentes idiomas.

El PSDK de C++ tiene una directiva &quot;no throw&quot; para sus API. La mayoría de los métodos API devuelven un valor PSDKErrorCode para indicar si el método se ejecutó correctamente. Los errores asincrónicos se notifican mediante los eventos de error.

El ActionScript y el PSDK de JAVA tienen una directiva diferente. La mayoría de los errores producirán una excepción ArgumentError o IllegalStateException para indicar que no se pudo ejecutar la parte sincrónica del método. Estas excepciones no se detectan y el código de la aplicación es responsable de administrarlas. Normalmente contienen información útil sobre por qué ha fallado la llamada al método. Por ejemplo, si se llama al comando prepareToPlay en un estado no válido, se produce la siguiente excepción:

```shell
throw new IllegalStateException("Invalid player state. prepareToPlay method 
must be called only once after replaceCurrentItem or replaceCurrentResource method.");
```

El ActionScript/JAVA también genera excepciones de los constructores para indicar que algún objeto interno se creó incorrectamente. Estas excepciones se gestionan internamente y no se propagan a la aplicación. Las excepciones se incluyen en una notificación de advertencia que se envía a la aplicación

Por ejemplo, si no se encontró ningún archivo multimedia válido para la respuesta de anuncio recibido, no se puede crear ningún objeto de recurso de anuncio o anuncio válido. Como resultado, no se coloca ningún anuncio en la cronología y se envía una notificación NotificationEvent.OperationFailed.

Los códigos de error o advertencia que se reciben de forma asíncrona desde el Motor de vídeo de Adobe (AVE) se envían a la aplicación como eventos normales. El evento de notificación contiene todos los códigos de error recibidos y cualquier metadato adicional, como la dirección URL, el identificador de recurso, el identificador, etc. Si el error es grave y la reproducción del contenido actual no puede continuar, MediaPlayer pasa al estado ERROR y se envía el evento onStatusChanged o MediaPlayerStatusChanged.STATUS_CHANGED. Si la reproducción puede continuar, se envía un evento de notificación normal.

<table> 
 <tbody> 
  <tr> 
   <th>Error de C++ (código de error PSDKE)</th> 
   <th> </th> 
   <th>Java</th> 
   <th>ActionScript</th> 
   <th>JavaScript</th> 
  </tr> 
  <tr> 
   <td>kECInvalidArgument</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ArgumentError</td> 
   <td>Excepción con código = 1, descripción = "INVALID_ARGUMENT" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNullPointer</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ArgumentError</td> 
   <td>Excepción con código = 2, descripción = "GENERIC_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECIllegalState</td> 
   <td> </td> 
   <td>IllegalStateException</td> 
   <td>IllegalStateException</td> 
   <td>Excepción con código = 3, descripción = "ILLEGAL_STATE" y additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInterfaceNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 4, descripción = "GENERIC_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCreationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 5, descripción = "CREATION_FAILED" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedOperation</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 5, descripción = "CREATION_FAILED" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECDataNotAvailable</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 7, descripción = "DATA_NOT_AVAILABLE" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECSeekError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 8, descripción = "SEEK_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedFeature</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 9, descripción = "UNSUPPORTED_FEATURE" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECRangeError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 10, descripción = "RANGE_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCodecNotSupported</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 11, descripción = "CODEC_NOT_SUPPORTED" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECMediaError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 12, descripción = "MEDIA_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNetworkError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 13, descripción = "NETWORK_ERROR" y additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECGenericError</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Error o MediaPlayerNotification.Warning</td> 
   <td>MediaError o NotificationEvent</td> 
   <td>Excepción con código = 14, descripción = "GENERIC_ERROR" y additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInvalidSeekTime</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 15, descripción = "INVALID_SEEK_TIME" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAudioTrackError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 16, descripción = "AUDIO_TRACK_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAccessFromDifferent<p>ThreadError</p> </td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 17, descripción = "GENERIC_ERROR" y additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECElementNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 18, descripción = "GENERIC_ERROR" y additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNotImplemented</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 19, descripción = "GENERIC_ERROR" y additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECPlaybackOperationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 200, descripción = "PLAYBACK_OPERATION_FAILED" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNativeWarning</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>NotificationEvent</td> 
   <td>Excepción con código = 201, descripción = "NATIVE_WARNING" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAdResolverFailed</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>-</td> 
   <td>Excepción con código = 202, descripción = "AD_RESOLVER_FAILED" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
 </tbody> 
</table>

## Cambios en los elementos de la API de utilidad y ayuda para 2.0 {#utility-and-helper-api-element-changes-for}

Estas tablas comparan los elementos de la API de utilidad y ayuda del TVSDK de JavaScript entre las versiones 1.3 y 2.0.

Tablas de este tema:

* Versión
* TimeRange
* QOSProvider
* DeviceInformation
* LoadInfo
* Ver
* InformaciónDeReproducción

### Versión {#version}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Versión de interfaz<br /> {<br /> atributo de solo lectura versión DomString;<br /> atributo de solo lectura DomString description;<br /> atributo de solo lectura long major;<br /> atributo readonly long minor;<br /> revisión larga de atributo de solo lectura;<br /> atributo de solo lectura long apiVersion;<br /> };</p> </td> 
   <td><p>Versión de interfaz<br /> {<br /> atributo de solo lectura versión DomString;<br /> atributo de solo lectura DomString description;<br /> atributo de solo lectura DomString principal;<br /> atributo de solo lectura DomString minor;<br /> revisión DomString del atributo de solo lectura;<br /> atributo de solo lectura DomString apiVersion;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TimeRange {#timerange}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0</td> 
   <td><p>intervalo de tiempo de interfaz<br /> {<br /> readonly attribute unsigned long begin;<br /> atributo readonly de extremo largo sin signo;<br /> atributo readonly de larga duración sin signo;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### QOSProvider {#qosprovider}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0</td> 
   <td><p>interfaz QOSProvider<br /> {<br /> void attachMediaPlayer(MediaPlayer player);<br /> void detachMediaPlayer();<br /> <br /> atributo de solo lectura DeviceInformation deviceInformation;<br /> atributo readonly PlaybackInformation playbackInformation;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DeviceInformation {#deviceinformation}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaz DeviceInformation<br /> {<br /> atributo de solo lectura DomString os;<br /> <br /> <br /> <br /> id de DomString de atributo de solo lectura;<br /> atributo de solo lectura int densidadDPI;<br /> atributo readonly int heightPixels;<br /> atributo readonly int widthPixels;<br /> atributo de solo lectura booleano seekToKeyFrame;<br /> };</p> </td> 
   <td><p>interfaz DeviceInformation<br /> {<br /> atributo de solo lectura DomString os;<br /> atributo readonly int sdk;<br /> modelo DomString de atributo de solo lectura;<br /> fabricante del atributo DomString de solo lectura;<br /> id de DomString de atributo de solo lectura;<br /> atributo de solo lectura int densidadDPI;<br /> atributo readonly int heightPixels;<br /> atributo readonly int widthPixels;<br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### LoadInfo {#loadinfo}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0</td> 
   <td><p>interfaz LoadInfo<br /> {<br /> url de DomString de atributo de solo lectura;<br /> atributo de solo lectura int size;<br /> atributo de solo lectura double downloadDuration;<br /> atributo readonly int periodIndex;<br /> atributo de solo lectura double mediaDuration;<br /> atributo readonly short TRACK_TYPE_FRAGMENT;<br /> atributo readonly short TRACK_TYPE_TRACK;<br /> atributo readonly short TRACK_TYPE_MANIFEST;<br /> tipo corto de atributo de solo lectura;<br /> atributo de solo lectura DomString trackName;<br /> atributo de solo lectura DomString trackType;<br /> atributo de solo lectura int trackIndex;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Ver {#view}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0</td> 
   <td><p>Vista de interfaz<br /> {<br /> atributo readonly x corta sin signo;<br /> atributo readonly sin signo corto y;<br /> atributo readonly de anchura corta sin signo;<br /> atributo readonly de altura corta sin signo;<br /> <br /> void setSize(ancho corto sin signo, alto corto sin signo);<br /> void setPos(unsigned short x, unsigned short y);<br /> }</p> </td> 
  </tr> 
 </tbody> 
</table>

### InformaciónDeReproducción {#playbackinformation}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>información de reproducción de interfaz<br /> {<br /> atributo readonly double timeToFirstByte;<br /> atributo de solo lectura double timeToLoad;<br /> atributo readonly double timeToStart;<br /> atributo de solo lectura double timeToFail;<br /> atributo readonly int totalSecondsPlayed;<br /> atributo readonly int totalSecondsSpent;<br /> atributo readonly double frameRate;<br /> atributo readonly int droppedFrameCount;<br /> readonly attribute int percibidoBandwidth;<br /> atributo de solo lectura int bitrate;<br /> atributo readonly double bufferTime;<br /> atributo readonly int bufferLength;<br /> readonly attribute int emptyBufferCount;<br /> atributo readonly double bufferingTime;<br /> };</p> </td> 
   <td><p>información de reproducción de interfaz<br /> {<br /> atributo readonly double timeToFirstByte;<br /> atributo de solo lectura double timeToLoad;<br /> atributo readonly double timeToStart;<br /> atributo de solo lectura double timeToFail;<br /> atributo readonly int totalSecondsPlayed;<br /> atributo readonly int totalSecondsSpent;<br /> atributo readonly double frameRate;<br /> atributo readonly int droppedFrameCount;<br /> <br /> atributo de solo lectura int bitrate;<br /> atributo readonly double bufferTime;<br /> atributo readonly int bufferLength;<br /> readonly attribute int emptyBufferCount;<br /> atributo readonly double bufferingTime;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en [Formación y asistencia de Adobe Primetime](https://helpx.adobe.com/support/primetime.html) página.
