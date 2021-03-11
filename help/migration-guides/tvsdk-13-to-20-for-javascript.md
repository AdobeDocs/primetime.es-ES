---
title: 'Conversión de TVSDK: 1.3 a 2.0 para JavaScript'
description: Muchas firmas de métodos y nombres de elementos de API han cambiado para 2.0. Revise estas tablas para ver todos los detalles de los cambios de API.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: migration
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '5034'
ht-degree: 0%

---


# Conversión de TVSDK: 1.3 a 2.0 para JavaScript {#tvsdk-conversion-to-for-javascript}

Muchas firmas de métodos y nombres de elementos de API han cambiado para 2.0. Revise estas tablas para ver todos los detalles de los cambios de API.

## Implementar funciones de llamada de retorno en JavaScript {#implement-callback-functions-in-javascript}

Los comentarios en la documentación del método sugieren la firma de llamadas de retorno que debe implementar.

Para JavaScript, la sintaxis de la API se basa en el ID web. Para una interfaz TVSDK, los nombres de método se llaman *methodName*(). Para que la aplicación implemente métodos, se agrega a la interfaz un atributo de lectura y escritura llamado *methodName* CallbackFunc y la aplicación debe configurarlo para que apunte a una función que implemente el método . Por ejemplo:

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

## Cambios en los elementos de la API del flujo de trabajo de publicidad para 2.0 {#advertising-workflow-api-element-changes-for}

En estas tablas se comparan los elementos de API del flujo de trabajo de publicidad para el SDK de TVSDK de JavaScript entre las versiones 1.3 y 2.0.

Tablas en este tema:

* TimedMetadata
* AdSignalingMode
* AdvertisingMetadata
* CustomRangeMetadata
* ReplaceTimeRange
* Colocación
* Oportunidad
* Reserva
* Línea de tiempo / Elemento de línea de tiempo / Marcador de línea de tiempo
* AdBreak
* Ad / AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset
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
   <td><p> <strong>Metadatos</strong> temporizados: interface TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0 ;  <br /> const unsigned short METADATA_TYPE_ID3 = 1 ;  <br /> atributo de sólo lectura tipo corto sin signo;  <br /> atributo de sólo lectura durante mucho tiempo;<br /> atributo de solo lectura DomString id;<br /> atributo de solo lectura DomString name;<br /> atributo de solo lectura DomString content;  <br /> atributo de solo lectura Metadatos de objeto;<br /> }; </p> </td> 
   <td><p>interface TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0 ;<br /> const unsigned short METADATA_TYPE_ID3 = 1 ;<br /> atributo readonly no firmado short metadataType;<br /> atributo readonly durante mucho tiempo;<br /> readonly attribute long id;<br /> readonly attribute DomString name; a6/&gt; <br /> atributo readonly metadatos de objeto;<br /> };<br /></p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetadataList</strong>: (Sin cambio para 2.0)</td> 
   <td><p>interface TimedMetadataList {<br /> atributo de solo lectura sin signo de longitud larga;<br /> getter TimedMetadata(índice largo sin signo);<br /> };</p> </td> 
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
   <td>Esto reemplaza la clave MetadataKeys::MANIFEST_CUES .</td> 
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
   <td><p>Interface AdvertisingMetadata { <br /> atributo AdSignalingMode modo; <br /> atributo AdBreakWatchedPolicy adBreakAsWatched; <br /> atributo booleano livePreroll; <br /> atributo booleano delayAdLoading ; <br /> };</p> </td> 
   <td>Esta funcionalidad fue proporcionada por<p>MetadataKeys::ADVERTISING_METADATA</p> key.</td> 
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
   <td><p>Interface CustomRangeMetadata { <br /> const unsigned short TYPE_MARK_RANGE; <br /> const unsigned short TYPE_DELETE_RANGE; <br /> const unsigned short TYPE_REPLACE_RANGE; <br /> atributo tipo corto sin signo; <br /> atributo booleano adaptSeekPosition; <br /> atributo TimeRangeList timeRangeList; <br /> };</p> </td> 
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
   <td><p>interface ReplaceTimeRange { <br /> atributo unsigned long begin; <br /> atributo de sólo lectura de fin largo sin firmar; <br /> atributo de duración larga sin firmar; <br /> atributo replaceDuration largo sin firmar; <br /> };</p> </td> 
   <td>(Nuevo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### Colocación {#placement}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Ubicación de la interfaz { <br /> const unsigned short TYPE_MID_ROLL; <br /> const unsigned short TYPE_PRE_ROLL; <br /> const unsigned short TYPE_POST_ROLL; <br /> const unsigned short TYPE_SERVER_MAP; <br /> const short TYPE_CUSTOM_RANGE sin signo;<br /> atributo de sólo lectura tipo corto sin signo; <br /> atributo de solo lectura durante mucho tiempo; <br /> duración larga del atributo de solo lectura; <br /> const unsigned short MODE_DEFAULT; <br /> const unsigned short MODE_INSERT; <br /> const unsigned short MODE_REPLACE; <br /> const unsigned short MODE_DELETE; <br /> const unsigned short MODE_MARK; <br /> const unsigned short MODE_FREE_REPLACE; <br /> atributo de solo lectura no firmado modo corto; <br /> intervalo de tiempo del atributo de sólo lectura; <br /> };</p> </td> 
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
   <td><p>oportunidad de interfaz { <br /> atributo de solo lectura DomString id; <br /> ubicación del atributo de solo lectura; <br /> atributo de sólo lectura Configuración de objetos; <br /> atributo de sólo lectura Object customParameters; <br /> }; </p> </td> 
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
   <td><p>interfaz Reserva { <br /> atributo de sólo lectura intervalo de tiempo; <br /> atributo de sólo lectura larga retención; <br /> }; </p> </td> 
   <td> (Nuevo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### Línea de tiempo / Elemento de línea de tiempo / Marcador de línea de tiempo {#timeline-timelineitem-timelinemarker}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p><strong>Cronología</strong>: interfaz Escala de tiempo  <br /> { atributo de sólo lectura Escala de tiempoMarcadorLista de cronogramasMarcadores;  <br /> atributo readonly TimelineItemList línea de tiempoItems;  <br /> double ConvertToLocalTime( doble hora);  <br /> double convertedToVirtualTime( doble hora);  <br /> };</p> </td> 
   <td><p>interfaz Línea de tiempo {<br /> atributo de sólo lectura TimelineMarkerList línea de tiempoMarkers;<br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>TimelineItem</strong>: interfaz TimelineItem : <br /> TimelineMarker {<br /> readonly attribute long id;  <br /> atributo de sólo lectura TimeRange virtualRange;  <br /> atributo de sólo lectura TimeRange localRange;  <br /> booleano de atributos de solo lectura visto;  <br /> el atributo de solo lectura es booleano;  <br /> }; </p> </td> 
   <td>(Nuevo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><strong>Marcador de cronología</strong>: (Sin cambio para 2.0)</td> 
   <td><p>interface TimelineMarker {<br /> atributo readonly doble tiempo;<br /> doble duración del atributo readonly;<br /> };</p> </td> 
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
   <td><p>interfaz AdBreak {<br /> <br /> <br /> <br /> atributo readonly doble duración;<br /> anuncios AdList de atributos de lectura solamente;<br /> <br /> <br /> atributo de sólo lectura AdInsertionType insertionType;<br /> }; </p> </td> 
   <td><p>interfaz AdBreak {<br /> atributo de sólo lectura doble tiempo;<br /> atributo de solo lectura doble replaceDuration;<br /> <br /> doble duración del atributo de solo lectura;<br /> atributo de solo lectura AdList;<br /> <br /> atributo de solo lectura DomString data;<br /> <br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### Ad / AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset {#ad-adasset-adclick-adlist-adassetlist-adbannerasset}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p> <strong>Publicidad</strong>: anuncio de interfaz {<br /> readonly attribute AdAsset primaryAsset;<br /> readonly attribute AdAssetList CompanionAssets;<br /> <br /> readonly attribute double duration;atributo de <br /> lectura DomString id;<br /> const unsigned short ADTYPE_LINEAR = 0 ;<br /> const unsigned short ADTYPE_NONLINEAR = 1 ;<br /> <br /> atributo de sólo lectura tipo de anuncio corto sin signo;<br /> atributo de solo lectura AdInsertionType adInsertionType;  <br /> <br /> se puede hacer clic en booleano del atributo de solo lectura;  <br /> el atributo de solo lectura booleano isCustomAdMarker;<br /> }; </p> </td> 
   <td><p>anuncio de interfaz {<br /> atributo de solo lectura AdAsset primaryAsset;<br /> atributo de solo lectura AdAssetList CompanionAssets;<br /> <br /> doble duración del atributo de solo lectura;<br /> atributo de solo lectura DomString id;<br /> const corto sin firmar ADTYPE_LINEAR = 0 ;<br /> const corto sin firmar ADTYPE_NTIPO LINEAR = 1 ;<br /> <br /> atributo de sólo lectura tipo corto sin signo;<br /> atributo de solo lectura AdInsertionType insertionType; <br /> rastreador de objetos de atributo de sólo lectura;<br /> <br /> <br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>: (Sin cambio para 2.0)</td> 
   <td><p>interfaz AdAsset {<br /> atributo de sólo lectura DomString id;<br /> doble atributo de solo lectura duración;<br /> atributo de solo lectura MediaResource recurso;<br /> atributo de solo lectura AdClick adClick;<br /> metadatos de objeto de atributo de solo lectura;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>: (Sin cambio para 2.0)</td> 
   <td><p>interfaz AdClick {<br /> atributo de sólo lectura DomString id;<br /> atributo de solo lectura DomString title;<br /> atributo de solo lectura DomString url;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdList</strong>: (Sin cambio para 2.0)</td> 
   <td><p>interfaz AdList {<br /> atributo de sólo lectura longitud sin signo;<br /> getter Ad(índice largo sin signo);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>: (Sin cambio para 2.0)</td> 
   <td><p>interfaz AdAssetList {<br /> atributo de sólo lectura de longitud sin signo;<br /> getter AdAsset(índice largo sin signo);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>: interfaz AdBannerAsset : AdAsset<br /> {<br /> readonly attribute int width;<br /> readonly attribute int height;atributo <br /> readonly DomString staticUrl;<br /> readonly attribute DomString height;<br /> readonly attribute DomString width;<br /> };</p> </td> 
   <td> Novedades de 2.0</td> 
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
   <td><p> <strong>AdBreakTimelineItem</strong>: interfaz AdBreakTimelineItem : TimelineItem {  <br /> atributo de sólo lectura AdBreak adBreak;  <br /> elementos AdTimelineItemList de atributo de solo lectura;  <br /> }; </p> </td> 
   <td> (Nuevo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimelineItem</strong>: interfaz AdTimelineItem : TimelineItem {  <br /> atributo de sólo lectura AdBreak adBreak;  <br /> anuncio de atributo de solo lectura;  <br /> }; </p> </td> 
   <td> (Nuevo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>: interfaz AdBreakTimelineItemList {  <br /> atributo readonly longitud sin signo;  <br /> get AdBreakTimelineItem (índice de registro sin firmar);  <br /> };</p> </td> 
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
   <td><p>interfaz AdBreakPolicy {<br /> atributo readonly corto AD_BREAK_POLICY_SKIP;<br /> atributo readonly corto AD_BREAK_POLICY_PLAY;<br /> atributo readonly corto AD_BREAK_POLICY_REMOVE;<br /> atributo readonly corto AD_BREAK_POLICY_REMOVE_AFTER_PLAY;<br /> };</p> </td> 
   <td><p> interfaz AdPolicyConstants {<br /> atributo readonly corto AD_BREAK_POLICY_SKIP;<br /> atributo readonly corto AD_BREAK_POLICY_PLAY;<br /> atributo readonly corto AD_BREAK_POLICY_REMOVE;<br /> atributo readonly corto AD_BREAK_POLICY_REMOVE VE_AFTER_PLAY;}<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p> interfaz AdBreakWatchedPolicy {<br /> atributo readonly corto AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> atributo readonly corto AD_BREAK_AS_WATCHED_ON_END;<br /> atributo readonly corto AD_BREAK_AS_WATCHED_NEVER;<br /> }; </p> </td> 
   <td><p> ...<br /> atributo de sólo lectura corto AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> atributo de sólo lectura corto AD_BREAK_AS_WATCHED_ON_END;<br /> atributo de sólo lectura corto AD_BREAK_AS_WATCHED_NEVER;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaz AdPolicy {<br /> atributo readonly corto AD_POLICY_PLAY;<br /> atributo readonly corto AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> atributo readonly corto AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN; atributo de sólo lectura atributo corto AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> <br /> atributo de sólo lectura corto AD_POLICY_SKIP_AD_BREAK;<br /> };</p> </td> 
   <td><p> ... <br /> atributo de sólo lectura atributo corto AD_POLICY_PLAY;<br /> atributo de sólo lectura corto AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> atributo de sólo lectura corto AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;<br /> atributo de sólo lectura corto AD_POLICY_SKIP_TO_TO _AD_IN_BREAK;<br /> atributo de sólo lectura corto AD_POLICY_SKIP_AD_BREAK;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaz AdPolicyMode {<br /> atributo readonly corto AD_POLICY_MODE_PLAY;<br /> atributo readonly corto AD_POLICY_MODE_SEEK;<br /> atributo readonly corto AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
   <td><p> ...<br /> {readonly attribute short AD_POLICY_MODE_PLAY;<br /> readonly attribute short AD_POLICY_MODE_SEEK;<br /> readonly attribute short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaz AdPolicyInfo {<br /> atributo de sólo lectura AdBreakTimelineItemList <br /> adBreakTimelineItems;<br /> atributo de solo lectura AdTimelineItem adTimelineItem;<br /> atributo de solo lectura currentTime;<br /> atributo de solo lectura seekToTime;<br /> tasa doble de atributo de lectura;&lt;a4; a6/&gt; modo corto de atributo de sólo lectura; //AdPolicyMode<br /> };<br /></p> </td> 
   <td><p>interfaz AdPolicyInfo {<br /> atributo de solo lectura AdBreakPlacementList <br /> adBreakPlacements;<br /> anuncio de atributo de solo lectura;<br /> atributo de solo lectura currentTime;<br /> atributo de solo lectura seekToTime;<br /> tasa doble de atributo de solo lectura;<br /> modo corto de atributo de solo lectura; //AdPolicyMode<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaz AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo SelectPolicyForAdBreakCallbackFunc;<br /> /*<br /> * AdPolicy TimelineItemList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectAdBreaksToPlayCallbackFunc;<br /> /*<br /> * AdPolicy selectForSeekInek toAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectPolicyForSeekIntoAdCallbackFunc; <br /> /**<br /> * AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectWatchedPolicyForAdBreakCallbackFunc;<br /> };</p> </td> 
   <td><p>interfaz AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo SelectPolicyForAdBreakFuncCallback;<br /> /*<br /> * AdPolicy PlacementList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectAdBreaksToPlayCallback;<br /> /*<br /> * AdPolicy selectPolicyForSeekIntoAd AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectPolicyForSeekIntoAdCallback; <br /> /**<br /> * AdBreakAsWatched selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Objeto selectWatchedPolicyForAdBreakCallback;&lt;a 19/&gt; };<br /></p> </td> 
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
   <td><p>interfaz TimelineOperation { <br /> readonly atributo ubicación ; <br /> };</p> </td> 
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
   <td><p>interfaz AdBreakPlacement : TimelineOperation {<br /> atributo de sólo lectura AdBreak;<br /> ubicación del atributo de solo lectura Colocación; // Desde TimelineOperation<br /> atributo readonly doble time;<br /> doble duración del atributo readonly;<br /> };</p> </td> 
   <td><p>interfaz AdBreakPlacement {<br /> atributo de solo lectura AdBreak adBreak;<br /> ubicación del atributo de solo lectura;<br /> tiempo doble del atributo de solo lectura;<br /> duración doble del atributo de solo lectura;<br /> };</p> </td> 
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
   <td><p>interfaz AuditudeSettings : AdvertisingMetadata { <br /> atributo DomString zoneId; <br /> atributo DomString mediaId; <br /> atributo DomString defaultMediaId ; <br /> atributo dominio DomString ; <br /> atributo Object targetInfo ; <br /> atributo Parámetros personalizados de objeto ; <br /> atributo Boolean creativePackaingEnabled ;<br /> atributo Boolean showStaticBanners ;<br /> };</p> </td> 
   <td>La funcionalidad la proporcionó la clave MetadataKeys::AUDITUDE_METADATA_KEY.</td> 
  </tr> 
 </tbody> 
</table>

## Cambios en los elementos de la API de personalización para 2.0 {#customization-api-element-changes-for}

Estas tablas comparan los elementos de API de personalización para el SDK de JavaScript entre las versiones 1.3 y 2.0.

Tablas en este tema:

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
   <td><p>interfaz MediaPlayerItemConfig {<br /> atributo ContentFactory adFactory;<br /> atributo StringList subscribeTags;<br /> <br /> atributo StringList adTags;<br /> <br /> <br /> atributo AdSignalingMode adSignalingMode;<br /> atributo CustomRangeMetadata customRange ;<br /> atributo NetworkConfiguration networkConfiguration;<br /> atributo AdvertisingMetadata advertisingMetadata;<br /> atributo Boolean useHardwareDecoder;<br /> };</p> </td> 
   <td><p>interfaz MediaPlayerConfig {<br /> <br /> <br /> <br /> atributo StringList adTags;<br /> atributo StringList subscribedTags;<br /> atributo MediaPlayerClientFactory clientFactory;<br /> <br /> <br /> <br /> <br /> <br /> 1/&gt; };</p> </td> 
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
   <td><p>interfaz ContentFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * elemento MediaPlayerItem);<br /> */<br /> atributo RecuperarAdPolicySelectorCallbackFunc;<br /> };</p> </td> 
   <td><p>interfaz MediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * elemento MediaPlayerItem);<br /> */<br /> atributo RecuperarAdPolicySelectorFunc;<br /> };</p> </td> 
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
   <td><p>interfaz NetworkConfiguration<br /> {<br /> atributo booleano forceNativeNetworking;<br /> atributo booleano useRedirectUrl;<br /> atributo Object cookieHeader;<br /> atributo booleano readSetCookieHeader;<br /> atributo int masterUpdateInterval; <br /> atributo booleano useCookieHeaderForAllRequests;<br /> atributo int readLimit;<br /> };</p> </td> 
   <td>En la versión 1.3, algunas de estas funciones las proporcionaban MetadataKeys</td> 
  </tr> 
 </tbody> 
</table>

## Cambios en los elementos de la API DRM para 2.0 {#drm-api-element-changes-for}

Estas tablas comparan los elementos de la API DRM para el SDK de TVSDK de JavaScript entre las versiones 1.3 y 2.0.

Tablas en este tema:

* Inicialización del flujo de trabajo de DRM
* DRMAcquireLicenseSettings / DRMAuthauthenticationMethod
* DRMMetadata
* DRMPlaybackTimeWindow
* DRMLicense
* DRMLicenseDomain
* DRMPolicy
* DRMManager

### Inicialización del flujo de trabajo DRM {#drm-workflow-initialization}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>La aplicación debe llamar a AdobePSDK.initiateDRMWorkflow para iniciar el flujo de trabajo de DRM. Sin esta llamada, los vídeos DRM no se reproducirán.<p>interfaz AdobePSDK<br /> {<br /> void initiateDRMWorkFlow(<br /> DomString appStoratePath, <br /> DomString publisherId, <br /> DomString appId, <br /> DomString appVersion, <br /> privacidad booleanaModeOn);<br /> };</p> </td> 
   <td>La inicialización se realizó internamente y no se requería ninguna llamada explícita.</td> 
  </tr> 
 </tbody> 
</table>

### DRMAcquireLicenseSettings/DRMAuthauthenticationMethod {#drmacquirelicensesettings-drmauthenticationmethod}

| API 2.0 | API 1.3 |
|--- |--- |
| **DRMAcquireLicenseSettings** |  |
| Sin cambios para 2.0. | enum DRMAcquireLicenseSettings <br>{<br> const unsigned int FORCE_REFRESH = 0;<br> const unsigned int LOCAL_ONLY = 1;<br> const unsigned int ALLOW_SERVER = 2;<br> }; |
| **DRMAuthauthenticationMethod** |  |
| Sin cambios para 2.0. | enum DRMAuthauthenticationMethod <br>{<br> const unsigned int UNKNOWN = 0;<br> const unsigned int ANONYMOUS = 1;<br> const unsigned int USERNAME_AND_PASSWORD = 2;<br> } |

### DRMMetadata {#drmmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0.</td> 
   <td><p>interfaz DRMMetadata<br /> {<br /> atributo de sólo lectura DomString serverUrl;<br /> atributo de solo lectura DomString licenseId;<br /> atributo de solo lectura DRMPolicyArray directivas; <br /> };</p> </td> 
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
   <td><p>interfaz DRMPlaybackTimeWindow {<br /> atributo de sólo lectura en playPeriodInSeconds;<br /> atributo de solo lectura long playStartDate;<br /> atributo de solo lectura long playEndDate;<br /> };</p> </td> 
   <td><p>interfaz DRMPlaybackTimeWindow {<br /> atributo de sólo lectura int periodInSeconds;<br /> atributo de sólo lectura int startDate;<br /> atributo de sólo lectura int endDate;<br /> };</p> </td> 
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
   <td><p>interfaz DRMLicense {<br /> atributo de sólo lectura Uint8Array bytes;<br /> atributo de sólo lectura Date licenseStartDate;<br /> atributo de sólo lectura Date licenseEndDate;<br /> atributo de sólo lectura Date offlineStorageStartDate;<br /> atributo de sólo lectura Fecha offlineStorageEndDate; <br /> atributo de sólo lectura DomString serverUrl;<br /> atributo de sólo lectura DomString licenseID;<br /> atributo de solo lectura DomString policyID;<br /> atributo de solo lectura DRMPlaybackTimeWindow playTimeWindow;<br /> atributo de sólo lectura Object customProperties;<br /> }; </p> </td> 
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
   <td><p>interfaz DRMLicenseDomain {<br /> atributo readonly DomString authenticationDomain;<br /> atributo readonly DRMAuthauthenticationMethod authenticationMethod; <br /> atributo de sólo lectura DomString serverUrl;<br /> };</p> </td> 
   <td><p>interfaz DRMLicenseDomain {<br /> atributo de sólo lectura DomString authDomain;<br /> atributo de solo lectura DRMAuthauthenticationMethod authMethod; <br /> atributo de sólo lectura DomString serverURL;<br /> };</p> </td> 
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
   <td><p>interfaz DRMPolicy<br /> {<br /> atributo de sólo lectura DomString authenticationDomain;<br /> atributo de solo lectura DRMAuthauthenticationMethod authenticationMethod;<br /> <br /> atributo de solo lectura DomString displayName;<br /> atributo de solo lectura DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
   <td><p>interfaz DRMPolicy<br /> {<br /> atributo de sólo lectura DomString authDomain;<br /> atributo de solo lectura DRMAuthauthenticationMethod authMethod;<br /> atributo de solo lectura DomString dispName;<br /> atributo de solo lectura DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMManager {#drmmanager}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaz DRMManager : EventTarget {<br /> void acquisitionLicense(metadatos DRMMetadata, <br /> configuración DRMAcquireLicenseSettings, <br /> detector DRMAquireLicenseListener);<br /> void acquisitionPreviewLicense(metadatos DRMMetadata, <br /> DRMAquireLicenseListener);<br /> void authentication(metadatos DRMMetadata, <br /> URL DomString,<br /> DomString y authenticationDomain, <br /> usuario DomString, <br /> contraseña DomString, <br /> detector DRMAuthenticateListener);<br /> <br /> DRMM1 adata createMetadataFromBytes(<br /> matriz Uint8Array, detector DRMErrorListener);<br /> void initialize(DRMOperationCompleteListener listener listener);<br /> atributo long maxOperationTime;<br /> <br /> void joinLicenseDomain(&lt;a DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, <br /> DRMOperationCompleteListener listener);<br /> void allowLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> DRMOperation Listener completo);<br /> <br /> void resetDRM(DRMOperationCompleteListener listener listener);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID, <br /> DomString policyID, &lt;a22 9/&gt; commit booleano (inmediatamente,<br /> DRMReturnLicenseListener listener);<br /> void setAuthenticationToken(<br /> metadatos DRMMetadata, <br /> dominio de autenticación DomString, <br /> Uint8Array, <br /> DRMOperationCompleteListener (listener);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> DRMOperationCompleteListener listener);<br /> };<br /><br /></p> </td> 
   <td><p>interfaz DRMManager : EventTarget {<br /> void acquisitionLicense(metadatos DRMMetadata, <br /> configuración DRMAcquireLicenseSettings, <br /> EventContext eventContext);<br /> void acquisitionPreview(metadatos DRMMetadata, <br /> EventContext eventContext);<br /> void authentication(DRMMetadata) metadatos, <br /> DomString url,<br /> DomString &amp;authenticationDomain, <br /> usuario de DomString, <br /> contraseña de DomString, <br /> EventContext eventContext);<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> 3/&gt; matriz Uint8Array, EventContext eventContext);<br /> void initialize(EventContext eventContext);<br /> atributo long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> booleano forceRefresh, <br /> EventContext eventContext);<br /> void LeaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> EventContext eventContext);<br /> <br /> void resetDRM(EventContext (Context);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID,<br /> DomString policyID, <br /> booleano commitInmediatamente,<br /> EventContext eventContext);<br /> void set1/&gt; AuthenticationToken(<br /> metadatos DRMMetadata, <br /> DomString authenticationDomain, <br /> Token Uint8Array, <br /> EventContext eventContext);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> EventContext) eventContext);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>clase DRMErrorListener : <br /> psdkutils públicos::PSDKInterfaceWithUserData {<br /> público:<br /> vacío virtual en DRMError(uint32_t mayor, <br /> uint32_t menor, <br /> const psdkutils: PSDKString&amp; errorString, <br /> const psdkutils::PSDKString&amp; errorServerUrl) = 0;<br /> <br /> protegido:<br /> virtual DRMErrorListener() {}<br /> }</p> </td> 
   <td>Evento / Interfaz / Descripción 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>Cuando se produce un error durante uno de los métodos asincrónicos de DRMManger.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>clase DRMOperationCompleteListener : <br /> público DRMErrorListener {<br /> público:<br /> vacío virtual en DRMOperationComplete() = 0;<br /> <br /> protegido:<br /> virtual ~DRMOperationCompleteListener() {}<br /> };</p> </td> 
   <td>Evento / Interfaz / Descripción 
    <ul> 
     <li>kEventDRMInitializationComplete<p>/ PSDKEvent</p> <p>Cuando se complete la inicialización de DRM.</p> </li> 
     <li>kEventDRMJoinLicenseDomainComplete<p>/ PSDKEvent</p> <p>Cuando la acción joinLicenseDomain() se completa correctamente.</p> </li> 
     <li>kEventDRMLeaveLicenseDomainComplete<p>/ PSDKEvent</p> <p>Cuando la acción allowLicenseDomain() se completa correctamente.</p> </li> 
     <li>kEventDRMResetCompletePSDKEvent<p>/ PSDKEvent</p> <p>Cuando la acción resetDRM() se completa correctamente.</p> </li> 
     <li>kEventDRMAuthauthenticationTokenSet<p>/ PSDKEvent</p> <p>Cuando la acción setAuthenticationTokenSet() se completa correctamente.</p> </li> 
     <li>kEventDRMLicenseStored<p>/ PSDKEvent</p> <p>Cuando la acción storeLicenseBytes() se completa correctamente.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>clase DRMAuthenticateListener : <br /> público DRMErrorListener {<br /> público:<br /> vacío virtual onAuthenticationComplete(<br /> psdkutils::PSDKImmutableByteArray* <br /> authenticationToken) = 0;<br /> <br /> protegido:<br /> ~DRMAuthenticateate virtual Listener() {}<br /> }</p> </td> 
   <td>Evento / Interfaz / Descripción 
    <ul> 
     <li>kEventDRMAuthauthenticationComplete<p>/ DRMAuthauthenticationCompleteEvent</p> <p>Cuando la llamada al método DRMManager::authentication se realiza correctamente.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>clase DRMAquireLicenseListener: <br /> público DRMErrorListener {<br /> público:<br /> vacío virtual onLicenseAcquired(const DRMLicense*) = 0;<br /> <br /> protegido:<br /> virtual ~DRMAquireLicenseListener() {}<br /> };</p> </td> 
   <td>Evento / Interfaz / Descripción 
    <ul> 
     <li>kEventDRMPreviewLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>Cuando la llamada al método DRMManager::acquisitionPreviewLicense se realiza correctamente.</p> </li> 
     <li>kEventDRMLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>Cuando la llamada al método DRMManager::acquisitionLicense se realiza correctamente.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>clase DRMReturnLicenseListener: <br /> público DRMErrorListener {<br /> público:<br /> vacío virtual onLicenseReturnComplete(uint32_t numReturned ) = 0;<br /> <br /> protegido:<br /> virtual ~DRMReturnLicenseListener() {}<br /> };</p> </td> 
   <td>Evento / Interfaz / Descripción 
    <ul> 
     <li>kEventDRMLicenseReturnComplete<p>/ DRMLicenseReturnCompleteEvent</p> <p>Cuando la llamada al método DRMManager::returnLicense se realiza correctamente.</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Cambios en el elemento de API de reproducción genérica para 2.0 {#generic-playback-api-element-changes-for}

En estas tablas se comparan los elementos genéricos de la API de reproducción entre JavaScript TVSDK 1.3 y 2.0.

Tablas en este tema:

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
   <td><p>interfaz MediaResource {<br /> atributo DomString url; <br /> atributo tipo corto sin signo;<br /> atributo Metadatos de objeto;<br /> const short TYPE_HLS sin signo;<br /> const short TYPE_HDS sin signo;<br /> const short TYPE_DASH sin signo;<br /> const short TYPE_CUSTOM;<br /> const short TYPE_UNKNOWN sin signo;<br /> const; a8/&gt; };</p> </td> 
   <td><p>interfaz MediaResource {<br /> atributo DomString url;<br /> atributo DomString type;<br /> atributo Metadatos de objeto;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
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
   <td><p>interfaz MediaPlayer : EventTarget<br /> {<br /> void prepareToPlay( doble posición);<br /> void play();<br /> void pause();<br /> void seek( doble posición);<br /> void seekToLocal( doble posición);<br /> void reset();<br /> void release();<br /> replaceCurrentItem(elemento MediaPlayerItem);<br /> void replaceCurrentResource(recurso MediaResource, <br /> configuración de MediaPlayerItemConfig); <br /> void detl();<br /> void restore();<br /> void notifyClick();<br /> <br /> atributo de solo lectura TimeRange;<br /> atributo de solo lectura TimeRange buskableRange;<br /> atributo de solo lectura Time;<br /> atributo de sólo lectura doble localTime;<br /> atributo de solo lectura TimeRange bufferedRange;<br /> atributo de solo lectura DRMManager drmManager;<br /> atributo de solo lectura MediaPlayerItem currentItem;<br /> <br /> //&gt; //&gt; Status<br /> <br /> <br /> const unsigned short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;&lt;a22 9/&gt; const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEEKING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;&lt;a33 3/&gt; const short sin firmar PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /> <br /> atributo de sólo lectura estado corto sin signo;<br /> <br /> atributo de volumen corto sin signo;<br /> atributo ABB RControlParameters abrControlParameters;<br /> atributo BufferControlParameters bufferControlParameters;<br /> <br /> const unsigned short VISIBLE; //Para CC visibility<br /> const unsigned short INVISIBLE; //Para la visibilidad CC<br /> atributo ccVisibility corto sin signo;<br /> atributo TextFormat ccStyle;<br /> atributo de sólo lectura PlaybackMetrics playMetrics;<br /> <br /> doble tasa;<br /> atributo MediaPlayerView vista;&lt;a4View 50/&gt; atributo de sólo lectura Escala de tiempo;<br /> atributo doble currentTimeUpdateInterval; <br /> // configurar esto no será compatible con 2.0<br /> };<br /><br /><br /></p> </td> 
   <td><p>interfaz MediaPlayer : EventTarget<br /> {<br /> void prepareToPlay( posición int);<br /> void play();<br /> void pause();<br /> void seek( posición int));<br /> void seekToLocalTime( posición int);<br /> void reset();<br /> void release();<br /> void release();&gt; void replaceCurrentItem(MediaResource source);<br /> <br /> <br /> <br /> <br /> <br /> <br /> atributo de sólo lectura TimeRange;<br /> atributo de solo lectura TimeRange buskableRange;&lt;a11 17/&gt; atributo de sólo lectura doble currentTime;<br /> atributo de solo lectura doble localTime;<br /> atributo de solo lectura TimeRange bufferedRange;<br /> atributo de solo lectura DRMManager drmManager;<br /> atributo de solo lectura MediaPlayerItem currentItem;<br /> <br /> &lt;aManager&gt; 23/&gt; // PlayerState<br /> const unsigned short PLAYER_STATE_IDLE;<br /> const unsigned short PLAYER_STATE_INITIALIZING;<br /> const unsigned short PLAYER_STATE_INITIALIZED;<br /> const sin firmar el corto PLAYER_STATE_PREPARING;<br /> const unsigned short PLAYER_STATE_PREPARED;<br /> const unsigned short PLAYER_STATE_PLAYING;<br /> const unsigned short PLAYER_STATE_PAUSED;<br /> const short PLAYER sin firmar_STATE_SEEKING;<br /> const unsigned short PLAYER_STATE_COMPLETE;<br /> const unsigned short PLAYER_STATE_ERROR;<br /> const unsigned short PLAYER_STATE_RELEASED;<br /> const short PLAYER_STATUS_sin firmar SUSPENDED;<br /> atributo de sólo lectura estado corto sin signo;<br /> <br /> atributo de volumen corto sin signo;<br /> atributo ABRControlParameters abrControlParameters;<br /> atributo BufferControlParameters bufferControlParameters;<br /> <br /> 42/&gt; léxico-solamente-corto sin firmar VISIBLE; //Para la visibilidad CC<br /> readonly sin firmar abreviatura INVISIBLE; //Para la visibilidad CC<br /> atributo ccVisibility corto sin signo;<br /> atributo TextFormat ccStyle;<br /> atributo de sólo lectura PlaybackMetrics playMetrics;<br /> atributo MediaPlayerConfig mediaPlayerConfig;<br /> doble tasa de atributo;<br /> atributo vista MediaPlayerView;<br /> atributo de sólo lectura línea de tiempo;<br /> <br /> <br /> };<br /></p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaz MediaPlayerStatus<br /> {<br /> // PlayerStatus<br /> const unsigned short PLAYER_STATUS_IDLE;<br /> const unsigned short PLAYER_STATUS_INITIALIZING;<br /> const unsigned short PLAYER_STATUS_INITIALIZED;<br /> const corto sin signo PLAYER_STATUS_PREPARING;<br /> const sin firmar short PLAYER_STATUS_PREPARED;<br /> const sin firmar short PLAYER_STATUS_PLAYING;<br /> const sin firmar short PLAYER_STATUS_PAUSED;<br /> const sin firmar EKING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_STATUS_RELEASED;<br /> const unsigned short PLAYER_STATUS_SUSUS_SUSUS_SUSUS_SUSUS_SUSED PENDED;<br /> };</p> </td> 
   <td>(Nuevo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

#### Eventos admitidos por MediaPlayer {#events-supported-by-mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 Nombre del evento</th> 
   <th>Interfaz 2.0</th> 
   <th> </th> 
   <th>1.3 Nombre del evento</th> 
   <th>Interfaz 1.3</th> 
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
   <td><p>actualizado</p> <p>Cuando el reproductor de medios ha actualizado correctamente el contenido.</p> </td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>timedMetadataAvailable</td> 
   <td>TimedMetadataEvent</td> 
   <td> </td> 
   <td>MetadatosTemporizados</td> 
   <td>TimedMetadataEvent</td> 
  </tr> 
  <tr> 
   <td>línea de tiempoActualizado</td> 
   <td>Evento</td> 
   <td> </td> 
   <td>Escala de tiempo actualizada</td> 
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
   <td>size</td> 
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
   <td>buffer</td> 
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
   <td>DRMMetadataEvent</td> 
   <td> </td> 
   <td>drmMetadata</td> 
   <td>DRMMetadataEvent</td> 
  </tr> 
  <tr> 
   <td>reserveReached</td> 
   <td>ReserationEvent</td> 
   <td> </td> 
   <td>línea de tiempoHolderReached</td> 
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
   <td><p>Novedades de 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>profileChanged<br /> Cuando cambia el perfil de reproducción.</td> 
   <td>ProfileEvent</td> 
   <td> </td> 
   <td><p>Novedades de 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>seekPositionAjusted<br /> Cuando la posición de búsqueda se ajusta debido a reglas internas o externas.</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td><p>Novedades de 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>audioUpdated<br /> Cuando se actualiza un elemento del reproductor de contenidos. Para ciertas emisiones que contienen pistas de audio que solo se pueden detectar en el momento de la reproducción, este evento se activa cuando hay nuevas pistas de audio disponibles.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novedades de 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>captionsActualizado <br /> Cuando se actualiza un elemento del reproductor de contenidos. Para los flujos en directo/lineales, el cliente debe actualizar periódicamente el recurso de medios para detectar el nuevo contenido disponible. Cuando esto sucede, ciertas características de los medios pueden cambiar.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novedades de 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>masterUpdated <br /> Cuando se actualiza un elemento del reproductor de contenidos. Para los flujos en directo/lineales, el cliente debe actualizar periódicamente el recurso de medios para detectar el nuevo contenido disponible. Cuando esto sucede, ciertas características de los medios pueden cambiar.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novedades de 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>playRangeUpdated<br /> Cuando se actualiza un elemento del reproductor de contenidos. Para los flujos en directo/lineales, el cliente debe actualizar periódicamente el recurso de medios para detectar el nuevo contenido disponible. Cuando esto sucede, ciertas características de los medios pueden cambiar.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novedades de 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>timedEvent<br /> Se envía cuando se generan eventos temporizados.</td> 
   <td>TimedEvent</td> 
   <td> </td> 
   <td><p>Novedades de 2.0</p> </td> 
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
   <td><p>interfaz ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ;<br /> const unsigned short ABR_POLICY_MODERATE = 1 ;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> atributo unsigned firma abreviado abrPolicy;<br /> atributo sin firmar int initialBitRate;<br /> atributo sin firmar int minBitRate;<br /> atributo sin firmar int maxBitRate;<br /> const unsigned short DEFAULT_ABR_INITIAL_BITRATE;<br /> const short sin firmar DEFAULT_ABR_ABR MIN_BITRATE;<br /> const unsigned short DEFAULT_ABR_MAX_BITRATE;<br /> const ABRPolicy DEFAULT_ABR_POLICY;<br /> };</p> </td> 
   <td><p>interfaz ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ;<br /> const unsigned short ABR_POLICY_MODERATE = 1 ;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> atributo unsigned firma abreviado abrPolicy;<br /> atributo sin firmar int initialBitRate;<br /> atributo sin firmar int minBitRate;<br /> atributo sin firmar int maxBitRate;<br /> <br /> <br /> <br /> <br /> };</p> </td> 
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
   <td><p>interface BufferControlParameters<br /> {<br /> atributo initialBufferTime;<br /> atributo double playBufferTime;<br /> const double DEFAULT_INITIAL_BUFFER_TIME;<br /> const double DEFAULT_PLAY_BUFFER_TIME;<br /> };</p> </td> 
   <td><p>interface BufferControlParameters<br /> {<br /> atributo initialBufferTime;<br /> atributo doble playBufferTime;<br /> <br /> <br /> };</p> </td> 
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
   <td><p>interfaz TextFormat<br /> {<br /> // Color<br /> const unsigned short COLOR_DEFAULT = 0 ;<br /> const unsigned short COLOR_BLACK = 1 ;<br /> const unsigned short COLOR_GRAY = 2 ;<br /> const unsigned short COLOR_WHITE = 3 ;&lt;a 6/&gt; const unsigned short COLOR_BRIGHT_WHITE = 4 ;<br /> const unsigned short COLOR_DARK_RED = 5 ;<br /> const unsigned short COLOR_RED = 6 ;<br /> const unsigned short COLOR_BRIGHT_RED = 7 ;<br /> const unsigned short COLOR_DOR_DOR ARK_GREEN = 8 ;<br /> const unsigned short COLOR_GREEN = 9 ;<br /> const unsigned short COLOR_BRIGHT_GREEN = 10 ;<br /> const unsigned short COLOR_DARK_BLUE = 11 ;<br /> const sin firmar short COLOR_BLUE = 12 ;<br /> const unsigned short COLOR_BRIGHT_BLUE = 13 ;<br /> const unsigned short COLOR_DARK_YELLOW = 14 ;<br /> const unsigned short COLOR_YELLOW = 15 ;&lt;a1 8/&gt; const unsigned short COLOR_BRIGHT_YELLOW = 16 ;<br /> const unsigned short COLOR_DARK_MAGENTA = 17 ;<br /> const unsigned short COLOR_MAGENTA = 18 ;<br /> const unsigned short COLOR_BRIGHT_MAGENTA TA = 19 ;<br /> const unsigned short COLOR_DARK_CYAN = 20 ;<br /> const unsigned short COLOR_CYAN = 21 ;<br /> const unsigned short COLOR_BRIGHT_CYAN = 22 ;<br /> &lt;a2 6/&gt; atributo readonly sin firmar short fontColor;<br /> atributo readonly sin firmar short backgroundColor;<br /> atributo readonly sin firmar short fillColor;<br /> atributo readonly sin firmar short edgeColor;<br /> <br /> // Size<br /> const sin firmar SIZE_DEFAULT = 0 ;<br /> const unsigned short SIZE_SMALL = 1 ;<br /> const unsigned short SIZE_MEDIUM = 2 ;<br /> const unsigned short SIZE_LARGE = 3 ;<br /> <br /> readonly atributo unsigned short size;<br /> <br /> // FontEdge<br /> const unsigned short FONT_EDGE_DEFAULT = 0 ;<br /> const unsigned short FONT_EDGE_NONE = 1 ;<br /> const unsigned short FONT_EDGE_RAISED = 2 ;&lt;a 43/&gt; const unsigned short FONT_EDGE_DEPRESSED = 3 ;<br /> const unsigned short FONT_EDGE_UNIFORM = 4 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_LEFT = 5 ;<br /> const unsigned short_EDT_EDT GE_DROP_SHADOW_RIGHT = 6 ;<br /> atributo de sólo lectura unsigned short fontEdge;<br /> <br /> // Font<br /> const unsigned short FONT_DEFAULT = 0 ;<br /> const unsigned short FONT_MONOSPACED_WITH_SERIFS = 1 ;<br /> const unsigned short FONT_PROPORTIONAL_WITH_SERIFS = 2 ;<br /> const unsigned short FONT_MONSPACED_WITHOUT_SERIFS = 3 ;<br /> const unsigned short FONT_CASUAL = 4 ;<br /> const unsigned short_CURT_CURT SIVE = 5 ;<br /> const short sin signo FONT_SMALL_CAPITALS = 6 ;<br /> atributo de sólo lectura fuente corta sin signo;<br /> atributo de solo lectura sin signo fontOpacity;<br /> atributo de solo lectura sin signo short backgroundOpacity;<br /> atributo de solo lectura firmado fillOpacity;<br /> atributo readonly sin firmar short DEFAULT_OPACITY;<br /> };<br /><br /><br /><br /></p> </td> 
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
   <td><p>interfaz MediaPlayerItemLoader:<br /> {<br /> void load(MediaResource resource, long resourceId,<br /> ItemLoaderListener listener, <br /> MediaPlayerItemConfig config) ;<br /> void cancel();<br /> readonly attribute MediaPlayerItem currentItem;<br /> };</p> </td> 
   <td>Nuevo para 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interfaz ItemLoaderListener<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc;<br /> //onErrorCallbackFunc(PSDKErrorCode)<br /> var onErrorCallbackFunc;<br /> a5/&gt; }</p> </td> 
   <td>Nuevo para 2.0</td> 
  </tr> 
 </tbody> 
</table>

## Cambios en los elementos de la API de características de medios para 2.0 {#media-characteristics-api-element-changes-for}

En estas tablas se comparan los elementos API de características de medios para el SDK de TVSDK de C++ entre las versiones 1.3 y 2.0.

Tablas en este tema:

* MediaPlayerItem
* Track, AudioTrack, ClosedCaptionsTrack
* Perfil
* DRMMetadataInfo

### MediaPlayerItem {#mediaplayeritem}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaz MediaPlayerItem {<br /> atributo de solo lectura recurso MediaResource;<br /> atributo de solo lectura long resourceId;<br /> atributo de solo lectura booleano en vivo;<br /> <br /> atributo de solo lectura booleano hasAlternateAudio;<br /> atributo de solo lectura AudioTrackTracks;<br /> atributo de solo lectura AudioTrack seleccionadoAudio Track;<br /> void selectAudioTrack(AudioTrack track); <br /> <br /> atributo de solo lectura booleano hasClosedCaptions;<br /> atributo de solo lectura ClosedCaptionsTrackList closedCaptionsTracks;<br /> atributo de solo lectura ClosedCaptionsTrack selectedClosedCaptionsTrack;<br /> void selectClosedCaptionsTrack(<br />&gt; ClosedCaptionsTrack track); <br /> <br /> atributo de solo lectura booleano hasTimedMetadata;<br /> atributo de solo lectura TimedMetadataList timedMetadata;<br /> atributo de solo lectura dinámico;<br /> <br /> atributo de solo lectura booleano isProtegido;<br /> readonly atributo DRMMetadataInfoList drmMetadataInfos;<br /> atributo readonly perfiles de ProfileList;<br /> atributo de lectura Perfil seleccionado;<br /> <br /> atributo de sólo lectura booleano equinaPlaySupported;<br /> atributo de solo lectura FloatArray availablePlaybackRates ;<br /> atributo de sólo lectura float selectedPlaybackRate;<br /> <br /> <br /> atributo de solo lectura MediaPlayer mediaPlayer;<br /> atributo de solo lectura MediaPlayerItemConfig config;<br /> };</p> </td> 
   <td><p>interfaz MediaPlayerItem {<br /> atributo de solo lectura recurso de medios;<br /> atributo de solo lectura long resourceId;<br /> atributo de solo lectura booleano en vivo;<br /> <br /> atributo de solo lectura booleano hasAlternateAudio;<br /> atributo de solo lectura AudioTrackTracks;<br /> atributo AudioTrack seleccionadoAudioTrack; <br /> <br /> <br /> atributo de sólo lectura booleano hasClosedCaptions;<br /> atributo de solo lectura ClosedCaptionsTrackList ccTracks;<br /> atributo ClosedCaptionsTrack selectedCCTrack;<br /> <br /> <br /> <br /> 15/&gt; atributo de solo lectura booleano hasTimedMetadata;<br /> atributo de solo lectura TimedMetadataList timedMetadata;<br /> atributo de solo lectura dinámico;<br /> <br /> atributo de solo lectura booleano isProtection;<br /> atributo de solo lectura DRMMetadataInfoList drmMetadataInfos;<br /> atributo de solo lectura Perfiles de ProfileList;<br /> <br /> <br /> atributo de solo lectura booleano "PlaySupported";<br /> atributo de solo lectura Int32Array availablePlaybackRates;<br /> <br />&gt; atributo de sólo lectura StringList adTags;<br /> <br /> atributo de solo lectura MediaPlayer mediaPlayer;<br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Track / AudioTrack / ClosedCaptionsTrack {#track-audiotrack-closedcaptionstrack}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface Track<br /> {<br /> atributo de solo lectura DomString name;<br /> atributo de solo lectura DomString language;<br /> atributo de solo lectura predeterminado booleano;<br /> atributo de solo lectura autoSelect booleano;<br /> }; </p> </td> 
   <td>Nuevo para 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interfaz AudioTrack : Track<br /> {<br /> atributo de solo lectura DomString name; //FromTrack<br /> atributo de solo lectura lenguaje lenguaje DomString idioma;//FromTrack<br /> atributo de solo lectura predeterminado: // Desde Track<br /> atributo de solo lectura booleano autoSelect;//FromTrack<br /> <br /> atributo de solo lectura sin firmar int pid;<br /> };</p> </td> 
   <td><p>interface AudioTrack<br /> {<br /> atributo de solo lectura DomString name;<br /> atributo de solo lectura DomString language; <br /> atributo de solo lectura predeterminado booleano;<br /> atributo de solo lectura autoseleccionar booleano;<br /> atributo de solo lectura obligatorio booleano;<br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0</td> 
   <td><p>interfaz AudioTrackList<br /> {<br /> atributo readonly sin signo de longitud larga;<br /> getter AudioTrack (índice largo sin signo);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaz ClosedCaptionsTrack : Track<br /> {<br /> atributo de solo lectura DomString name; //FromTrack<br /> atributo de solo lectura lenguaje lenguaje DomString idioma;//FromTrack<br /> atributo de solo lectura predeterminado: // FromTrack<br /> atributo de sólo lectura booleano autoSelect;//FromTrack<br /> <br /> <br /> const unsigned short SERVICE_608_CAPTIONS = 0;<br /> const unsigned short SERVICE_708_CAPTIONS = 1;<br /> const short SERVICE_WEB sin firmar _VTT_CAPTIONS = 2;<br /> atributo de sólo lectura serviceType corto sin firmar;<br /> atributo de solo lectura obligatorio;<br /> };</p> </td> 
   <td><p>interfaz ClosedCaptionsTrack<br /> {<br /> atributo de sólo lectura DomString name;<br /> atributo de solo lectura DomString language;<br /> atributo de solo lectura predeterminado booleano;<br /> <br /> <br /> atributo de solo lectura booleano activo;<br /> <br /> <br /> <br /> <br /> 11/&gt; <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0</td> 
   <td><p>interfaz ClosedCaptionsTrackList<br /> {<br /> atributo de sólo lectura sin signo de longitud;<br /> getter ClosedCaptionsTrack(índice largo sin signo);<br /> };</p> </td> 
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
   <td>Perfil: Sin cambios para 2.0</td> 
   <td><p>perfil de interfaz<br /> {<br /> atributo de sólo lectura sin firmar ancho de int;<br /> atributo de solo lectura sin firmar en altura;<br /> atributo de solo lectura sin firmar int bitRate;<br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td>ProfileList: Sin cambios para 2.0</td> 
   <td><p>interfaz ProfileList<br /> {<br /> atributo de sólo lectura sin signo de longitud larga;<br /> getter Profile(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMMetadataInfo {#drmmetadatainfo}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfo</strong>: Sin cambios para 2.0</td> 
   <td><p>interfaz DRMMetadataInfo<br /> { <br /> atributo de sólo lectura metadatos DRMMetadata;<br /> atributo de solo lectura prefetchTimestamp;<br /> atributo de solo lectura TimeRange timeRange;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>: Sin cambios para 2.0</td> 
   <td><p>interfaz DRMMetadataInfoList<br /> {<br /> atributo de sólo lectura sin signo de longitud;<br /> getter DRMMetadataInfo(índice largo sin signo);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## Asignación de errores de C++ a excepciones en diferentes idiomas {#mapping-c-errors-to-exceptions-in-different-languages}

Puede asignar códigos de error C++ a excepciones en distintos idiomas.

El PSDK de C++ tiene una directiva &quot;no pull&quot; para sus API. La mayoría de los métodos API devuelven un valor PSDKErrorCode para indicar si el método se ejecutó correctamente. Los errores asincrónicos se notifican mediante los eventos de error.

El ActionScript y el SDK de JAVA tienen una política diferente. La mayoría de los errores generarán ArgumentError o IllegalStateException para indicar que no se pudo ejecutar la parte sincrónica del método. Estas excepciones no se detectan y el código de la aplicación es responsable de gestionar las excepciones. Normalmente llevan información útil sobre por qué ha fallado la llamada al método. Por ejemplo, si se llama al comando prepareToPlay en un estado no válido, se produce la siguiente excepción:

```shell
throw new IllegalStateException("Invalid player state. prepareToPlay method 
must be called only once after replaceCurrentItem or replaceCurrentResource method.");
```

El ActionScript/JAVA también arroja excepciones de los constructores para indicar que algún objeto interno se creó incorrectamente. Estas excepciones se gestionan internamente y no se propagan a la aplicación. Las excepciones se incluyen en una notificación de advertencia que se envía a la aplicación

Por ejemplo, si no se encontró ningún archivo multimedia válido para la respuesta de publicidad recibida, no se puede crear ningún objeto o anuncio de recurso de publicidad válido. Como resultado, no se coloca ningún anuncio en la cronología y se envía una notificación NotificationEvent.OperationFailed .

Los códigos de error o advertencia que se reciben asincrónicamente del motor de vídeo de Adobe (AVE) se envían a la aplicación como eventos normales. El evento de notificación contiene todos los códigos de error recibidos y cualquier metadato adicional, como la URL, el identificador de recursos, el identificador, el identificador, etc. Si el error es grave y la reproducción del contenido multimedia actual no puede continuar, MediaPlayer pasa al estado ERROR y se envía la llamada de retorno onStatusChanged o el evento MediaPlayerStatusChanged.STATUS_CHANGED. Si la reproducción puede continuar, se envía un evento de notificación normal.

<table> 
 <tbody> 
  <tr> 
   <th>Error C++ (código PSDKError)</th> 
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
   <td>Excepción con el código = 1, descripción = "INVALID_ARGUMENT" y additionalInfo= &lt;as pass by method que provocó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNullPointer</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ArgumentError</td> 
   <td>Excepción con el código = 2, descripción = "GENERIC_ERROR" y additionalInfo= &lt;as pass by method que provocó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECIllegalState</td> 
   <td> </td> 
   <td>IllegalStateException</td> 
   <td>IllegalStateException</td> 
   <td>Excepción con el código = 3, descripción = "ILLEGAL_STATE" y additionalInfo= &lt;as pass by method que lanzó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInterfaceNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con el código = 4, descripción = "GENERIC_ERROR" y additionalInfo= &lt;as pass by method que lanzó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCreationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con el código = 5, descripción = "CREATION_FAILED" y additionalInfo= &lt;as pass by method que provocó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedOperation</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con el código = 5, descripción = "CREATION_FAILED" y additionalInfo= &lt;as pass by method que provocó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECDataNotAvailable</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con el código = 7, descripción = "DATA_NOT_AVAILABLE" y additionalInfo= &lt;as pass by method que lanzó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECSeekError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con el código = 8, descripción = "SEEK_ERROR" y additionalInfo= &lt;as pass by method que lanzó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedFeature</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con el código = 9, descripción = "UNSUPPORTED_FEATURE" y additionalInfo= &lt;as pass by method que lanzó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECRangeError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 10, descripción = "RANGE_ERROR" y additionalInfo= &lt;as pass by method que lanzó esta excepción</td> 
  </tr> 
  <tr> 
   <td>kECCodecNotSupported</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con el código = 11, descripción = "CODEC_NOT_SUPPORTED" y additionalInfo= &lt;as pass by method que provocó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECMediaError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 12, descripción = "MEDIA_ERROR" y additionalInfo= &lt;as pass by method que provocó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNetworkError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 13, descripción = "NETWORK_ERROR" y additionalInfo= &lt;as pass by method que lanzó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECGenericError</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Error o MediaPlayerNotification.Warning</td> 
   <td>MediaError o NotificationEvent</td> 
   <td>Excepción con código = 14, descripción = "GENERIC_ERROR" y additionalInfo= &lt;as pass by method que lanzó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInvalidSeekTime</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 15, descripción = "INVALID_SEEK_TIME" y additionalInfo= &lt;según el método que lanzó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAudioTrackError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 16, descripción = "AUDIO_TRACK_ERROR" y additionalInfo= &lt;según el método que lanzó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAccessFromDifferent<p>ThreadError</p> </td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 17, descripción = "GENERIC_ERROR" y additionalInfo= &lt;as pass by method que provocó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECElementNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 18, descripción = "GENERIC_ERROR" y additionalInfo= &lt;as pass by method que lanzó esta excepción</td> 
  </tr> 
  <tr> 
   <td>kECNotImplementado</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 19, descripción = "GENERIC_ERROR" y additionalInfo= &lt;as pass by method que provocó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECPlaybackOperationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 200, descripción = "PLAYBACK_OPERATION_FAILED" y additionalInfo= &lt;como se transfiere por el método que lanzó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNativeWarning</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>NotificationEvent</td> 
   <td>Excepción con código = 201, descripción = "NATIVE_WARNING" y additionalInfo= &lt;as pass by method que lanzó esta excepción</td> 
  </tr> 
  <tr> 
   <td>kECAdResolverFailed</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>-</td> 
   <td>Excepción con código = 202, descripción = "AD_RESOLVER_FAILED" y additionalInfo= &lt;como pasó por el método que lanzó esta excepción&gt;</td> 
  </tr> 
 </tbody> 
</table>

## Cambios en los elementos de la API de utilidad y ayuda para 2.0 {#utility-and-helper-api-element-changes-for}

Estas tablas comparan los elementos de la API de utilidades y de ayuda para el SDK de JavaScript entre las versiones 1.3 y 2.0.

Tablas en este tema:

* Versión
* TimeRange
* QOSProvider
* DeviceInformation
* LoadInfo
* Ver
* Información de reproducción

### Versión {#version}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaz Versión<br /> {<br /> atributo de sólo lectura versión DomString;<br /> atributo de solo lectura descripción DomString;<br /> atributo de solo lectura mayor;<br /> atributo de solo lectura menor largo;<br /> atributo de solo lectura revisión larga;<br /> atributo de solo lectura apiVersion larga;<br /> };</p> </td> 
   <td><p>interfaz Versión<br /> {<br /> atributo de sólo lectura versión DomString;<br /> atributo de solo lectura descripción DomString;<br /> atributo de solo lectura DomString mayor;<br /> atributo de solo lectura DomString menor;<br /> atributo de solo lectura revisión DomString;<br /> atributo de solo lectura DomString apiVersion;<br /> };</p> </td> 
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
   <td><p>interfaz TimeRange<br /> {<br /> atributo de sólo lectura inicio largo sin signo;<br /> atributo de solo lectura sin signo de fin largo;<br /> atributo de solo lectura sin firmar de duración larga;<br /> };</p> </td> 
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
   <td><p>interfaz QOSProvider<br /> {<br /> void attachMediaPlayer(MediaPlayer player player);<br /> void detachMediaPlayer();<br /> <br /> atributo de lectura DeviceInformation deviceInformation;<br /> atributo de lectura PlaybackInformation playInformation playInformation;<br /> };</p> </td> 
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
   <td><p>interfaz DeviceInformation<br /> {<br /> atributo de sólo lectura DomString os;<br /> <br /> <br /> <br /> atributo de solo lectura DomString id;<br /> atributo de solo lectura int denyDPI;<br /> atributo de solo lectura int heightPixels;<br /> atributo de solo lectura int width9 Pixels;&lt;a/&gt; atributo de sólo lectura booleano seekToKeyFrame;<br /> };<br /></p> </td> 
   <td><p>interfaz DeviceInformation<br /> {<br /> atributo de solo lectura DomString os;<br /> atributo de solo lectura int sdk;<br /> modelo DomString de atributo de solo lectura;<br /> fabricante de solo lectura DomString;<br /> atributo de solo lectura DomString id;<br /> atributo de solo lectura intDPI;<br /> readonly atributo int heightPixels;<br /> atributo de sólo lectura int widthPixels;<br /> <br /> };</p> </td> 
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
   <td><p>interfaz LoadInfo<br /> {<br /> atributo de sólo lectura DomString url;<br /> tamaño de int de atributo de solo lectura;<br /> atributo de solo lectura doble downloadDuration;<br /> atributo de solo lectura int periodIndex;<br /> atributo de solo lectura doble mediaDuration;<br /> atributo de solo lectura corto TRACK_TYPE_FRAGMENT;<br /> readonly atributo corto TRACK_TYPE_TRACK;<br /> atributo de sólo lectura abreviado TRACK_TYPE_MANIFEST;<br /> tipo corto de atributo de solo lectura;<br /> atributo de solo lectura DomString trackName;<br /> atributo de solo lectura DomString trackType;<br /> atributo de solo lectura trackIndex;<br /> atributo &gt; };</p> </td> 
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
   <td><p>vista de interfaz<br /> {<br /> atributo readonly sin signo x;<br /> atributo readonly sin signo y corto;<br /> atributo readonly sin signo de ancho corto;<br /> atributo readonly sin signo de altura corta;<br /> <br /> void setSize(unsigned short width, unsigned short height);<br /> void setPos(unsigned short) x, y corta sin signo);<br /> }</p> </td> 
  </tr> 
 </tbody> 
</table>

### Información de reproducción {#playbackinformation}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface PlaybackInformation<br /> {<br /> atributo de sólo lectura doble timeToFirstByte;<br /> atributo de solo lectura doble timeToLoad;<br /> atributo de solo lectura doble timeToStart;<br /> atributo de solo lectura doble timeToFail;<br /> atributo de solo lectura int totalSecondsPlayed;<br /> atributo de solo lectura int totalSecondsSpent;<br /> atributo de sólo lectura doble frameRate;<br /> atributo de solo lectura int droppedFrameCount;<br /> atributo de solo lectura int viewBandwidth;<br /> atributo de solo lectura int bitrate;<br /> atributo de solo lectura bufferTime;<br /> atributo de solo lectura int bufferLength;&lt;aLength; a13/&gt; atributo de sólo lectura en emptyBufferCount;<br /> atributo de solo lectura bufferingTime;<br /> };<br /></p> </td> 
   <td><p>interface PlaybackInformation<br /> {<br /> atributo de sólo lectura doble timeToFirstByte;<br /> atributo de solo lectura doble timeToLoad;<br /> atributo de solo lectura doble timeToStart;<br /> atributo de solo lectura doble timeToFail;<br /> atributo de solo lectura int totalSecondsPlayed;<br /> atributo de solo lectura int totalSecondsSpent;<br /> atributo de sólo lectura doble frameRate;<br /> atributo de solo lectura int droppedFrameCount;<br /> <br /> atributo de solo lectura en la velocidad de bits;<br /> atributo de solo lectura bufferTime;<br /> atributo de solo lectura int bufferLength;<br /> atributo de solo lectura int emptyBufferCount;<br /> atributo de sólo lectura: bufferingTime;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en la página [Aprendizaje y asistencia de Adobe Primetime](https://helpx.adobe.com/support/primetime.html).
