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

Para JavaScript, la sintaxis de la API se basa en el ID web. Para una interfaz TVSDK, los nombres de método se denominan *methodName*(). Para los métodos que la aplicación debe implementar, se agrega a la interfaz un atributo de lectura y escritura llamado ** methodNameCallbackFunc y la aplicación debe configurarlo para que apunte a una función que implemente el método. Por ejemplo:

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

### Metadatos temporizados {#timedmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p> <strong>Metadatos</strong>temporizados: interface TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0 ; <br /> const unsigned short METADATA_TYPE_ID3 = 1 ; <br /> atributo readonly tipo abreviado sin firmar; <br /> atributo de sólo lectura durante mucho tiempo;<br /> atributo de sólo lectura DomString id;<br /> nombre de DomString de atributo de sólo lectura;<br /> atributo de sólo lectura contenido de DomString; <br /> atributo readonly Metadatos de objeto;<br /> }; </p> </td> 
   <td><p>interface TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0 ;<br /> const unsigned short METADATA_TYPE_ID3 = 1 ;<br /> readonly attribute unsigned short metadataType;<br /> atributo de sólo lectura durante mucho tiempo;<br /> identificación larga del atributo de sólo lectura;<br /> nombre de DomString de atributo de sólo lectura;<br /> <br /> atributo readonly Metadatos de objeto;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetadataList</strong>: (Sin cambios para 2.0)</td> 
   <td><p>interface TimedMetadataList {<br /> atributo de solo lectura longitud sin firmar;<br /> getTimedMetadata(índice largo sin firmar);<br /> };</p> </td> 
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
   <td><p>Interface AdSignalingMode { <br /> const unsigned short MODE_DEFAULT, <br /> const unsigned short MODE_MANIFEST_CUES , const unsigned short MODE_SERVER_MAP , const unsigned short MODE_CUSTOM_RANGES <br /> <br /> <br /> };</p> </td> 
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
   <td><p>Interface AdvertisingMetadata { <br /> atributo AdSignalingMode; <br /> atributo AdBreakWatchedPolicy adBreakAsWatched; <br /> atributo boolean livePreroll; <br /> attribute boolean delayAdLoading ; <br /> };</p> </td> 
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
   <td><p>Interface CustomRangeMetadata { <br /> const unsigned short TYPE_MARK_RANGE; <br /> const unsigned short TYPE_DELETE_RANGE; <br /> const unsigned short TYPE_REPLACE_RANGE; <br /> atributo tipo abreviado sin firmar; <br /> atributo boolean ajustaSeekPosition; <br /> atributo TimeRangeList timeRangeList; <br /> };</p> </td> 
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
   <td><p>interface ReplaceTimeRange { <br /> atributo unsigned long begin; <br /> atributo de sólo lectura final largo sin firmar; <br /> atributo de duración larga sin firmar; <br /> attribute unsigned long replaceDuration; <br /> };</p> </td> 
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
   <td><p>Ubicación de interfaz { <br /> const unsigned short TYPE_MID_ROLL; <br /> const unsigned short TYPE_PRE_ROLL; <br /> const unsigned short TYPE_POST_ROLL; <br /> const unsigned short TYPE_SERVER_MAP; <br /> const unsigned short TYPE_CUSTOM_RANGE;<br /> atributo readonly tipo abreviado sin firmar; <br /> atributo de sólo lectura durante mucho tiempo; <br /> duración larga del atributo de sólo lectura; <br /> const unsigned short MODE_DEFAULT; <br /> const unsigned short MODE_INSERT; <br /> const unsigned short MODE_REPLACE; <br /> const unsigned short MODE_DELETE; <br /> const unsigned short MODE_MARK; <br /> const unsigned short MODE_FREE_REPLACE; <br /> atributo readonly modo abreviado sin firmar; <br /> intervalo TimeRange de atributos de sólo lectura; <br /> };</p> </td> 
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
   <td><p>interface Opportunity { <br /> readonly attribute DomString id; <br /> colocación de atributos de sólo lectura; <br /> atributos de sólo lectura Configuración de objetos; <br /> readonly attribute Object customParameters; <br /> }; </p> </td> 
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
   <td><p>interface Reservation { <br /> readonly atributo TimeRange range; <br /> retenedor largo del atributo de sólo lectura; <br /> }; </p> </td> 
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
   <td><p><strong>Cronología</strong>: interface Timeline <br /> { readonly attribute TimelineMarkerList timelineMarkers; <br /> atributo de sólo lectura TimelineItemList timelineItems; <br /> doble convertToLocalTime( tiempo de doble); <br /> doble convertToVirtualTime( tiempo de doble); <br /> };</p> </td> 
   <td><p>interfaz Línea de tiempo {<br /> atributo de sólo lectura Línea de tiempo MarcadorLista de tiempo Marcadores de línea de tiempo;<br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>TimelineItem</strong>: interface TimelineItem :<br /> TimelineMarker {<br /> readonly attribute long id; <br /> atributo de sólo lectura TimeRange virtualRange; <br /> atributo de sólo lectura TimeRange localRange; <br /> atributo de sólo lectura booleano visto; <br /> atributo de sólo lectura booleano temporal; <br /> }; </p> </td> 
   <td>(Nuevo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><strong>Marcador</strong>de línea de tiempo: (Sin cambios para 2.0)</td> 
   <td><p>interfaz TimelineMarker {<br /> tiempo de doble del atributo de solo lectura;<br /> duración del doble de atributos de solo lectura;<br /> };</p> </td> 
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
   <td><p>interfaz AdBreak {<br /> <br /> duración del doble de <br /> <br /> solo lectura;<br /> anuncios de AdList de atributos de solo lectura;<br /> <br /> <br /> atributo de sólo lectura AdInsertionType insertType;<br /> }; </p> </td> 
   <td><p>interfaz AdBreak {<br /> tiempo de doble de atributos de solo lectura;<br /> replaceDuration de doble de atributos de sólo lectura;<br /> <br /> duración del doble de atributos de solo lectura;<br /> adList de atributo de solo lectura;<br /> <br /> atributo de sólo lectura datos de DomString;<br /> <br /> }; </p> </td> 
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
   <td><p> <strong>Publicidad</strong>: anuncio de interfaz {<br /> atributo de solo lectura AdAsset primarioAsset;<br /> atributo de solo lectura AdAssetList CompanionAssets;<br /> <br /> duración del doble de atributos de solo lectura;<br /> atributo de sólo lectura DomString id;<br /> const unsigned short ADTYPE_LINEAR = 0 ;<br /> const unsigned short ADTYPE_NONLINEAR = 1 ;<br /> <br /> atributo readonly adType corto sin firmar;<br /> atributo de sólo lectura AdInsertionType adInsertionType; <br /> <br /> se puede hacer clic en booleano de atributo de solo lectura; <br /> el booleano de atributos de sólo lectura isCustomAdMarker;<br /> }; </p> </td> 
   <td><p>anuncio de interfaz {<br /> atributo de solo lectura AdAsset primarioAsset;<br /> atributo de solo lectura AdAssetList CompanionAssets;<br /> <br /> duración del doble de atributos de solo lectura;<br /> atributo de sólo lectura DomString id;<br /> const unsigned short ADTYPE_LINEAR = 0 ;<br /> const unsigned short ADTYPE_NONLINEAR = 1 ;<br /> <br /> atributo readonly tipo abreviado sin firmar;<br /> atributo de sólo lectura AdInsertionType insertType; <br /> rastreador de objetos de atributo readonly;<br /> <br /> <br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>: (Sin cambios para 2.0)</td> 
   <td><p>interfaz AdAsset {<br /> atributo de solo lectura DomString id;<br /> duración del doble de atributos de solo lectura;<br /> atributo de solo lectura MediaResource resource;<br /> atributo AdClick adClick de sólo lectura;<br /> atributo readonly Metadatos de objeto;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>: (Sin cambios para 2.0)</td> 
   <td><p>interfaz AdClick {<br /> atributo de sólo lectura DomString id;<br /> atributo de sólo lectura DomString title;<br /> url de DomString de atributo de sólo lectura;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdList</strong>: (Sin cambios para 2.0)</td> 
   <td><p>interfaz AdList {<br /> atributo de solo lectura longitud sin firmar;<br /> get Ad (índice largo sin firmar);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>: (Sin cambios para 2.0)</td> 
   <td><p>interfaz AdAssetList {<br /> atributo de solo lectura longitud sin firmar;<br /> getAdAsset(índice largo sin firmar);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>: interfaz AdBannerAsset : AdAsset<br /> {<br /> atributo int de solo lectura width;<br /> atributo int height de sólo lectura;<br /> atributo de sólo lectura DomString staticUrl;<br /> Altura de DomString de atributo de sólo lectura;<br /> atributo de sólo lectura DomString width;<br /> };</p> </td> 
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
   <td><p> <strong>AdBreakTimelineItem</strong>: interfaz AdBreakTimelineItem: TimelineItem { <br /> atributo de sólo lectura AdBreak adBreak; <br /> elementos AdTimelineItemList de atributo de solo lectura; <br /> }; </p> </td> 
   <td> (Nuevo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimelineItem</strong>: interfaz AdTimelineItem : TimelineItem { <br /> atributo de sólo lectura AdBreak adBreak; <br /> anuncio de atributo de solo lectura; <br /> }; </p> </td> 
   <td> (Nuevo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>: interface AdBreakTimelineItemList { <br /> atributo de solo lectura longitud sin firmar; <br /> get AdBreakTimelineItem (índice de eventos sin firmar); <br /> };</p> </td> 
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
   <td><p>interfaz AdBreakPolicy {<br /> atributo de solo lectura abreviado AD_BREAK_POLICY_SKIP;<br /> atributo readonly short AD_BREAK_POLICY_PLAY;<br /> atributo readonly short AD_BREAK_POLICY_REMOVE;<br /> atributo de sólo lectura short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;<br /> };</p> </td> 
   <td><p> interfaz AdPolicyConstances {<br /> atributo readonly corto AD_BREAK_POLICY_SKIP;<br /> atributo readonly short AD_BREAK_POLICY_PLAY;<br /> atributo readonly short AD_BREAK_POLICY_REMOVE;<br /> atributo readonly abreviado AD_BREAK_POLICY_REMOVE_AFTER_PLAY;}<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p> interfaz AdBreakWatchedPolicy {<br /> atributo de solo lectura abreviado AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> atributo readonly short AD_BREAK_AS_WATCHED_ON_END;<br /> atributo readonly short AD_BREAK_AS_WATCHED_NEVER;<br /> }; </p> </td> 
   <td><p> ...<br /> atributo readonly short AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> atributo readonly short AD_BREAK_AS_WATCHED_ON_END;<br /> atributo readonly short AD_BREAK_AS_WATCHED_NEVER;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaz AdPolicy {<br /> readonly attribute short AD_POLICY_PLAY;<br /> atributo readonly short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> atributo de sólo lectura short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN; atributo de sólo lectura short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> <br /> atributo readonly short AD_POLICY_SKIP_AD_BREAK;<br /> };</p> </td> 
   <td><p> ... <br /> atributo readonly short AD_POLICY_PLAY;<br /> atributo readonly short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> atributo de sólo lectura short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;<br /> atributo de sólo lectura short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> atributo readonly short AD_POLICY_SKIP_AD_BREAK;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaz AdPolicyMode {<br /> readonly attribute short AD_POLICY_MODE_PLAY;<br /> atributo readonly short AD_POLICY_MODE_SEEK;<br /> atributo readonly short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
   <td><p> ...<br /> {readonly attribute short AD_POLICY_MODE_PLAY;<br /> atributo readonly short AD_POLICY_MODE_SEEK;<br /> atributo readonly short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaz AdPolicyInfo {<br /> atributo de solo lectura AdBreakTimelineItemList y <br /> BreakTimelineItems;<br /> atributo AdTimelineItem de sólo lectura adTimelineItem;<br /> doble de atributos de solo lectura currentTime;<br /> doble de atributos de sólo lectura, searchToTime;<br /> velocidad de doble de atributos de solo lectura;<br /> modo abreviado de atributo de sólo lectura; //AdPolicyMode<br /> };</p> </td> 
   <td><p>interfaz AdPolicyInfo {<br /> atributo de solo lectura AdBreakPlacementList y <br /> BreakPlacements;<br /> anuncio de atributo de solo lectura;<br /> doble de atributos de solo lectura currentTime;<br /> doble de atributos de sólo lectura, searchToTime;<br /> velocidad de doble de atributos de solo lectura;<br /> modo abreviado de atributo de sólo lectura; //AdPolicyMode<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaz AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectPolicyForAdBreakCallbackFunc;<br /> /**<br /> * AdBreakTimelineItemList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectAdBreaksToPlayCallbackFunc;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectPolicyForSeekIntoAdCallbackFunc; <br /> /**<br /> * AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectWatchedPolicyForAdBreakCallbackFunc;<br /> };</p> </td> 
   <td><p>interfaz AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectPolicyForAdBreakFuncCallback;<br /> /**<br /> * AdBreakPlacementList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectAdBreaksToPlayCallback;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectPolicyForSeekIntoAdCallback; <br /> /**<br /> * AdBreakAsWatched selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectWatchedPolicyForAdBreakCallback;<br /> };</p> </td> 
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
   <td><p>interfaz TimelineOperation { <br /> readonly attribute Ubicación del atributo ; <br /> };</p> </td> 
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
   <td><p>interfaz AdBreakPlacement: TimelineOperation {<br /> atributo de sólo lectura AdBreak adBreak;<br /> colocación de atributos de sólo lectura; // Desde TimelineOperation<br /> tiempo de doble de atributos de solo lectura;<br /> duración del doble de atributos de solo lectura;<br /> };</p> </td> 
   <td><p>interfaz AdBreakPlacement {<br /> atributo de solo lectura AdBreak adBreak;<br /> colocación de atributos de sólo lectura;<br /> tiempo de doble de atributos de solo lectura;<br /> duración del doble de atributos de solo lectura;<br /> };</p> </td> 
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
   <td><p>interfaz AuditudeSettings: AdvertisingMetadata { <br /> atributo DomString zoneId; <br /> atributo DomString mediaId; <br /> atributo DomString defaultMediaId ; <br /> atributo dominio DomString ; <br /> attribute Object targetInfo ; <br /> attribute Object customParameters ; <br /> attribute Boolean creativePackaingEnabled ;<br /> atributo Boolean showStaticBanners ;<br /> };</p> </td> 
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
   <td><p>interfaz MediaPlayerItemConfig {<br /> atributo ContentFactory adFactory;<br /> attribute StringList subscriptionTags;<br /> <br /> attribute StringList adTags;<br /> <br /> <br /> atributo AdSignalingMode adSignalingMode;<br /> atributo CustomRangeMetadata customRangeMetadata;<br /> atributo NetworkConfiguration networkConfiguration;<br /> atributo AdvertisingMetadata publicidadMetadata;<br /> attribute Boolean useHardwareDecoder;<br /> };</p> </td> 
   <td><p>interfaz MediaPlayerConfig {<br /> <br /> atributo <br /> <br /> StringList adTags;<br /> attribute StringList subscribedTags;<br /> atributo MediaPlayerClientFactory clientFactory;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
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
   <td><p>interfaz ContentFactory {<br /> /*<br /> * AdPolicySelector recuperarAdPolicySelector(<br /> * elemento MediaPlayerItem);<br /> */<br /> atributo Object recuperaAdPolicySelectorCallbackFunc;<br /> };</p> </td> 
   <td><p>interfaz MediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector recuperarAdPolicySelector(<br /> * elemento MediaPlayerItem);<br /> */<br /> attribute Object recuperaAdPolicySelectorFunc;<br /> };</p> </td> 
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
   <td><p>interfaz NetworkConfiguration<br /> {<br /> atributo boolean forceNativeNetworking;<br /> atributo booleano useRedirectUrl;<br /> attribute Object cookieHeader;<br /> atributo booleano readSetCookieHeader;<br /> attribute int masterUpdateInterval; <br /> atributo booleano useCookieHeaderForAllRequests;<br /> attribute int readLimit;<br /> };</p> </td> 
   <td>En 1.3, MetadataKeys proporcionó parte de esta funcionalidad</td> 
  </tr> 
 </tbody> 
</table>

## Cambios en elementos de la API de DRM para 2.0 {#drm-api-element-changes-for}

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
   <td>La aplicación debe llamar a AdobePSDK.initiateDRMWorkflow para iniciar el flujo de trabajo de DRM. Sin esta llamada, los vídeos DRM no se reproducirán.<p>interfaz AdobePSDK<br /> {<br /> void initiateDRMWorkFlow(<br /> DomString appStoratePath, DomString publisherId, DomString appId, <br /> DomString appVersion, <br /> <br /> <br /> boolean privacyModeOn);<br /> };</p> </td> 
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
   <td><p>interfaz DRMMetadata<br /> {<br /> atributo de sólo lectura DomString serverUrl;<br /> readonly attribute DomString licenseId;<br /> políticas DRMPolicyArray de atributos de sólo lectura; <br /> };</p> </td> 
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
   <td><p>interfaz DRMPlaybackTimeWindow {<br /> atributo de sólo lectura int playbackPeriodInSeconds;<br /> atributo readonly long playStartDate;<br /> atributo readonly long playEndDate;<br /> };</p> </td> 
   <td><p>interfaz DRMPlaybackTimeWindow {<br /> atributo de sólo lectura int periodInSeconds;<br /> atributo de sólo lectura int startDate;<br /> atributo de sólo lectura int endDate;<br /> };</p> </td> 
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
   <td><p>interfaz DRMLicense {<br /> readonly attribute Uint8Array bytes;<br /> atributo de sólo lectura Date licenseStartDate;<br /> atributo de sólo lectura Date licenseEndDate;<br /> atributo de sólo lectura Date offlineStorageStartDate;<br /> atributo de sólo lectura Date offlineStorageEndDate; <br /> atributo de sólo lectura DomString serverUrl;<br /> readonly attribute DomString licenseID;<br /> atributo de sólo lectura DomString policyID;<br /> atributo de sólo lectura DRMPlaybackTimeWindow playbackTimeWindow;<br /> atributo de sólo lectura CustomProperties;<br /> }; </p> </td> 
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
   <td><p>interfaz DRMLicenseDomain {<br /> atributo de sólo lectura DomString authenticationDomain;<br /> readonly attribute DRMAuthauthenticationMethod authenticationMethod; <br /> atributo de sólo lectura DomString serverUrl;<br /> };</p> </td> 
   <td><p>interfaz DRMLicenseDomain {<br /> atributo de sólo lectura DomString authDomain;<br /> atributo de sólo lectura DRMAuthauthenticationMethod authMethod; <br /> atributo de sólo lectura DomString serverURL;<br /> };</p> </td> 
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
   <td><p>interfaz DRMPolicy<br /> {<br /> readonly attribute DomString authenticationDomain;<br /> readonly attribute DRMAuthauthenticationMethod authenticationMethod;<br /> <br /> atributo de sólo lectura DomString displayName;<br /> atributo de sólo lectura DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
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
   <td><p>interfaz DRMManager: EventTarget {<br /> void acquisitionLicense(metadatos DRMMetadata, <br /> configuración de DRMAcquireLicenseSettings, detector <br /> DRMAquireLicenseListener);<br /> void acquisitionPreviewLicense(metadatos DRMMetadata, detector <br /> DRMAquireLicenseListener);<br /> void authentication(metadatos DRMMetadata, dirección URL de DomString, <br /> dominio de autenticación de DomString y DomString,<br /> usuario de DomString, <br /> contraseña de DomString, <br /> <br /> detector de DRMAuthenticateListener);<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> matriz Uint8Array, detector DRMErrorListener);<br /> void initialize(detector DRMOperationCompleteListener);<br /> atributo long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> detector DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, <br /> DRMOperationCompleteListener);<br /> void allowLicenseDomain(<br /> detector de licenseDomain de DRMLicenseDomain, <br /> DRMOperationCompleteListener);<br /> <br /> void resetDRM(detector DRMOperationCompleteListener);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID, <br /> DomString policyID, <br /> boolean commitInmediatamente,<br /> detector DRMReturnLicenseListener);<br /> void setAuthenticationToken(<br /> metadatos DRMMetadata, <br /> DomString authenticationDomain, token <br /> Uint8Array, <br /> detector DRMOperationCompleteListener);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> detector DRMOperationCompleteListener);<br /> };</p> </td> 
   <td><p>interfaz DRMManager: EventTarget {<br /> void acquisitionLicense(metadatos DRMMetadata, <br /> configuración de DRMAcquireLicenseSettings, <br /> EventContext eventContext);<br /> void acquisitionPreviewLicense(metadatos DRMMetadata, <br /> EventContext eventContext);<br /> void authentication(metadatos DRMMetadata, <br /> URL de DomString,<br /> DomString &amp;authenticationDomain, usuario <br /> de DomString, contraseña de DomString, <br /> <br /> eventContext);<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> matriz Uint8Array, EventContext eventContext);<br /> void initialize(EventContext eventContext);<br /> atributo long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, <br /> EventContext eventContext);<br /> void leftLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> EventContext eventContext);<br /> <br /> void resetDRM(EventContext eventContext);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID,<br /> DomString policyID, <br /> boolean commitInmediatamente,<br /> EventContext eventContext);<br /> void setAuthenticationToken(<br /> metadatos DRMMetadata, <br /> DomString authenticationDomain, token <br /> <br /> Uint8Array, eventContext eventContext);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> EventContext eventContext);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>clase DRMErrorListener: <br /> public psdkutils::PSDKInterfaceWithUserData {<br /> public:<br /> virtual void onDRMError(uint32_t major, <br /> uint32_t minor, <br /> const psdkutils: PSDKString&amp; errorString, <br /> const psdkutils::PSDKString&amp; errorServerUrl) = 0;<br /> <br /> protected:<br /> virtual ~DRMErrorListener() {}<br /> }</p> </td> 
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
   <td><p>clase DRMAuthenticateListener: <br /> public DRMErrorListener {<br /> public:<br /> virtual void onAuthenticationComplete(<br /> psdkutils::PSDKImmutableByteArray* <br /> authenticationToken) = 0;<br /> <br /> protected:<br /> virtual ~DRMAuthenticateListener() {}<br /> }</p> </td> 
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

## Cambios genéricos del elemento API de reproducción para 2.0 {#generic-playback-api-element-changes-for}

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
   <td><p>interfaz MediaResource {<br /> atributo DomString url; <br /> atributo tipo abreviado sin firmar;<br /> metadatos del objeto attribute;<br /> const unsigned short TYPE_HLS;<br /> const unsigned short TYPE_HDS;<br /> const unsigned short TYPE_DASH;<br /> const unsigned short TYPE_CUSTOM;<br /> const unsigned short TYPE_UNKNOWN;<br /> };</p> </td> 
   <td><p>interfaz MediaResource {<br /> atributo DomString url;<br /> atributo DomString type;<br /> metadatos del objeto attribute;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
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
   <td><p>interfaz MediaPlayer: EventTarget<br /> {<br /> void prepareToPlay( posición de doble);<br /> void play();<br /> void pause();<br /> void search( posición de doble);<br /> void searchToLocal( posición de doble);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem(elemento MediaPlayerItem);<br /> void replaceCurrentResource(MediaResource, <br /> configuración de MediaPlayerItemConfig); <br /> void suspensión();<br /> void restore();<br /> void notificationClick();<br /> <br /> atributo de sólo lectura TimeRange playbackRange;<br /> atributo de sólo lectura TimeRange seekableRange;<br /> doble de atributos de solo lectura currentTime;<br /> doble localTime de atributos de sólo lectura;<br /> atributo de sólo lectura TimeRange bufferedRange;<br /> atributo de sólo lectura DRMManager drmManager;<br /> atributo de sólo lectura MediaPlayerItem currentItem;<br /> <br /> // PlayerStatus<br /> <br /> const <br /> unsigned short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEEKING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /> <br /> atributo de sólo lectura estado corto sin firmar;<br /> <br /> atributo volumen corto sin firmar;<br /> attribute ABRControlParameters abrControlParameters;<br /> atributo BufferControlParameters bufferControlParameters;<br /> <br /> const unsigned short VISIBLE; //Para CC visibility<br /> const unsigned short INVISIBLE; //Para CC visibility<br /> attribute unsigned short ccVisibility;<br /> atributo TextFormat ccStyle;<br /> atributo de sólo lectura PlaybackMetrics playMetrics;<br /> <br /> tasa de doble de atributos;<br /> vista de atributo MediaPlayerView;<br /> escala de tiempo del atributo de solo lectura;<br /> doble de atributos currentTimeUpdateInterval; <br /> // establecer esto no será compatible con 2.0<br /> };</p> </td> 
   <td><p>interfaz MediaPlayer: EventTarget<br /> {<br /> void prepareToPlay( posición int);<br /> void play();<br /> void pause();<br /> void search( posición int);<br /> void searchToLocalTime( posición int);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem(fuente de MediaResource);<br /> <br /> <br /> <br /> <br /> <br /> <br /> atributo de sólo lectura TimeRange playbackRange;<br /> atributo de sólo lectura TimeRange seekableRange;<br /> doble de atributos de solo lectura currentTime;<br /> doble localTime de atributos de sólo lectura;<br /> atributo de sólo lectura TimeRange bufferedRange;<br /> atributo de sólo lectura DRMManager drmManager;<br /> atributo de sólo lectura MediaPlayerItem currentItem;<br /> <br /> // PlayerState<br /> const unsigned short PLAYER_STATE_IDLE;<br /> const unsigned short PLAYER_STATE_INITIALIZING;<br /> const unsigned short PLAYER_STATE_INITIALIZED;<br /> const unsigned short PLAYER_STATE_PREPARING;<br /> const unsigned short PLAYER_STATE_PREPARED;<br /> const unsigned short PLAYER_STATE_PLAYING;<br /> const unsigned short PLAYER_STATE_PAUSED;<br /> const unsigned short PLAYER_STATE_SEEKING;<br /> const unsigned short PLAYER_STATE_COMPLETE;<br /> const unsigned short PLAYER_STATE_ERROR;<br /> const unsigned short PLAYER_STATE_RELEASED;<br /> const unsigned short PLAYER_STATUS_SUSPENDED;<br /> atributo readonly estado corto sin signo;<br /> <br /> atributo volumen corto sin firmar;<br /> attribute ABRControlParameters abrControlParameters;<br /> atributo BufferControlParameters bufferControlParameters;<br /> <br /> readonly unsigned short VISIBLE; //Para la visibilidad<br /> CC lésólo lectura corta no firmada INVISIBLE; //Para CC visibility<br /> attribute unsigned short ccVisibility;<br /> atributo TextFormat ccStyle;<br /> atributo de sólo lectura PlaybackMetrics playMetrics;<br /> atributo MediaPlayerConfig mediaPlayerConfig;<br /> tasa de doble de atributos;<br /> vista de atributo MediaPlayerView;<br /> escala de tiempo del atributo de solo lectura;<br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerStatus<br /> {<br /> // PlayerStatus<br /> const unsigned short PLAYER_STATUS_IDLE;<br /> const unsigned short PLAYER_STATUS_INITIALIZING;<br /> const unsigned short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEEKING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /> const unsigned short PLAYER_STATUS_SUSPENDED;<br /> };</p> </td> 
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
   <td>adClic<br /> Cuando el usuario hace clic en una publicidad.</td> 
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
   <td>audioActualizado<br /> al actualizar un elemento de reproductor multimedia. Para determinados flujos que contienen pistas de audio que solo se pueden detectar durante la reproducción, este evento se activa cuando hay nuevas pistas de audio disponibles.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Nuevo en 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>captionsActualizado <br /> Cuando se actualiza un elemento de reproductor de medios. En el caso de los flujos en vivo/lineales, el cliente debe actualizar periódicamente el recurso de medios para detectar el nuevo contenido disponible. Cuando esto sucede, ciertas características de los medios pueden cambiar.</td> 
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
   <td>timedEvent<br /> enviado cuando se generan eventos temporizados.</td> 
   <td>TimedEvent</td> 
   <td> </td> 
   <td><p>Nuevo en 2.0</p> </td> 
  </tr> 
 </tbody> 
</table>

### ABRControlParameters {#abrcontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ;<br /> const unsigned short ABR_POLICY_MODERATE = 1 ;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> attribute unsigned short abrPolicy;<br /> atributo unsigned int initialBitRate;<br /> atributo unsigned int minBitRate;<br /> atributo unsigned int maxBitRate;<br /> const unsigned short DEFAULT_ABR_INITIAL_BITRATE;<br /> const unsigned short DEFAULT_ABR_MIN_BITRATE;<br /> const unsigned short DEFAULT_ABR_MAX_BITRATE;<br /> const ABRPolicy DEFAULT_ABR_POLICY;<br /> };</p> </td> 
   <td><p>interface ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ;<br /> const unsigned short ABR_POLICY_MODERATE = 1 ;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> attribute unsigned short abrPolicy;<br /> atributo unsigned int initialBitRate;<br /> atributo unsigned int minBitRate;<br /> atributo unsigned int maxBitRate;<br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Parámetros de BufferControl {#buffercontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface BufferControlParameters<br /> {<br /> doble de atributos initialBufferTime;<br /> doble de atributos playBufferTime;<br /> doble DE CONst DEFAULT_INITIAL_BUFFER_TIME;<br /> doble DE CONst DEFAULT_PLAY_BUFFER_TIME;<br /> };</p> </td> 
   <td><p>interface BufferControlParameters<br /> {<br /> doble de atributos initialBufferTime;<br /> doble de atributos playBufferTime;<br /> <br /> <br /> };</p> </td> 
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
   <td><p>interface TextFormat<br /> {<br /> // Color<br /> const unsigned short COLOR_DEFAULT = 0 ;<br /> const unsigned short COLOR_BLACK = 1 ;<br /> const unsigned short COLOR_GRAY = 2 ;<br /> const unsigned short COLOR_WHITE = 3 ;<br /> const unsigned short COLOR_BRIGHT_WHITE = 4 ;<br /> const unsigned short COLOR_DARK_RED = 5 ;<br /> const unsigned short COLOR_RED = 6 ;<br /> const unsigned short COLOR_BRIGHT_RED = 7 ;<br /> const unsigned short COLOR_DARK_GREEN = 8 ;<br /> const unsigned short COLOR_GREEN = 9 ;<br /> const unsigned short COLOR_BRIGHT_GREEN = 10 ;<br /> const unsigned short COLOR_DARK_BLUE = 11 ;<br /> const unsigned short COLOR_BLUE = 12 ;<br /> const unsigned short COLOR_BRIGHT_BLUE = 13 ;<br /> const unsigned short COLOR_DARK_YELLOW = 14 ;<br /> const unsigned short COLOR_YELLOW = 15 ;<br /> const unsigned short COLOR_BRIGHT_YELLOW = 16 ;<br /> const unsigned short COLOR_DARK_MAGENTA = 17 ;<br /> const unsigned short COLOR_MAGENTA = 18 ;<br /> const unsigned short COLOR_BRIGHT_MAGENTA = 19 ;<br /> const unsigned short COLOR_DARK_CYAN = 20 ;<br /> const unsigned short COLOR_CYAN = 21 ;<br /> const unsigned short COLOR_BRIGHT_CYAN = 22 ;<br /> <br /> atributo readonly fontColor corto sin signo;<br /> atributo de sólo lectura unsigned short backgroundColor;<br /> atributo readonly short fillColor sin firmar;<br /> atributo readonly short edgeColor sin signo;<br /> <br /> // Tamaño<br /> const unsigned short SIZE_DEFAULT = 0 ;<br /> const unsigned short SIZE_SMALL = 1 ;<br /> const unsigned short SIZE_MEDIUM = 2 ;<br /> const unsigned short SIZE_LARGE = 3 ;<br /> <br /> atributo de sólo lectura de tamaño corto sin firmar;<br /> <br /> // FontEdge<br /> const unsigned short FONT_EDGE_DEFAULT = 0 ;<br /> const unsigned short FONT_EDGE_NONE = 1 ;<br /> const unsigned short FONT_EDGE_RAISED = 2 ;<br /> const unsigned short FONT_EDGE_DEPRESSED = 3 ;<br /> const unsigned short FONT_EDGE_UNIFORM = 4 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_LEFT = 5 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_RIGHT = 6 ;<br /> atributo readonly fontEdge corto sin signo;<br /> <br /> // Font<br /> const unsigned short FONT_DEFAULT = 0 ;<br /> const unsigned short FONT_MONOSPACED_WITH_SERIFS = 1 ;<br /> const unsigned short FONT_PROPORTIONAL_WITH_SERIFS = 2 ;<br /> const unsigned short FONT_MONSPACED_WITHOUT_SERIFS = 3 ;<br /> const unsigned short FONT_CASUAL = 4 ;<br /> const unsigned short FONT_CURSIVE = 5 ;<br /> const unsigned short FONT_SMALL_CAPITALS = 6 ;<br /> atributo readonly fuente corta sin signo;<br /> atributo readonly fontOpacity corto sin signo;<br /> readonly attribute unsigned short backgroundOpacity;<br /> atributo de sólo lectura short fill sin firmarOpacidad;<br /> atributo readonly unsigned short DEFAULT_OPACITY;<br /> };</p> </td> 
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
   <td><p>interfaz MediaPlayerItemLoader:<br /> {<br /> void load(recurso de MediaResource, resourceId largo,<br /> <br /> detector de ItemLoaderListener, configuración de MediaPlayerItemConfig) ;<br /> void cancel();<br /> atributo de sólo lectura MediaPlayerItem currentItem;<br /> };</p> </td> 
   <td>Nuevo para 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interface ItemLoaderListener<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc;<br /> //onErrorCallbackFunc(PSDKErrorCode)<br /> var onErrorCallbackFunc;<br /> }</p> </td> 
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
   <td><p>interfaz MediaPlayerItem {<br /> atributo de solo lectura MediaResource resource;<br /> atributo readonly long resourceId;<br /> atributo de solo lectura booleano activo;<br /> <br /> el atributo readonly boolean hasAlternateAudio;<br /> atributo de sólo lectura AudioTrackList (pistas de audio);<br /> atributo de sólo lectura AudioTrack selectedAudioTrack;<br /> void selectAudioTrack(pista AudioTrack); <br /> <br /> atributo readonly boolean hasClosedCaptions;<br /> atributo de sólo lectura ClosedCaptionsTrackList ClosedCaptionsTracks;<br /> atributo de sólo lectura ClosedCaptionsTrack selectedClosedCaptionsTrack;<br /> void selectClosedCaptionsTrack(<br /> ClosedCaptionsTrack track); <br /> <br /> el valor boolean de atributo readonly hasTimedMetadata;<br /> atributo de sólo lectura TimedMetadataList timedMetadata;<br /> atributo de sólo lectura booleano dinámico;<br /> <br /> atributo de sólo lectura boolean isProtected;<br /> atributo de sólo lectura DRMMetadataInfoList drmMetadataInfos;<br /> perfiles ProfileList de atributos de sólo lectura;<br /> perfil de atributos de sólo lectura selectedProfile;<br /> <br /> atributo de sólo lectura booleano: tapPlaySupported;<br /> atributo de sólo lectura FloatArray availablePlaybackRates;<br /> atributo de sólo lectura float selectedPlaybackRate;<br /> <br /> <br /> atributo de sólo lectura MediaPlayer mediaPlayer;<br /> atributo de sólo lectura MediaPlayerItemConfig config;<br /> };</p> </td> 
   <td><p>interfaz MediaPlayerItem {<br /> atributo de solo lectura MediaResource resource;<br /> atributo readonly long resourceId;<br /> atributo de solo lectura booleano activo;<br /> <br /> el atributo readonly boolean hasAlternateAudio;<br /> atributo de sólo lectura AudioTrackList (pistas de audio);<br /> atributo AudioTrack selectedAudioTrack;<br /> <br /> <br /> atributo readonly boolean hasClosedCaptions;<br /> atributo de sólo lectura ClosedCaptionsTrackList ccTracks;<br /> atributo ClosedCaptionsTrack selectedCCTrack;<br /> <br /> <br /> <br /> el valor boolean de atributo readonly hasTimedMetadata;<br /> atributo de sólo lectura TimedMetadataList timedMetadata;<br /> atributo de sólo lectura booleano dinámico;<br /> <br /> atributo de sólo lectura boolean isProtected;<br /> atributo de sólo lectura DRMMetadataInfoList drmMetadataInfos;<br /> perfiles ProfileList de atributos de sólo lectura;<br /> <br /> <br /> atributo de sólo lectura booleano: tapPlaySupported;<br /> atributo de sólo lectura Int32Array availablePlaybackRates;<br /> <br /> readonly attribute StringList adTags;<br /> <br /> atributo de sólo lectura MediaPlayer mediaPlayer;<br /> <br /> };</p> </td> 
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
   <td><p>interfaz Track<br /> {<br /> readonly attribute DomString name;<br /> lenguaje DomString de atributo de sólo lectura;<br /> atributo readonly booleano predeterminado;<br /> atributo readonly boolean autoSelect;<br /> }; </p> </td> 
   <td>Nuevo para 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interfaz AudioTrack: Track<br /> {<br /> readonly attribute DomString name; //FromTrack<br /> atributo de sólo lectura lenguaje DomString;//FromTrack<br /> atributo de sólo lectura predeterminado booleano; // Desde Track<br /> readonly atributo boolean autoSelect;//FromTrack<br /> <br /> atributo de sólo lectura unsigned int pid;<br /> };</p> </td> 
   <td><p>interfaz AudioTrack<br /> {<br /> atributo de sólo lectura nombre de DomString;<br /> lenguaje DomString de atributo de sólo lectura; <br /> atributo readonly booleano predeterminado;<br /> atributo readonly boolean autoSelect;<br /> valor booleano de atributo de solo lectura forzado;<br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0</td> 
   <td><p>interfaz AudioTrackList<br /> {<br /> atributo de sólo lectura longitud sin signo;<br /> getter AudioTrack (índice largo sin firmar);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaz ClosedCaptionsTrack: Track<br /> {<br /> readonly attribute DomString name; //FromTrack<br /> atributo de sólo lectura lenguaje DomString;//FromTrack<br /> atributo de sólo lectura predeterminado booleano; // Atributo de sólo lectura FromTrack<br /> autoSelect booleano;//FromTrack<br /> const <br /> <br /> unsigned short SERVICE_608_CAPTIONS = 0;<br /> const unsigned short SERVICE_708_CAPTIONS = 1;<br /> const unsigned short SERVICE_WEB_VTT_CAPTIONS = 2;<br /> atributo readonly serviceType corto sin firmar;<br /> valor booleano de atributo de solo lectura forzado;<br /> };</p> </td> 
   <td><p>interfaz ClosedCaptionsTrack<br /> {<br /> atributo de sólo lectura nombre de DomString;<br /> lenguaje DomString de atributo de sólo lectura;<br /> atributo readonly booleano predeterminado;<br /> <br /> <br /> atributo de sólo lectura booleano activo;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>Sin cambios para 2.0</td> 
   <td><p>interfaz ClosedCaptionsTrackList<br /> {<br /> atributo de sólo lectura longitud sin signo;<br /> getter ClosedCaptionsTrack(índice largo sin firmar);<br /> };</p> </td> 
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
   <td><p>perfil<br /> de interfaz {<br /> atributo de sólo lectura unsigned int width;<br /> atributo de sólo lectura sin firmar int height;<br /> atributo readonly unsigned int bitRate;<br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td>ProfileList: Sin cambios para 2.0</td> 
   <td><p>interface ProfileList<br /> {<br /> atributo de sólo lectura longitud sin firmar;<br /> perfil de captador (índice largo sin firmar);<br /> };</p> </td> 
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
   <td><p>interfaz DRMMetadataInfo<br /> { <br /> atributo de sólo lectura Metadatos DRMMetadata;<br /> readonly attribute long prefetchTimestamp;<br /> atributo de sólo lectura TimeRange timeRange;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>: Sin cambios para 2.0</td> 
   <td><p>interfaz DRMMetadataInfoList<br /> {<br /> atributo de sólo lectura longitud sin signo;<br /> getter DRMMetadataInfo(índice largo sin firmar);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## Asignación de errores de C++ a excepciones en distintos idiomas {#mapping-c-errors-to-exceptions-in-different-languages}

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

## Cambios en los elementos de la API de ayuda y la utilidad para 2.0 {#utility-and-helper-api-element-changes-for}

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
   <td><p>interfaz Versión<br /> {<br /> atributo de sólo lectura DomString versión;<br /> atributo de sólo lectura Descripción de DomString;<br /> atributo readonly long major;<br /> atributo de sólo lectura menor largo;<br /> revisión larga del atributo readonly;<br /> atributo readonly long apiVersion;<br /> };</p> </td> 
   <td><p>interfaz Versión<br /> {<br /> atributo de sólo lectura DomString versión;<br /> atributo de sólo lectura Descripción de DomString;<br /> atributo de sólo lectura DomString mayor;<br /> atributo de sólo lectura DomString secundario;<br /> revisión DomString de atributo de sólo lectura;<br /> atributo de sólo lectura DomString apiVersion;<br /> };</p> </td> 
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
   <td><p>interface TimeRange<br /> {<br /> atributo de sólo lectura unsigned long begin;<br /> atributo de sólo lectura final largo sin firmar;<br /> atributo de sólo lectura de duración larga sin firmar;<br /> };</p> </td> 
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
   <td><p>interfaz DeviceInformation<br /> {<br /> atributo de solo lectura DomString os;<br /> <br /> <br /> <br /> atributo de sólo lectura DomString id;<br /> atributo de sólo lectura int DensidadDPI;<br /> atributo de sólo lectura int heightPixels;<br /> atributo de sólo lectura int widthPixels;<br /> atributo de sólo lectura booleano searchToKeyFrame;<br /> };</p> </td> 
   <td><p>interfaz DeviceInformation<br /> {<br /> atributo de solo lectura DomString os;<br /> atributo de sólo lectura int sdk;<br /> atributo de sólo lectura modelo DomString;<br /> fabricante de DomString de sólo lectura;<br /> atributo de sólo lectura DomString id;<br /> atributo de sólo lectura int DensidadDPI;<br /> atributo de sólo lectura int heightPixels;<br /> atributo de sólo lectura int widthPixels;<br /> <br /> };</p> </td> 
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
   <td><p>interfaz LoadInfo<br /> {<br /> atributo de sólo lectura url de DomString;<br /> atributo int size de sólo lectura;<br /> downloadDuration del doble de atributos de sólo lectura;<br /> atributo de sólo lectura int periodIndex;<br /> doble mediaDuration de atributos de sólo lectura;<br /> atributo de sólo lectura abreviado TRACK_TYPE_FRAGMENT;<br /> atributo readonly short TRACK_TYPE_TRACK;<br /> atributo readonly short TRACK_TYPE_MANIFEST;<br /> tipo abreviado de atributo de sólo lectura;<br /> atributo de sólo lectura DomString trackName;<br /> atributo de sólo lectura DomString trackType;<br /> atributo de sólo lectura int trackIndex;<br /> };</p> </td> 
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
   <td><p>vista<br /> de interfaz {<br /> atributo de sólo lectura unsigned short x;<br /> atributo de sólo lectura sin signo y corto;<br /> atributo de sólo lectura sin firmar ancho corto;<br /> atributo readonly altura corta sin firmar;<br /> <br /> void setSize(unsigned short width, unsigned short height);<br /> void setPos(unsigned short x, unsigned short y);<br /> }</p> </td> 
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
   <td><p>interface PlaybackInformation<br /> {<br /> readonly attribute timeToFirstByte;<br /> timeToLoad del doble de atributos de sólo lectura;<br /> timeToStart de doble de atributos de sólo lectura;<br /> timeToFail, doble de atributos de sólo lectura;<br /> atributo de sólo lectura int totalSecondsPlayed;<br /> atributo de sólo lectura int totalSecondsSpent;<br /> frameRate, doble de atributos de sólo lectura;<br /> atributo de sólo lectura int droppedFrameCount;<br /> atributo de sólo lectura int seenBandwidth;<br /> atributo de solo lectura en la velocidad de bits;<br /> doble bufferTime de atributos de sólo lectura;<br /> atributo de sólo lectura int bufferLength;<br /> atributo de sólo lectura int emptyBufferCount;<br /> doble de almacenamiento en búfer de atributos de sólo lectura;<br /> };</p> </td> 
   <td><p>interface PlaybackInformation<br /> {<br /> readonly attribute timeToFirstByte;<br /> timeToLoad del doble de atributos de sólo lectura;<br /> timeToStart de doble de atributos de sólo lectura;<br /> timeToFail, doble de atributos de sólo lectura;<br /> atributo de sólo lectura int totalSecondsPlayed;<br /> atributo de sólo lectura int totalSecondsSpent;<br /> frameRate, doble de atributos de sólo lectura;<br /> atributo de sólo lectura int droppedFrameCount;<br /> <br /> atributo de solo lectura en la velocidad de bits;<br /> doble bufferTime de atributos de sólo lectura;<br /> atributo de sólo lectura int bufferLength;<br /> atributo de sólo lectura int emptyBufferCount;<br /> doble de almacenamiento en búfer de atributos de sólo lectura;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en la página de información y asistencia [de](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.
