---
title: Conversión de TVSDK - 1.3 a 2.0 para JavaScript
seo-title: Conversión de TVSDK - 1.3 a 2.0 para JavaScript
description: Muchas firmas de métodos y nombres de elementos de API han cambiado para 2.0. Revise estas tablas para ver todos los detalles de los cambios de API.
seo-description: Muchas firmas de métodos y nombres de elementos de API han cambiado para 2.0. Revise estas tablas para ver todos los detalles de los cambios de API.
uuid: d2d1742d-c90c-43f5-94fc-8c4a57cb8ed4
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: migration
discoiquuid: c732f54d-116c-43f3-bec4-5e71af208426
translation-type: tm+mt
source-git-commit: cfd6da49e85e13e29e8458ee98231a8b476867db
workflow-type: tm+mt
source-wordcount: '5058'
ht-degree: 0%

---


# Conversión de TVSDK - 1.3 a 2.0 para JavaScript {#tvsdk-conversion-to-for-javascript}

Muchas firmas de métodos y nombres de elementos de API han cambiado para 2.0. Revise estas tablas para ver todos los detalles de los cambios de API.

## Implementar funciones de llamada de retorno en JavaScript {#implement-callback-functions-in-javascript}

Los comentarios en la documentación del método sugieren la firma de las rellamadas que debe implementar.

Para JavaScript, la sintaxis de la API se basa en el ID web. Para una interfaz TVSDK, los nombres de método se denominan *methodName*(). Para los métodos que su aplicación debe implementar, se agrega a la interfaz un atributo de lectura y escritura llamado *methodName* CallbackFunc y la aplicación debe configurarlo para que señale a una función que implemente el método. Por ejemplo:

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

## Cambios en los elementos de la API de flujo de trabajo de publicidad para 2.0 {#advertising-workflow-api-element-changes-for}

Estas tablas comparan los elementos de API de flujo de trabajo de publicidad para el SDK de TVSDK de JavaScript entre las versiones 1.3 y 2.0.

Tablas en este tema:

* Metadatos temporizados
* AdSignalingMode
* AdvertisingMetadata
* CustomRangeMetadata
* ReplaceTimeRange
* Ubicación
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
   <td><p> <strong>Metadatos</strong> temporizados: interface TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0 ;  <br /> const unsigned short METADATA_TYPE_ID3 = 1 ;  <br /> atributo readonly tipo abreviado sin firmar;  <br /> atributo de sólo lectura durante mucho tiempo;<br /> atributo de sólo lectura DomString id;<br />  <br /> atributo de sólo lectura DomString name;atributo de sólo lectura contenido DomString;  <br /> metadatos de objeto de atributo de solo lectura;<br /> }; </p> </td> 
   <td><p>interface TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0 ;<br /> const unsigned short METADATA_TYPE_ID3 = 1 ;<br /> atributo de sólo lectura unsigned short metadataType;<br /> atributo de sólo lectura durante mucho tiempo;<br /> atributo de sólo lectura long id;<br /> readonly attribute DomString name; a6/&gt; <br /> atributo de sólo lectura Metadatos de objeto;<br /> };<br /></p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetadataList</strong>: (Sin cambios para 2.0)</td> 
   <td><p>interface TimedMetadataList {<br /> atributo de solo lectura longitud sin firmar;<br /> getter TimedMetadata(índice largo sin firmar);<br /> };</p> </td> 
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
   <td><p>Interface AdSignalingMode { <br /> const unsigned short MODE_DEFAULT, <br /> const unsigned short MODE_MANIFEST_CUES , <br /> const unsigned short MODE_SERVER_MAP , <br /> const unsigned short MODE_CUSTOM_RANGES <br /> };</p> </td> 
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
   <td><p>Interface AdvertisingMetadata { <br /> atributo AdSignalingMode; <br /> atributo AdBreakWatchedPolicy adBreakAsWatched; <br /> atributo boolean livePreroll; <br /> atributo booleano delayAdLoading ; <br /> };</p> </td> 
   <td>Esta funcionalidad la proporcionó el<p>MetadataKeys::ADVERTISING_METADATA</p> key.</td> 
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
   <td><p>La interfaz CustomRangeMetadata { <br /> const unsigned short TYPE_MARK_RANGE; <br /> const unsigned short TYPE_DELETE_RANGE; <br /> const unsigned short TYPE_REPLACE_RANGE; <br /> atributo tipo corto sin firmar; <br /> atributo boolean ajustaSeekPosition; <br /> atributo TimeRangeList timeRangeList; <br /> };</p> </td> 
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
   <td><p>interface ReplaceTimeRange { <br /> atributo unsigned long begin; <br /> atributo de sólo lectura de extremo largo sin firmar; <br /> atributo duración larga sin firmar; <br /> atributo replaceDuration largo sin firmar; <br /> };</p> </td> 
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
   <td><p>Ubicación de interfaz { <br /> const unsigned short TYPE_MID_ROLL; <br /> const unsigned short TYPE_PRE_ROLL; <br /> const unsigned short TYPE_POST_ROLL; <br /> const unsigned short TYPE_SERVER_MAP; <br /> const short TYPE_CUSTOM_RANGE sin firmar;<br /> atributo de sólo lectura tipo abreviado sin firmar; <br /> atributo de sólo lectura durante mucho tiempo; <br /> atributo de sólo lectura de larga duración; <br /> const unsigned short MODE_DEFAULT; <br /> const unsigned short MODE_INSERT; <br /> const unsigned short MODE_REPLACE; <br /> const unsigned short MODE_DELETE; <br /> const unsigned short MODE_MARK; <br /> const unsigned short MODE_FREE_REPLACE; <br /> atributo de sólo lectura modo corto sin signo; <br /> intervalo TimeRange de atributos de sólo lectura; <br /> };</p> </td> 
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
   <td><p>interface Opportunity { <br /> atributo de sólo lectura DomString id; <br /> ubicación del atributo de sólo lectura; <br /> readonly attribute Configuración de objetos; <br /> atributo de sólo lectura Object customParameters; <br /> }; </p> </td> 
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
   <td><p>interface Reservation { <br /> atributo de sólo lectura intervalo de tiempo; <br /> atributo de sólo lectura en espera larga; <br /> }; </p> </td> 
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
   <td><p><strong>Cronología</strong>: interfaz Línea de tiempo  <br /> { atributo readonly TimelineMarkerList timelineMarkers;  <br /> atributo de sólo lectura TimelineItemList timelineItems;  <br /> doble convertToLocalTime( tiempo de doble);  <br /> doble convertToVirtualTime( tiempo de doble);  <br /> };</p> </td> 
   <td><p>interfaz Timeline {<br /> atributo de sólo lectura TimelineMarkerList timelineMarkers;<br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>TimelineItem</strong>: interface TimelineItem:<br /> TimelineMarker {<br /> readonly attribute long id;  <br /> atributo de sólo lectura TimeRange virtualRange;  <br /> atributo de sólo lectura TimeRange localRange;  <br /> atributo de sólo lectura booleano visto;  <br /> atributo de sólo lectura booleano temporal;  <br /> }; </p> </td> 
   <td>(Nuevo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><strong>Marcador</strong> de línea de tiempo: (Sin cambios para 2.0)</td> 
   <td><p>interface TimelineMarker {<br /> tiempo de doble de atributos de sólo lectura;<br /> duración de doble de atributos de solo lectura;<br /> };</p> </td> 
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
   <td><p>interfaz AdBreak {<br /> <br /> <br /> <br /> duración del doble de atributos de sólo lectura;<br /> anuncios de AdList de atributos de sólo lectura;<br /> <br /> <br /> atributo de sólo lectura AdInsertionType insertType;<br /> }; </p> </td> 
   <td><p>interfaz AdBreak {<br /> tiempo de doble de atributos de sólo lectura;<br /> doble de atributos de sólo lectura;<br /> <br /> duración de doble de atributos de sólo lectura;<br /> atributo de sólo lectura AdList adList;<br /> <br /> datos de DomString de sólo lectura;<br /> <br /> }; </p> </td> 
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
   <td><p> <strong>Publicidad</strong>: anuncio de interfaz {<br /> readonly attribute AdAsset primarioAsset;<br /> readonly attribute AdAssetList CompanionAssets;<br /> <br /> readonly attribute doble duration;atributo <br /> readonly id DomString id;<br /> const unsigned short ADTYPE_LINEAR = 0 ;<br /> const unsigned short ADTYPE_NONLINEAR = 1 ;atributo <br /> <br /> readonly atributo unsigned short adType;<br /> readonly atributo AdInsertionType adInsertionType;  <br /> <br /> se puede hacer clic en booleano de atributo de solo lectura;  <br /> atributo de sólo lectura booleano isCustomAdMarker;<br /> }; </p> </td> 
   <td><p>anuncio de interfaz {<br /> atributo de sólo lectura AdAsset primarioAsset;<br /> atributo de solo lectura AdAssetList CompanionAssets;<br /> <br /> duración de doble de atributo de sólo lectura;<br /> atributo de solo lectura DomString id;<br /> const unsigned short ADTYPE_LINEAR = 0 ;<br /> const corto sin firmar ADTYPE_Ntam ONLINEAR = 1 ;<br /> <br /> atributo de sólo lectura tipo corto sin signo;<br /> atributo de solo lectura AdInsertionType insertType; <br /> rastreador de objetos de atributo de sólo lectura;<br /> <br /> <br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>: (Sin cambios para 2.0)</td> 
   <td><p>interfaz AdAsset {<br /> atributo de solo lectura DomString id;<br /> duración del doble de atributos de solo lectura;<br /> atributo de solo lectura MediaResource;<br /> atributo de solo lectura AdClick adClick;<br /> metadatos de objeto de atributo de solo lectura;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>: (Sin cambios para 2.0)</td> 
   <td><p>interfaz AdClick {<br /> atributo de sólo lectura DomString id;<br /> atributo de sólo lectura DomString title;<br /> atributo de sólo lectura DomString url;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdList</strong>: (Sin cambios para 2.0)</td> 
   <td><p>interface AdList {<br /> atributo de sólo lectura longitud sin signo;<br /> getter Ad(índice largo sin signo);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>: (Sin cambios para 2.0)</td> 
   <td><p>interfaz AdAssetList {<br /> atributo de solo lectura longitud sin signo;<br /> captador AdAsset(índice largo sin signo);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>: interfaz AdBannerAsset : AdAsset<br /> {<br /> readonly attribute int width;<br /> readonly attribute int height;<br /> readonly attribute DomString staticUrl;<br /> readonly attribute DomString height;<br /> readonly attribute DomString width;<br /> };</p> </td> 
   <td> Nuevo en 2.0</td> 
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
   <td><p> <strong>AdBreakTimelineItem</strong>: interfaz AdBreakTimelineItem: TimelineItem {  <br /> readonly attribute AdBreak adBreak;  <br /> elementos AdTimelineItemList de atributo de solo lectura;  <br /> }; </p> </td> 
   <td> (Nuevo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimelineItem</strong>: interfaz AdTimelineItem : TimelineItem {  <br /> readonly attribute AdBreak adBreak;  <br /> anuncio de atributo de solo lectura;  <br /> }; </p> </td> 
   <td> (Nuevo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>: interface AdBreakTimelineItemList { atributo de solo  <br /> lectura longitud sin firmar;  <br /> get AdBreakTimelineItem (índice de eventos sin firmar);  <br /> };</p> </td> 
   <td> (Nuevo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakPolicy / AdBreakWatchedPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector {#adbreakpolicy-adbreakwatchedpolicy-adpolicy-adpolicymode-adpolicyinfo-adpolicyselector}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>atributo de sólo lectura de la interfaz AdBreakPolicy {<br /> atributo de sólo lectura abreviado AD_BREAK_POLICY_SKIP;<br /> atributo de sólo lectura abreviado AD_BREAK_POLICY_PLAY;<br /> atributo de sólo lectura abreviado AD_BREAK_POLICY_REMOVE_AFTER_PLAY;<br /> };<br /></p> </td> 
   <td><p> atributo de sólo lectura de interfaz AdPolicyConstances {<br /> atributo de sólo lectura abreviado AD_BREAK_POLICY_SKIP;<br /> atributo de sólo lectura abreviado AD_BREAK_POLICY_PLAY;<br /> atributo de sólo lectura abreviado AD_BREAK_POLICY_REMOVE;<br /> atributo de sólo lectura VE_AFTER_PLAY;}<br />...</p> </td> 
  </tr> 
  <tr> 
   <td><p> interfaz AdBreakWatchedPolicy {<br /> atributo de sólo lectura abreviado AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> atributo de sólo lectura abreviado AD_BREAK_AS_WATCHED_ON_END;<br /> atributo de sólo lectura abreviado AD_BREAK_AS_WATCHED_NEVER;<br /> }; </p> </td> 
   <td><p> ...<br /> atributo de sólo lectura corto AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> atributo de sólo lectura corto AD_BREAK_AS_WATCHED_ON_END;<br /> atributo de sólo lectura corto AD_BREAK_AS_WATCHED_NEVER;<br />...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaz AdPolicy {<br /> atributo de sólo lectura short AD_POLICY_PLAY;<br /> atributo de sólo lectura short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> atributo de sólo lectura abreviado AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN; atributo readonly short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> <br /> atributo de sólo lectura short AD_POLICY_SKIP_AD_BREAK;<br /> };</p> </td> 
   <td><p> ... <br /> atributo de sólo lectura short AD_POLICY_PLAY;<br /> atributo de sólo lectura short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> atributo de sólo lectura short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;<br /> atributo de sólo lectura abreviado AD_POLICY_SKIP_TO_NEXT_NEXT_AD_AD_NEXT_AD_NEXT_AD_NEXT_AD_AD_AD_NEXT_AD_AD_AD_NEXT_AD_NEXT_AD_AD_AD_NEXT_AD_AD_AD_AD_NEXT_AD_AD_NEXT_AD_AD_NEXT_AD_AD_NEXT_AD_AD_AD_AD_NEXT_AD_AD_NEXT_AD_AD_NEXT_AD_AD_AD_NEXT_AD_AD_NEXT_NEXT_AD_BEGIN IN_BREAK;<br /> atributo de sólo lectura corto AD_POLICY_SKIP_AD_BREAK;<br />...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaz AdPolicyMode {<br /> atributo de sólo lectura abreviado AD_POLICY_MODE_PLAY;<br /> atributo de sólo lectura abreviado AD_POLICY_MODE_SEEK;<br /> atributo de sólo lectura abreviado AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
   <td><p> ...<br /> {readonly attribute short AD_POLICY_MODE_PLAY;<br /> readonly attribute short AD_POLICY_MODE_SEEK;<br /> readonly attribute short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaz AdPolicyInfo {<br /> atributo de sólo lectura AdBreakTimelineItemList <br /> adBreakTimelineItems;<br /> atributo de solo lectura AdTimelineItem adTimelineItem;<br /> atributo de solo lectura currentTime;<br /> atributo de sólo lectura searchToTime;<br /> doble de solo lectura rate;<br /> modo abreviado de atributo de sólo lectura; //AdPolicyMode<br /> };</p> </td> 
   <td><p>interfaz AdPolicyInfo {<br /> atributo de sólo lectura AdBreakPlacementList <br /> adBreakPlacements;<br /> anuncio de atributo de solo lectura;<br /> atributo de solo lectura currentTime;<br /> atributo de sólo lectura searchToTime;<br /> velocidad de doble de atributo de solo lectura;<br /> atributo de sólo lectura short ; //AdPolicyMode<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaz AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo SelectPolicyForAdBreakCallbackFunc;<br /> /*<br /> * AdAdBreak TimelineItemList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo SelectAdBreaksToPlayCallbackFunc;<br /> /**<br /> * AdPolicy selectPolicyForSeekType toAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectPolicyForSeekIntoAdCallbackFunc; <br /> /**<br /> * AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectWatchedPolicyForAdBreakCallbackFunc;<br /> };</p> </td> 
   <td><p>interfaz AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo SelectPolicyForAdBreakFuncCallback;<br /> /*<br /> * AdAdBreak SelectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo SeleccionarAdBreaksToPlayCallback;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdAdAdAdIntoPolicy AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectPolicyForSeekIntoAdCallback; <br /> /**<br /> * AdBreakAsWatched selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo SelectWatchedPolicyForAdBreakCallback;&lt;a 19/&gt; };<br /></p> </td> 
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
   <td><p>interfaz TimelineOperation { <br /> readonly atributo Colocación ; <br /> };</p> </td> 
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
   <td><p>interfaz AdBreakPlacement: TimelineOperation {<br /> atributo de sólo lectura AdBreak adBreak;<br /> ubicación del atributo de solo lectura; // Desde TimelineOperation<br /> tiempo de doble de atributos de sólo lectura;<br /> duración de doble de atributos de solo lectura;<br /> };</p> </td> 
   <td><p>interfaz AdBreakPlacement {<br /> atributo de solo lectura AdBreak adBreak;<br /> ubicación de asignación de atributos de solo lectura;<br /> tiempo de doble de atributos de solo lectura;<br /> duración de doble de atributos de solo lectura;<br /> };</p> </td> 
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
   <td><p>interfaz AuditudeSettings: AdvertisingMetadata { <br /> atributo DomString zoneId; <br /> atributo DomString mediaId; <br /> atributo DomString defaultMediaId ; <br /> atributo dominio DomString ; <br /> atributo Object targetInfo ; <br /> atributo Object customParameters ; <br /> atributo Boolean creativePackaingEnabled ;<br /> atributo Boolean showStaticBanners ;<br /> };</p> </td> 
   <td>La funcionalidad la proporcionó la clave MetadataKeys::AUDITUDE_METADATA_KEY.</td> 
  </tr> 
 </tbody> 
</table>

## Cambios en los elementos de la API de personalización para 2.0 {#customization-api-element-changes-for}

Estas tablas comparan los elementos de la API de personalización para el TVSDK de JavaScript entre las versiones 1.3 y 2.0.

Tablas en este tema:

* MediaPlayerItemConfig
* ContentFactory
* NetworkConfiguration

### MediaPlayerItemConfig {#mediaplayeritemconfig}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaz MediaPlayerItemConfig {<br /> atributo ContentFactory adFactory;<br /> atributo StringList subscriptionTags;<br /> <br /> atributo StringList adTags;<br /> <br /> atributo AdSignalingMode adSignalingMode;<br /> atributo CustomRangeMetadatacustomRangeRange ;<br /> atributo NetworkConfiguration networkConfiguration;<br /> atributo AdvertisingMetadata publicidadMetadata;<br /> atributo Boolean useHardwareDecoder;<br /> };<br /></p> </td> 
   <td><p>interfaz MediaPlayerConfig {<br /> <br /> <br /> <br /> atributo StringList adTags;<br /> atributo StringList subscribedTags;<br /> atributo MediaPlayerClientFactory clientFactory;<br /> <br /> <br /> <br /> <br /> &lt;a10/&gt; 1/&gt; };<br /></p> </td> 
  </tr> 
 </tbody> 
</table>

### ContentFactory {#contentfactory}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaz ContentFactory {<br /> /*<br /> * AdPolicySelector recuperarAdPolicySelector(<br /> * elemento MediaPlayerItem);<br /> */<br /> atributo Recuperación de objeto AdPolicySelectorCallbackFunc;<br /> };</p> </td> 
   <td><p>interfaz MediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector recuperarAdPolicySelector(<br /> * elemento MediaPlayerItem);<br /> */<br /> atributo Recuperación de objeto AdPolicySelectorFunc;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### NetworkConfiguration {#networkconfiguration}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface NetworkConfiguration<br /> {<br /> atributo booleano forceNativeNetworking;<br /> atributo boolean useRedirectUrl;<br /> atributo Object cookieHeader;<br /> atributo boolean readSetCookieHeader;<br /> atributo int masterUpdateInterval; <br /> atributo booleano useCookieHeaderForAllRequests;<br /> atributo int readLimit;<br /> };</p> </td> 
   <td>En 1.3, MetadataKeys proporcionó parte de esta funcionalidad</td> 
  </tr> 
 </tbody> 
</table>

## Cambios en el elemento de API de DRM para 2.0 {#drm-api-element-changes-for}

Estas tablas comparan los elementos de la API de DRM para el TVSDK de JavaScript entre las versiones 1.3 y 2.0.

Tablas en este tema:

* Inicialización del flujo de trabajo de DRM
* DRMAcquireLicenseSettings / DRMAuthauthenticationMethod
* DRMMetadata
* DRMPlaybackTimeWindow
* DRMLicense
* DRMLicenseDomain
* DRMPolicy
* DRMManager

### Inicialización del flujo de trabajo de DRM {#drm-workflow-initialization}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>La aplicación debe llamar a AdobePSDK.initiateDRMWorkflow para iniciar el flujo de trabajo de DRM. Sin esta llamada, los vídeos DRM no se reproducirán.<p>interfaz AdobePSDK<br /> {<br /> void initiateDRMWorkFlow(<br /> DomString appStoratePath, <br /> DomString publisherId, <br /> DomString appId, <br /> DomString appVersion, <br /> privacyModeOn booleano);<br /> };</p> </td> 
   <td>La inicialización se realizó internamente y no se requería ninguna llamada explícita.</td> 
  </tr> 
 </tbody> 
</table>

### DRMAcquireLicenseSettings/DRMAuthauthenticationMethod {#drmacquirelicensesettings-drmauthenticationmethod}

| API 2.0 | 1.3 API |
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
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0.</td> 
   <td><p>interfaz DRMMetadata<br /> {<br /> atributo de sólo lectura DomString serverUrl;<br /> atributo de sólo lectura DomString licenseId;<br /> atributo de sólo lectura DRMPolicyArray políticas; <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPlaybackTimeWindow {#drmplaybacktimewindow}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface DRMPlaybackTimeWindow {<br /> atributo de sólo lectura int playbackPeriodInSeconds;<br /> atributo de sólo lectura long playbackStartDate;<br /> atributo de sólo lectura long playbackEndDate;<br /> };</p> </td> 
   <td><p>interface DRMPlaybackTimeWindow {<br /> atributo de sólo lectura int periodInSeconds;<br /> atributo de solo lectura int startDate;<br /> atributo de solo lectura int endDate;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMLicense {#drmlicense}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0.</td> 
   <td><p>interfaz DRMLicense {<br /> atributo de sólo lectura Uint8Bytes de matriz;<br /> atributo de sólo lectura Date licenseStartDate;<br /> atributo de sólo lectura Date licenseEndDate;<br /> atributo de sólo lectura Date offlineStorageStartDate;<br /> atributo de sólo lectura Date offlineStorageEndDate; <br /> atributo de sólo lectura DomString serverUrl;<br /> atributo de sólo lectura DomString licenseID;<br /> atributo de sólo lectura DomString policyID;<br /> atributo de sólo lectura DRMPlaybackTimeWindow playTimeWindow;<br /> atributo de sólo lectura Object customProperties;<br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMLicenseDomain {#drmlicensedomain}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaz DRMLicenseDomain {<br /> atributo de sólo lectura DomString authenticationDomain;<br /> atributo de sólo lectura DRMAuthauthenticationMethod authenticationMethod; <br /> atributo de sólo lectura DomString serverUrl;<br /> };</p> </td> 
   <td><p>interface DRMLicenseDomain {<br /> atributo de sólo lectura DomString authDomain;<br /> atributo de solo lectura DRMAuthauthenticationMethod authMethod; <br /> atributo de sólo lectura DomString serverURL;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPolicy {#drmpolicy}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaz DRMPolicy<br /> {<br /> atributo de sólo lectura DomString authenticationDomain;<br /> atributo de sólo lectura DRMAuthauthenticationMethod authenticationMethod;<br /> atributo de sólo lectura DomString displayName;<br /> atributo de sólo lectura DRMLicenseDomain licenseDomain;<br /> };<br /></p> </td> 
   <td><p>interfaz DRMPolicy<br /> {<br /> atributo de sólo lectura DomString authDomain;<br /> atributo de sólo lectura DRMAuthauthenticationMethod authMethod;<br /> atributo de sólo lectura DomString dispName;<br /> atributo de sólo lectura DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMManager {#drmmanager}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaz DRMManager: EventTarget {<br /> void acquisitionLicense(metadatos DRMMetadata, <br /> configuración de DRMAcquireLicenseSettings, <br /> detector de DRMAquireLicenseListener);<br /> void acquisitionPreviewLicense(metadatos de DRMMetadata, <br /> detector de DRMAquireLicenseListener);<br /> void authentication(metadatos DRMMetadata, <br /> URL de DomString,<br /> DomString y authenticationDomain, <br /> usuario de DomString, <br /> contraseña de DomString, <br /> DRMAuthenticateListener);<br /> <br /> DRMMetlistener adata createMetadataFromBytes(<br /> matriz Uint8Array, detector de DRMErrorListener);<br /> void initialize(detector de DRMOperationCompleteListener);<br /> atributo long maxOperationTime;<br /> <br /> void joinLicenseDomain(&lt;a 18/&gt; DominioDeLicenciaDeDRMLicense, <br /> valor booleano forceRefresh, <br /> detector DRMOperationCompleteListener);<br /> valor nulo de LeaveLicenseDomain(<br /> dominioDeLicenciaDeDRMLLicenciaDomain, &lt;a223/&gt; DRMO3/&gt; controlador000000000000000000000000000000000000000000000000000000000000000000listener CompleteListener);<br /> <br /> void resetDRM(detector DRMOperationCompleteListener);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID, <br /> DomString policyID, &lt;a2222 9/&gt; commit booleano inmediatamente,<br /> detector DRMReturnLicenseListener);<br /> void setAuthenticationToken(<br /> metadatos DRMMetadata, <br /> dominio de autenticación DomString, <br /> token Uint8Array, <br /> detector DRMOperationCompleteListener);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> detector DRMOperationCompleteListener);<br /> };<br /><br /><br /></p> </td> 
   <td><p>interfaz DRMManager: EventTarget {<br /> void acquisitionLicense(metadatos DRMMetadata, <br /> configuración de DRMAcquireLicenseSettings, <br /> EventContext eventContext);<br /> void acquisitionPreviewLicense(metadatos de DRMMetadata, <br /> EventContext eventContext);<br /> void authentication(DRMMadata metadata, <br /> URL de DomString,<br /> DomString y authenticationDomain, <br /> usuario de DomString, <br /> contraseña de DomString, <br /> EventContext eventContext);<br /> <br /> DRMMetadata createMetadataFromBytes(&lt;a1Context) 3/&gt; matriz Uint8Array, EventContext eventContext);<br /> void initialize(EventContext eventContext);<br /> atributo long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> booleano forceRefresh, <br /> EventContext eventContext);<br /> void leftLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> EventContext eventContext);<br /> <br /> void resetDRM(EventContext Contexto);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID,<br /> DomString policyID, <br /> commitInmediatamente booleano,<br /> EventContext eventContext);<br /> void set1/&gt; AuthenticationToken(<br /> metadatos DRMMetadata, <br /> dominio de autenticación DomString, <br /> token Uint8Array, <br /> eventContext de EventContext);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> EventContext eventContext);<br /> };<br /></p> </td> 
  </tr> 
  <tr> 
   <td><p>clase DRMErrorListener: <br /> psdkutils públicos::PSDKInterfaceWithUserData {<br /> public:<br /> virtual void onDRMError(uint32_t major, <br /> uint32_t minor, <br /> const psdkutils: PSDKString&amp; errorString, <br /> const psdkutils::PSDKString&amp; errorServerUrl) = 0;<br /> <br /> protegido:<br /> virtual ~DRMErrorListener() {}<br /> }</p> </td> 
   <td>Evento/interfaz/descripción 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>Cuando se produce un error durante uno de los métodos asincrónicos de DRMManger.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>clase DRMOperationCompleteListener: <br /> public DRMErrorListener {<br /> public:<br /> virtual void onDRMOperationComplete() = 0;<br /> <br /> protected:<br /> virtual ~DRMOperationCompleteListener() {}<br /> };</p> </td> 
   <td>Evento/interfaz/descripción 
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
   <td><p>clase DRMAuthenticateListener: <br /> public DRMErrorListener {<br /> public:<br /> virtual void onAuthenticationComplete(<br /> psdkutils::PSDKImmutableByteArray* <br /> authenticationToken) = 0;<br /> <br /> protegido:<br /> virtual ~DRMAuthenticateateid Listener() {}<br /> }</p> </td> 
   <td>Evento/interfaz/descripción 
    <ul> 
     <li>kEventDRMAuthauthenticationComplete<p>/ DRMAuthauthenticationCompleteEvent</p> <p>Cuando la llamada al método DRMManager::authentication se realiza correctamente.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>clase DRMAquireLicenseListener: <br /> public DRMErrorListener {<br /> public:<br /> virtual void onLicenseAcquired(const DRMLicense*) = 0;<br /> <br /> protected:<br /> virtual ~DRMAquireLicenseListener() {}<br /> };</p> </td> 
   <td>Evento/interfaz/descripción 
    <ul> 
     <li>kEventDRMPreviewLicenseAdquired<p>/ DRMLicenseAcquiredEvent</p> <p>Cuando la llamada al método DRMManager::acquisitionPreviewLicense se realiza correctamente.</p> </li> 
     <li>kEventDRMLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>Cuando la llamada al método DRMManager::acquisitionLicense se realiza correctamente.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>clase DRMReturnLicenseListener: <br /> public DRMErrorListener {<br /> public:<br /> virtual void onLicenseReturnComplete(uint32_t numReturn ) = 0;<br /> <br /> protected:<br /> virtual ~DRMReturnLicenseListener() {}<br /> };</p> </td> 
   <td>Evento/interfaz/descripción 
    <ul> 
     <li>kEventDRMLicenseReturnComplete<p>/ DRMLicenseReturnCompleteEvent</p> <p>Cuando la llamada al método DRMManager::returnLicense se realiza correctamente.</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Cambios genéricos en el elemento de la API de reproducción para 2.0 {#generic-playback-api-element-changes-for}

Estas tablas comparan los elementos genéricos de la API de reproducción entre el TVSDK de JavaScript 1.3 y 2.0.

Tablas en este tema:

* MediaResource
* MediaPlayer
* ABRControlParameters
* Parámetros de BufferControl
* TextFormat
* MediaPlayerItemLoader

### MediaResource {#mediaresource}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaResource {<br /> atributo DomString url; <br /> atributo tipo corto sin firmar;<br /> atributo Metadatos de objeto;<br /> const short TYPE_HLS sin firmar;<br /> const short TYPE_HDS sin firmar;<br /> const unsigned short TYPE_DASH;<br /> const unsigned short TYPE_CUSTOM;<br /> const unsigned short TYPE_UNKUNKNOWN sin firmar; a8/&gt; };<br /></p> </td> 
   <td><p>interfaz MediaResource {<br /> atributo Dirección URL de DomString;<br /> atributo Tipo de cadena Dom;<br /> atributo Metadatos de objeto;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### MediaPlayer {#mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaz MediaPlayer: EventTarget<br /> {<br /> void prepareToPlay( posición de doble);<br /> void play();<br /> void pause();<br /> void search( posición de doble);<br /> void searchToLocal( posición de doble);<br /> void reset();<br /> void release();&lt;a7/&gt; void release();&lt;a);&lt;a);&lt;a5/&gt; void;/&gt; void replaceCurrentItem(elemento MediaPlayerItem);<br /> void replaceCurrentResource(recursoMedia, <br /> configuración de MediaPlayerItemConfig); <br /> void stopús();<br /> void restore();<br /> void notificationClick();<br /> <br /> atributo de sólo lectura TimeRange playbackRange;<br /><br /> atributo de sólo lectura TimeRange buscableRange;<br /> atributo de sólo lectura currentTime;<br /> atributo de sólo lectura doble localTime;<br /> atributo de sólo lectura TimeRange bufferedRange;<br /> atributo de sólo lectura DRMManager drmManager;<br /> atributo de sólo lectura MediaPlayerItem actualItem;<br /> <br /> // PlayerStatus<br /> <br /> <br /> const unsigned short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;&lt;a12/ const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEEKING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;&lt;a16/ const unsigned short PLAYER_STATUS_ERROR;<br /> <br /><br /> const short sin firmar PLAYER_STATUS_RELEASED;<br /> <br /> atributo de sólo lectura estado corto sin firmar;<br /> <br /> atributo short volumen sin firmar;<br /> atributo ABRControlParameters abrControlParameters;<br /> atributo BufferControlParameters bufferControlParameters;<br /> <br />&gt; const unsigned short VISIBLE; //Para la visibilidad de CC<br /> const unsigned short INVISIBLE; //Para la visibilidad de CC<br /> atributo ccVisibility corto sin firmar;<br /> atributo TextFormat ccStyle;<br /> atributo de sólo lectura PlaybackMetrics playMetrics;<br /> <br /> tasa de doble de atributos;<br /> atributo MediaPlayerView vista;&lt;a111111 5/&gt; escala de tiempo de línea de tiempo de atributos de solo lectura;<br /> doble de atributos currentTimeUpdateInterval; <br /> // establecer esto no será compatible con 2.0<br /> };<br /></p> </td> 
   <td><p>interfaz MediaPlayer: EventTarget<br /> {<br /> void prepareToPlay( posición int);<br /> void play();<br /> void pause();<br /> void search( posición int);<br /> void searchToLocalTime( posición int);<br /> void reset();<br /> void release();<br /> void release();&lt;a8/&gt;);&gt; void replaceCurrentItem(origen de MediaResource);<br /> <br /> <br /> <br /> <br /> <br /> <br /> atributo de sólo lectura TimeRange;<br /> atributo de sólo lectura TimeRange de búsqueda;&lt;a1111114/&gt; 17/&gt; doble de atributos de solo lectura currentTime;<br /> doble de atributos de solo lectura localTime;<br /> atributo de solo lectura TimeRange bufferedRange;<br /> <br /> atributo de sólo lectura DRMManager drmManager;<br /> atributo de sólo lectura MediaPlayerItem currentItem;<br /> <br /> // PlayerState<br /> const unsigned short PLAYER_STATE_IDLE;<br /> const unsigned short PLAYER_STATE_INITIALIZING;<br /> const unshort PLAYER YER_STATE_INITIALIZED;<br /> const unsigned short PLAYER_STATE_PREPARING;<br /> const unsigned short PLAYER_STATE_PREPARED;<br /> const unsigned short PLAYER_STATE_STATE_PAUSED;<br /> const unsigned short PLAYER_STATE_PAUSED;&lt;a8;&lt;a&gt; 10/&gt; const unsigned short PLAYER_STATE_SEEKING;<br /> const unsigned short PLAYER_STATE_COMPLETE;<br /> const unsigned short PLAYER_STATE_ERROR;<br /> const unsigned short PLAYER_STATE_RELEASED;<br /> const short PLAYER_STATUS_SUSPENDED sin firmar;<br /> atributo de sólo lectura estado corto sin firmar;<br /> <br /> atributo short volumen sin firmar;<br /> <br /> atributo ABRControlParameters abrControlParameters;<br /> atributo BufferControlParameters bufferControlParameters;<br /> <br /> readonly unsigned short VISIBLE; //Para la visibilidad de CC<br /> léonly unsigned short INVISIBLE; //Para la visibilidad de CC<br /> atributo ccVisibility corto sin firmar;<br /> atributo TextFormat ccStyle;<br /> atributo de sólo lectura PlaybackMetrics playbackMetrics;<br /> atributo MediaPlayerConfig mediaPlayerConfig;<br /> tasa de doble de atributos;<br /> atributo MediaPlayerView vista;<br />&gt; escala de tiempo del atributo readonly;<br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerStatus<br /> {<br /> // PlayerStatus<br /> const unsigned short PLAYER_STATUS_IDLE;<br /> const unsigned short PLAYER_STATUS_INITIALIZING;<br /> const unsigned short PLAYER_STATUS_INITIALIZED;<br /> const sin firmar, PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SETUS EKING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_SUSTUS_RELEASED;<br /> const unsigned short PLAYER_STATUS_SUSTUS_SUSUS_SUSTUS_SUSED PENDED;<br /> };</p> </td> 
   <td>(Nuevo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

#### Eventos admitidos por MediaPlayer {#events-supported-by-mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 Nombre del Evento</th> 
   <th>Interfaz 2.0</th> 
   <th> </th> 
   <th>1.3 Nombre del Evento</th> 
   <th>1.3 Interfaz</th> 
  </tr> 
  <tr> 
   <td><p>(eliminado para 2.0)</p> </td> 
   <td> </td> 
   <td> </td> 
   <td>preparado</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td><p>itemUpdated</p> <p>Cuando se actualiza un elemento de reproductor de medios.</p> </td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>actualizado</p> <p>Cuando el reproductor de medios ha actualizado correctamente el medio.</p> </td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>timedMetadataAvailable</td> 
   <td>TimedMetadataEvent</td> 
   <td> </td> 
   <td>MetadatosTmed</td> 
   <td>TimedMetadataEvent</td> 
  </tr> 
  <tr> 
   <td>línea de tiempoActualizada</td> 
   <td>Evento</td> 
   <td> </td> 
   <td>TtmelineUpdated</td> 
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
   <td>searchBegin</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td>searchStart</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>searchEnd</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td>searchComplete</td> 
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
   <td>adClick<br /> Cuando el usuario hace clic en una publicidad.</td> 
   <td>AdClicksEvent</td> 
   <td> </td> 
   <td><p>Nuevo en 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>profileChanged<br /> Cuando cambia el perfil de reproducción.</td> 
   <td>ProfileEvent</td> 
   <td> </td> 
   <td><p>Nuevo en 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>searchPositionAdjusted<br /> Cuando la posición de búsqueda se ajusta debido a reglas internas o externas.</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td><p>Nuevo en 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>audioUpdated<br /> Cuando se actualiza un elemento de reproductor de medios. Para determinados flujos que contienen pistas de audio que solo se pueden detectar durante la reproducción, este evento se activa cuando hay nuevas pistas de audio disponibles.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Nuevo en 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>captionsUpdated <br /> Cuando se actualiza un elemento de reproductor de medios. En el caso de los flujos en vivo/lineales, el cliente debe actualizar periódicamente el recurso de medios para detectar el nuevo contenido disponible. Cuando esto sucede, ciertas características de los medios pueden cambiar.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Nuevo en 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>masterUpdated <br /> Cuando se actualiza un elemento de reproductor de medios. En el caso de los flujos en vivo/lineales, el cliente debe actualizar periódicamente el recurso de medios para detectar el nuevo contenido disponible. Cuando esto sucede, ciertas características de los medios pueden cambiar.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Nuevo en 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>playRangeUpdated<br /> Cuando se actualiza un elemento de reproductor de medios. En el caso de los flujos en vivo/lineales, el cliente debe actualizar periódicamente el recurso de medios para detectar el nuevo contenido disponible. Cuando esto sucede, ciertas características de los medios pueden cambiar.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Nuevo en 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>timedEvent<br /> Se envía cuando se generan eventos temporizados.</td> 
   <td>TimedEvent</td> 
   <td> </td> 
   <td><p>Nuevo en 2.0</p> </td> 
  </tr> 
 </tbody> 
</table>

### Parámetros de ABRControl {#abrcontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ;<br /> const unsigned short ABR_POLICY_MODERATE = 1 ;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> atributo unsigned signed short abrPolicy;<br /> atributo unsigned int initialBitRate;<br /> atributo unsigned int minBitRate;<br /> atributo unsigned int maxBitRate;<br /> const unsigned short DEFAULT_ABR_INITIAL_BITRATE;<br /> const unsigned short DEFAULT_ABR MIN_BITRATE;<br /> const unsigned short DEFAULT_ABR_MAX_BITRATE;<br /> const ABRPolicy DEFAULT_ABR_POLICY;<br /> };</p> </td> 
   <td><p>interface ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ;<br /> const unsigned short ABR_POLICY_MODERATE = 1 ;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> atributo unsigned signed short abrPolicy;<br /> atributo unsigned int initialBitRate;<br /> atributo unsigned int minBitRate;<br /> atributo unsigned int maxBitRate;<br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### BufferControlParameters {#buffercontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface BufferControlParameters<br /> {<br /> doble de atributos initialBufferTime;<br /> atributo playBufferTime;<br /> doble de const DEFAULT_INITIAL_BUFFER_TIME;<br /> doble de const DEFAULT_PLAY_BUFFER_TIME;<br /> };</p> </td> 
   <td><p>interface BufferControlParameters<br /> {<br /> doble de atributos initialBufferTime;<br /> atributo playBufferTime;<br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TextFormat {#textformat}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0</td> 
   <td><p>interface TextFormat<br /> {<br /> // Color<br /> const unsigned short COLOR_DEFAULT = 0 ;<br /> const unsigned short COLOR_BLACK = 1 ;<br /> const unsigned short COLOR_GRAY = 2 ;<br /> const unsigned short COLOR_WHITE = 3 ;&lt;a 6/&gt; const unsigned short COLOR_BRIGHT_WHITE = 4 ;<br /> const unsigned short COLOR_DARK_RED = 5 ;<br /> const unsigned short COLOR_RED = 6 ;<br /> const unsigned short COLOR_BRIGHT_RED = 7 ;<br /> const unsigned short COLOR_DOR_DOR ARK_GREEN = 8 ;<br /> const unsigned short COLOR_GREEN = 9 ;<br /> const unsigned short COLOR_BRIGHT_GREEN = 10 ;<br /> const unsigned short COLOR_DARK_BLUE = 11 ;<br /> const unsigned short COLOR_BLUE = 12 ;<br /> const unsigned short COLOR_BRIGHT_BLUE = 13 ;<br /> const unsigned short COLOR_DARK_YELLOW = 14 ;<br /> const unsigned short COLOR_YELLOW = 15 ;&lt;a11 8/&gt; const unsigned short COLOR_BRIGHT_YELLOW = 16 ;<br /><br /><br /> const unsigned short COLOR_DARK_MAGENTA = 17 ;<br /> const unsigned short COLOR_MAGENTA = 18 ;<br /> const unsigned short COLOR_BRIGHT_MAGENTA = 19 ;<br /> const unsigned short COLOR_DARK_CYAN = 20 ;<br /> const st short COLOR_CYAN = 21 ;<br /> const unsigned short COLOR_BRIGHT_CYAN = 22 ;<br /> <br /> atributo de sólo lectura unsigned short fontColor;<br /> atributo de sólo lectura unsigned short fillColor;<br /> atributo de sólo lectura unsigned short fillColor;<br /> atributo de sólo lectura edgeColor corto firmado;<br /> <br /> // Tamaño<br /> const unsigned short SIZE_DEFAULT = 0 ;<br /> const unsigned short SIZE_SMALL = 1 ;<br /> const unsigned short SIZE_MEDIUM = 2 ;<br /> const short SIZE_LARGE = 3 ;<br /> <br /> atributo de sólo lectura sin signo de tamaño corto;<br /> <br /> // FontEdge<br /> const unsigned short FONT_EDGE_DEFAULT = 0 ;<br /> const unsigned short FONT_EDGE_NONE = 1 ;<br /> const signed short FONT_EDGE_RAISED = 2 ;<br /> const unsigned short FONT_EDGE_DEPRESSED = 3 ;<br /> const unsigned short FONT_EDGE_UNIFORM = 4 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_LEFT = 5 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_RIGHT = 6 ;<br /> atributo de sólo lectura unsigned short fontEdge;<br /> <br /> // Font<br /> const unsigned short FONT_DEFAULT = 0 ;<br /> const unsigned short T_MONOSLT PACED_WITH_SERIFS = 1 ;<br /> const unsigned short FONT_PROPORTIONAL_WITH_SERIFS = 2 ;<br /> const unsigned short FONT_MONSPACED_WITHOUT_SERIFS = 3 ;<br /> const unsigned short FONT_CASUAL = 4 ;<br /> const unsigned short FONT_CURSIVE = 5 ;<br /> const short FONT_SMALL_CAPITALS = 6 ;<br /> atributo readonly font unsigned short;<br /> atributo readonly fontOpacity;<br /> atributo readonly sin firmar short backgroundOpacity;<br /> atributo readonly short fill sin signoOpacity;<br /> atributo de sólo lectura sin firmar short DEFAULT_OPACITY;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### MediaPlayerItemLoader {#mediaplayeritemloader}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaz MediaPlayerItemLoader:<br /> {<br /> void load(recurso de MediaResource, identificador de recurso largo,<br /> detector de ItemLoaderListener, <br /> configuración de MediaPlayerItemConfig);<br /> void cancel();<br /> atributo de sólo lectura MediaPlayerItem actualItem;<br /> };;;;;</p> </td> 
   <td>Nuevo para 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interface ItemLoaderListener<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc;<br /> //onErrorCallbackFunc(PSDKErrorCode)<br /> var onErrorCallbackFunc; a5/&gt; }<br /></p> </td> 
   <td>Nuevo para 2.0</td> 
  </tr> 
 </tbody> 
</table>

## Cambios en el elemento API de características de medios para 2.0 {#media-characteristics-api-element-changes-for}

Estas tablas comparan los elementos API de características de medios para el SDK de C++ entre las versiones 1.3 y 2.0.

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
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaz MediaPlayerItem {<br /> atributo de solo lectura MediaResource resource;<br /> atributo de solo lectura long resourceId;<br /> atributo de solo lectura live;<br /> <br /> atributo de solo lectura boolean hasAlternateAudio;<br /> atributo de solo lectura AudioTrackList AudioTracks;<br /> atributo de solo lectura AudioTrackAudioAudioAudioAudio Track;<br /> void selectAudioTrack(pista AudioTrack); <br /> <br /> atributo de sólo lectura booleano hasClosedCaptions;<br /> atributo de sólo lectura ClosedCaptionsTrackList ClosedCaptionsTracks;<br /> atributo de solo lectura ClosedCaptionsTrack selectedClosedCaptionsTrack;<br /> void selectClosedCaptionsTrack(<br />&gt; ClosedCaptionsTrack track); <br /> <br /> atributo de solo lectura booleano hasTimedMetadata;<br /> atributo de solo lectura TimedMetadataList timedMetadata;<br /> atributo de solo lectura dinámico;<br /> <br /> atributo de solo lectura booleano isProtected;<br /> atributo de solo lectura atributo DRMMetadataInfoList drmMetadataInfos;<br /> atributos de sólo lectura perfiles ProfileList;<br /> Perfil de atributos de solo lectura selectedProfile;<br /> <br /> atributo de sólo lectura booleanPlaySupported;<br /> atributo de solo lectura FloatArray availablePlaybackPlayback Tarifas;<br /> atributo de sólo lectura float selectedPlaybackRate;<br /> <br /> <br /> atributo de sólo lectura MediaPlayer mediaPlayer;<br /> atributo de sólo lectura MediaPlayerItemConfig config;<br /> };</p> </td> 
   <td><p>interfaz MediaPlayerItem {<br /> atributo de solo lectura recurso de medios;<br /> atributo de sólo lectura long resourceId;<br /> atributo de sólo lectura booleano;<br /> <br /> atributo de solo lectura boolean hasAlternateAudio;<br /> atributo de sólo lectura AudioTrackList AudioTracks;<br /> atributo AudioTrack selectedAudioAudioAudioTrack;<br /> <br /> <br /> atributo de sólo lectura booleano hasClosedCaptions;<br /> atributo de sólo lectura ClosedCaptionsTrackList ccTracks;<br /> atributo ClosedCaptionsTrack selectedCCTrack;<br /> <br /> <br /> &lt;a112/&gt; 15/&gt; atributo de sólo lectura booleano hasTimedMetadata;<br /> atributo de solo lectura TimedMetadataList timedMetadata;<br /> atributo de solo lectura booleano;<br /> <br /> atributo de solo lectura booleano isProtected;<br /> atributo de solo lectura DRMMetadataInfoList drmMetadataInfos;<br /> perfiles ProfileList de atributos de sólo lectura;<br /> <br /> <br /> atributo de sólo lectura boolean DORPlaySupported;<br /> atributo de sólo lectura Int32Array availablePlaybackRates;<br /> &lt;a7/&gt; atributo de sólo lectura StringList adTags;<br /> <br /> atributo de sólo lectura MediaPlayer mediaPlayer;<br /> <br /> };<br /><br /></p> </td> 
  </tr> 
 </tbody> 
</table>

### Track / AudioTrack / ClosedCaptionsTrack {#track-audiotrack-closedcaptionstrack}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface Track<br /> {<br /> atributo de sólo lectura nombre DomString;<br /> atributo de sólo lectura lenguaje DomString;<br /> atributo de sólo lectura predeterminado booleano;<br /> atributo de sólo lectura autoSelect booleano;<br /> }; </p> </td> 
   <td>Nuevo para 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interfaz AudioTrack: Track<br /> {<br /> nombre de DomString de solo lectura; //FromTrack<br /> atributo de sólo lectura lenguaje DomString;//FromTrack<br /> atributo de sólo lectura predeterminado booleano; // Desde Track<br /> atributo de sólo lectura autoSelect booleano;//FromTrack<br /> <br /> atributo de sólo lectura sin signo int pid;<br /> };</p> </td> 
   <td><p>interfaz AudioTrack<br /> {<br /> atributo de sólo lectura nombre DomString;<br /> atributo de sólo lectura lenguaje DomString; <br /> atributo de sólo lectura predeterminado booleano;<br /> atributo de sólo lectura autoSelect booleano;<br /> atributo de sólo lectura obligatorio booleano;<br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0</td> 
   <td><p>interface AudioTrackList<br /> {<br /> atributo de sólo lectura longitud sin signo;<br /> getter AudioTrack (índice largo sin firmar);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaz ClosedCaptionsTrack: Track<br /> {<br /> nombre de DomString de solo lectura; //FromTrack<br /> atributo de sólo lectura lenguaje DomString;//FromTrack<br /> atributo de sólo lectura predeterminado booleano; // FromTrack<br /> atributo de sólo lectura autoSelect booleano;//FromTrack<br /> <br /> <br /> const unsigned short SERVICE_608_CAPTIONS = 0;<br /> const unsigned short SERVICE_WEB_708_CAPTIONS = 1;<br /> const short SERVICE_WEB sin firmar_VTT_CAPTIONS = 2;<br /> atributo de sólo lectura serviceType corto sin firmar;<br /> atributo de solo lectura booleano forzado;<br /> };</p> </td> 
   <td><p>interfaz ClosedCaptionsTrack<br /> {<br /> atributo de sólo lectura nombre DomString;<br /> atributo de sólo lectura lenguaje DomString;<br /> atributo de sólo lectura predeterminado booleano;<br /> <br /> <br /> atributo de sólo lectura booleano activo;<br /> <br /> <br /> &lt;a 10/&gt; &lt;a&gt; 11/&gt; <br /> };<br /><br /></p> </td> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0</td> 
   <td><p>interface ClosedCaptionsTrackList<br /> {<br /> atributo de sólo lectura longitud sin firmar;<br /> getter ClosedCaptionsTrack(índice largo sin firmar);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Perfil {#profile}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>Perfil: Sin cambios para 2.0</td> 
   <td><p>interface Perfil<br /> {<br /> atributo de sólo lectura unsigned int width;<br /> atributo de solo lectura unsigned int height;<br /> atributo de solo lectura unsigned int bitRate;<br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td>ProfileList: Sin cambios para 2.0</td> 
   <td><p>interface ProfileList<br /> {<br /> atributo de sólo lectura longitud sin firmar;<br /> Perfil de captador (índice largo sin firmar);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMMetadataInfo {#drmmetadatainfo}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfo</strong>: Sin cambios para 2.0</td> 
   <td><p>interfaz DRMMetadataInfo<br /> { <br /> atributo de sólo lectura metadatos DRMMetadata;<br /> atributo de sólo lectura prefetchTimestamp;<br /> atributo de sólo lectura TimeRange timeRange;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>: Sin cambios para 2.0</td> 
   <td><p>interfaz DRMMetadataInfoList<br /> {<br /> atributo de sólo lectura longitud sin signo;<br /> getter DRMMetadataInfo(índice largo sin signo);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## Asignación de errores de C++ a excepciones en diferentes idiomas {#mapping-c-errors-to-exceptions-in-different-languages}

Puede asignar códigos de error de C++ a excepciones en distintos idiomas.

El PSDK de C++ tiene una política de &quot;no tirar&quot; para sus API. La mayoría de los métodos API devuelven un valor PSDKErrorCode para indicar si el método se ejecutó correctamente. Los errores asincrónicos se notifican mediante los eventos de error.

ActionScript y JAVA PSDK tienen una política diferente. La mayoría de los errores generarán un ArgumentError o IllegalStateException para indicar que no se pudo ejecutar la parte sincrónica del método. Estas excepciones no se detectan y el código de la aplicación es responsable de gestionar las excepciones. Generalmente contienen información útil de por qué falló la llamada al método. Por ejemplo, si se llama al comando prepareToPlay en un estado no válido, se genera la siguiente excepción:

```shell
throw new IllegalStateException("Invalid player state. prepareToPlay method 
must be called only once after replaceCurrentItem or replaceCurrentResource method.");
```

El ActionScript/JAVA también emite excepciones de los constructores para indicar que algún objeto interno se creó incorrectamente. Estas excepciones se gestionan internamente y no se propagan a la aplicación. Las excepciones se incluirán en una notificación de advertencia que se envía a la aplicación

Por ejemplo, si no se encontró ningún archivo de medios válido para la respuesta de publicidad recibida, no se puede crear ningún objeto o publicidad de recurso de publicidad válido. Como resultado, no se coloca ninguna publicidad en la línea de tiempo y se envía una notificación NotificationEvent.OperationFailed.

Los códigos de error o de advertencia que se reciben asincrónicamente desde el motor de vídeo de Adobe (AVE) se envían a la aplicación como eventos normales. El evento de notificación contiene todos los códigos de error recibidos y todos los metadatos adicionales, como la dirección URL, el identificador de recurso, el identificador, el identificador, etc. Si el error es grave y la reproducción del medio actual no puede continuar, se envía la transición de MediaPlayer al estado ERROR y al evento onStatusChanged o MediaPlayerStatusChanged.STATUS_CHANGED. Si la reproducción puede continuar, se envía un evento de notificación normal.

<table> 
 <tbody> 
  <tr> 
   <th>Error de C++ (código PSDKError)</th> 
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
   <td>Excepción con código = 1, description = "INVALID_ARGUMENT" y extraInfo= &lt;como se pasó por el método que generó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNullPointer</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ArgumentError</td> 
   <td>Excepción con código = 2, descripción = "GENERIC_ERROR" y extraInfo= &lt;como se pasó por el método que generó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECIllegalState</td> 
   <td> </td> 
   <td>IllegalStateException</td> 
   <td>IllegalStateException</td> 
   <td>Excepción con código = 3, description = "ILLEGAL_STATE" y extraInfo= &lt;como se pasó por el método que generó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInterfaceNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 4, description = "GENERIC_ERROR" y extraInfo= &lt;como se pasó por el método que generó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCreationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 5, description = "CREATION_FAILED" y extraInfo= &lt;as pasada por el método que generó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedOperation</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 5, description = "CREATION_FAILED" y extraInfo= &lt;as pasada por el método que generó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECDataNotAvailable</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 7, description = "DATA_NOT_AVAILABLE" y extraInfo= &lt;como se pasó por el método que generó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECSeekError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 8, description = "SEEK_ERROR" y extraInfo= &lt;como se pasó por el método que generó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedFeature</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 9, description = "UNSUPPORTED_FEATURE" y extraInfo= &lt;como se pasó por el método que generó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECRangeError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 10, description = "RANGE_ERROR" y extraInfo= &lt;como se pasó por el método que produjo esta excepción</td> 
  </tr> 
  <tr> 
   <td>kECCodecNotSupported</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 11, descripción = "CODEC_NOT_SUPPORTED" y adicionalInfo= &lt;como se pasó por el método que produjo esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECMediaError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 12, descripción = "MEDIA_ERROR" y extraInfo= &lt;como se pasó por el método que arrojó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNetworkError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 13, descripción = "NETWORK_ERROR" y extraInfo= &lt;según se pasó por el método que generó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECGenericError</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Error o MediaPlayerNotification.Warning</td> 
   <td>MediaError o NotificationEvent</td> 
   <td>Excepción con código = 14, descripción = "GENERIC_ERROR" y extraInfo= &lt;como se pasó por el método que generó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInvalidSeekTime</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 15, descripción = "INVALID_SEEK_TIME" y extraInfo= &lt;según se pasó por el método que generó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAudioTrackError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 16, descripción = "AUDIO_TRACK_ERROR" y extraInfo= &lt;según se pasó por el método que generó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAccessFromDifferent<p>ThreadError</p> </td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 17, descripción = "GENERIC_ERROR" y extraInfo= &lt;como se pasó por el método que generó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECElementNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 18, descripción = "GENERIC_ERROR" y extraInfo= &lt;como se pasó por el método que generó esta excepción</td> 
  </tr> 
  <tr> 
   <td>kECNotImplemented</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 19, descripción = "GENERIC_ERROR" y extraInfo= &lt;como se pasó por el método que generó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECPlaybackOperationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Excepción con código = 200, descripción = "PLAYBACK_OPERATION_FAILED" y extraInfo= &lt;según se pasó por el método que generó esta excepción&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNativeWarning</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>NotificationEvent</td> 
   <td>Excepción con código = 201, description = "NATIVE_WARNING" y extraInfo= &lt;como pasó por el método que generó esta excepción</td> 
  </tr> 
  <tr> 
   <td>kECAdResolverFailed</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>-</td> 
   <td>Excepción con código = 202, descripción = "AD_RESOLVER_FAILED" y extraInfo= &lt;según se pasó por el método que generó esta excepción&gt;</td> 
  </tr> 
 </tbody> 
</table>

## Cambios en el elemento de la API de ayuda y utilidad para 2.0 {#utility-and-helper-api-element-changes-for}

Estas tablas comparan los elementos de la API de la Utilidad y del Asistente para el SDK de JavaScript TVSDK entre las versiones 1.3 y 2.0.

Tablas en este tema:

* Versión
* TimeRange
* QOSProvider
* DeviceInformation
* LoadInfo
* Vista
* PlaybackInformation

### Versión {#version}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface Version<br /> {<br /> atributo de sólo lectura versión DomString;<br /> atributo de sólo lectura descripción DomString;<br /> atributo de sólo lectura mayor largo;<br /> atributo de sólo lectura menor largo;<br /> revisión larga del atributo de sólo lectura;<br /> atributo de sólo lectura apiVersion largo;<br /> };</p> </td> 
   <td><p>interface Version<br /> {<br /> atributo de sólo lectura versión DomString;<br /> atributo de sólo lectura descripción DomString;<br /> atributo de sólo lectura DomString mayor;<br /> atributo de sólo lectura DomString menor;<br /> atributo de sólo lectura revisión DomString;<br /> atributo de sólo lectura DomString apiVersion;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TimeRange {#timerange}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0</td> 
   <td><p>interface TimeRange<br /> {<br /> atributo de sólo lectura inicio largo sin firmar;<br /> atributo de sólo lectura sin firmar extremo largo;<br /> atributo de sólo lectura duración sin firmar;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### QOSProvider {#qosprovider}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0</td> 
   <td><p>interfaz QOSProvider<br /> {<br /> void attachMediaPlayer(reproductor de MediaPlayer);<br /> void detachMediaPlayer();<br /> <br /> atributo de sólo lectura DeviceInformation deviceInformation;<br /> atributo de sólo lectura PlaybackInformation playbackInformation;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DeviceInformation {#deviceinformation}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaz DeviceInformation<br /> {<br /> atributo de sólo lectura DomString os;<br /> <br /> <br /> atributo de sólo lectura DomString id;<br /> atributo de sólo lectura int DensidadDPI;<br /> atributo de sólo lectura int heightPixels;<br /> atributo de sólo lectura int widthPixels;&lt;a7/&gt; atributo de sólo lectura booleano searchToKeyFrame;<br /> };<br /><br /></p> </td> 
   <td><p>interfaz DeviceInformation<br /> {<br /> atributo de sólo lectura DomString os;<br /> atributo de sólo lectura int sdk;<br /> atributo de sólo lectura modelo DomString;<br /> fabricante de DomString de sólo lectura;<br /> atributo de sólo lectura DomString id;<br /> atributo de sólo lectura intDPI;<br /> readonly de lectura atributo int heightPixels;<br /> atributo de sólo lectura int widthPixels;<br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### LoadInfo {#loadinfo}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0</td> 
   <td><p>interface LoadInfo<br /> {<br /> atributo de sólo lectura url de DomString;<br /> tamaño int de atributo de sólo lectura;<br /> atributo de sólo lectura downloadDuration;<br /> atributo de sólo lectura int periodIndex;<br /> atributo de sólo lectura mediaDuration;<br /> atributo de sólo lectura abreviado TRACK_TYPE_FRAGMENT;<br /> atributo de sólo lectura abreviado TRACK_TYPE_TRACK;<br /> atributo de sólo lectura abreviado TRACK_TYPE_MANIFEST;<br /> tipo abreviado de atributo de sólo lectura;<br /> atributo de sólo lectura DomString trackName;<br /> atributo de sólo lectura DomString trackType;<br /> atributo de sólo lectura int trackIndex;&lt;a111111111 3/&gt; };<br /></p> </td> 
  </tr> 
 </tbody> 
</table>

### Vista {#view}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0</td> 
   <td><p>interfaz Vista<br /> {<br /> atributo de sólo lectura atributo sin signo x;<br /> atributo de solo lectura atributo sin signo y corto;<br /> atributo de solo lectura ancho corto sin firmar;<br /> atributo de sólo lectura altura corta sin firmar;<br /> <br /> void setSize(ancho corto sin firmar, altura corta sin firmar);<br /> void setPos(sin firmar) x corta (y sin signo);<br /> }</p> </td> 
  </tr> 
 </tbody> 
</table>

### PlaybackInformation {#playbackinformation}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface PlaybackInformation<br /> {<br /> tiempo de doble del atributo de sólo lecturaToFirstByte;<br /> tiempoToLoad del atributo de solo lectura;<br /> tiempoDedoble del atributo de solo lectura;<br /> tiempoDedoble del atributo de solo lectura;<br /> atributo de solo lectura int totalSecondsPlayed;<br /> tiempoPlayed;&lt;a6/&gt;&gt; atributo readonly int totalSecondsSpent;<br /> atributo de sólo lectura frameRate;<br /> atributo de solo lectura int droppedFrameCount;<br /> atributo de solo lectura int seenBandwidth;<br /> atributo de solo lectura bitrate;<br /> atributo de solo lectura bufferTime;<br /> atributo de solo lectura. int bufferLength;<br /> atributo de sólo lectura int emptyBufferCount;<br /> atributo de sólo lectura bufferingTime;<br /> };</p> </td> 
   <td><p>interface PlaybackInformation<br /> {<br /> tiempo de doble del atributo de sólo lecturaToFirstByte;<br /> tiempoToLoad del atributo de solo lectura;<br /> tiempoDedoble del atributo de solo lectura;<br /> tiempoDedoble del atributo de solo lectura;<br /> atributo de solo lectura int totalSecondsPlayed;<br /> tiempoPlayed;&lt;a6/&gt;&gt; atributo readonly int totalSecondsSpent;<br /> atributo de sólo lectura frameRate;<br /> atributo de sólo lectura int droppedFrameCount;<br /> <br /> atributo de solo lectura int bitrate;<br /> atributo de solo lectura bufferTime;<br /> atributo de sólo lectura int bufferLength;&lt;a1111111 3/&gt; atributo de sólo lectura int emptyBufferCount;<br /> atributo de sólo lectura bufferingTime;<br /> };<br /></p> </td> 
  </tr> 
 </tbody> 
</table>

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en la página [Información y soporte de Adobe Primetime](https://helpx.adobe.com/support/primetime.html).
