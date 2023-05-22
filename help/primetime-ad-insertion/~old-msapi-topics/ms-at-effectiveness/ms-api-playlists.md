---
description: El servidor de manifiesto devuelve listas de reproducción maestras en formato M3U8, que se ajustan al estándar de flujo en directo HTTP propuesto. Consiste en un conjunto de flujos de transporte de variante (TS), cada uno de los cuales contiene representaciones del mismo contenido para diferentes velocidades de bits y formatos. La inserción de anuncios de Adobe Primetime agrega la etiqueta de directiva EXT-X-MARKER, que deben interpretar los reproductores de vídeo del cliente.
title: DIRECTIVA EXT-X-MARKER
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---


# DIRECTIVA EXT-X-MARKER {#ext-x-marker-directive}

El servidor de manifiesto devuelve listas de reproducción maestras en formato M3U8, que se ajustan al estándar de flujo en directo HTTP propuesto. Consiste en un conjunto de flujos de transporte de variante (TS), cada uno de los cuales contiene representaciones del mismo contenido para diferentes velocidades de bits y formatos. La inserción de anuncios de Adobe Primetime agrega la etiqueta de directiva EXT-X-MARKER, que deben interpretar los reproductores de vídeo del cliente.

Para obtener más información sobre la etiqueta EXT-X-MARKER, consulte [Perfil de streaming en directo HTTP de Adobe Primetime](https://wwwimages2.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeHLS_April2014.pdf).

>[!NOTE]
>
>Esta funcionalidad sólo está disponible si la dirección URL del servidor de manifiesto de arranque no contiene el `pttrackingmode` parámetro.

>[!NOTE]
>
>La etiqueta EXT-X-MARKER se añade a los segmentos de publicidad y no a los de contenido.

El borrador de la norma en [HTTP Live Streaming](https://tools.ietf.org/html/draft-pantos-http-live-streaming-23) describe el contenido y el formato de las listas de reproducción de variante. La etiqueta EXT-X-MARKER indica al cliente que invoque una llamada de retorno. Contiene los siguientes componentes:

* **ID** Identificador único (cadena) de este evento de llamada de retorno en el contexto del flujo de programa.

* **TIPO** Tipo (cadena) del evento de llamada de retorno: PodBegin, PodEnd, PrerollPodBegin, PrerollPodEnd o AdBegin

* **DURACIÓN** Tiempo (en segundos) desde el inicio del segmento que lleva la etiqueta durante el cual la directiva sigue siendo válida.

* **OFFSET** Opcional. El desplazamiento (en segundos) en relación con el principio de la reproducción del segmento, cuando se debe invocar la llamada de retorno.

   * `PodBegin` y `PrerollPodBegin` contienen información de señalización en el atributo DATA y se activan al principio del segmento. Por lo tanto, `OFFSET` La etiqueta de no está disponible aquí.

   * `AdBegin` contiene información de señalización en el atributo de DATOS y las etiquetas de impresión se activan al principio de ese segmento. Por lo tanto, `OFFSET` La etiqueta de tampoco está disponible aquí.

   * `PodEnd` y `PrerollPodEnd` contienen información de señalización en el atributo DATA, pero se activan al final del segmento actual porque se espera que estas etiquetas se activen al final del último segmento del último anuncio de la secuencia. En este caso, `OFFSET` se establece en `<duration of segment>` para especificar que la señalización se active al final del segmento actual.

* **DATOS** Cadena codificada en Base64 entre comillas dobles que contiene los datos que se van a pasar a la aplicación al invocar la devolución de llamada. Contiene información de seguimiento de anuncios que cumple las especificaciones de VMAP1.0 y VAST3.0.

* **RECUENTO** Número de anuncios que se vincularán en la pausa publicitaria.

   Solo es aplicable si el componente TYPE está establecido en PodBegin o PreRollPodBegin.

* **RUPTURA** Duración total (en segundos) de la pausa publicitaria rellenada.

   Solo es aplicable si el componente TYPE está establecido en PodBegin o PreRollPodBegin.

Al construir la llamada de retorno, interprete los componentes EXT-X-MARKER de la siguiente manera:

* Cuando la etiqueta contenga `OFFSET`, active la llamada de retorno en el desplazamiento especificado en relación con el principio de la reproducción del contenido en ese segmento. De lo contrario, activa la llamada de retorno en cuanto el contenido de ese segmento comience a reproducirse.
* Uso `DURATION` para realizar un seguimiento del progreso del contenido del anuncio y solicitar direcciones URL para el seguimiento de eventos.
* Aprobado `ID`, `TYPE`, y `DATA` a la llamada de retorno.

Utilice el `PrerollPodBegin`, y `PrerollPodEnd` valores para `TYPE` para decidir qué segmento TS se reproducirá primero en emisiones en directo/lineales.

>[!NOTE]
>
>El `PrerollPodBegin`, y `PrerollPodEnd` Estos valores solo están disponibles cuando se inserta un anuncio previo a la emisión en una emisión en directo.

El servidor de manifiestos incluye etiquetas EXT-X-MARKER en los siguientes segmentos:

* El primer segmento de la pausa publicitaria, para rastrear el principio de un pod de anuncios.
* El primer segmento del anuncio, para realizar un seguimiento del inicio, la finalización o el progreso de un anuncio individual dentro de un pod de anuncios.
* El último segmento de la pausa publicitaria, para rastrear el final de un pod de anuncios.

El servidor de manifiesto envía un `VMAP1.0-conformant` Documento XML para realizar un seguimiento del inicio y el final de cada pausa publicitaria. Es una versión filtrada de la respuesta VMAP1.0 real devuelta por el servidor de publicidad y contiene principalmente los eventos de seguimiento como se muestra a continuación:

```xml
<?xml version="1.0"?> 
<AdTrackingFragments> 
<AdTrackingFragment> 
<vmap:VMAP xmlns:vmap="https://www.iab.net/vmap-1.0" version="1.0"> 
    <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start"> 
        <vmap:TrackingEvents> 
            <vmap:Tracking event="breakStart"> 
                https://MyServer.com/breakstart.gif 
            </vmap:Tracking> 
            <vmap:Tracking event="breakEnd"> 
                https://MyServer.com/breakend.gif 
            </vmap:Tracking> 
            <vmap:Tracking event="error"> 
                https://MyServer.com/error.gif 
            </vmap:Tracking> 
        </vmap:TrackingEvents> 
    </vmap:AdBreak> 
</vmap:VMAP> 
</AdTrackingFragment> 
</AdTrackingFragments>
```

Para cada creatividad publicitaria que el servidor de manifiesto inserta en el contenido del programa, envía un documento XML compatible con VAST3.0 para realizar el seguimiento de dicha publicidad. Cada documento XML contiene un `<InLine>` elemento que describe el anuncio lineal insertado o un `<Wrapper>` en el caso de los anuncios envolventes (es decir, anuncios vinculados o redirigidos) y cualquier anuncio complementario y extensión asociados. Si la respuesta VAST contiene un atributo de secuencia, como cuando el anuncio forma parte de un pod de anuncios, el documento incluye ese atributo. A continuación se muestra un ejemplo de un documento XML compatible con VAST3.0 para realizar el seguimiento de un anuncio individual:

```xml
<?xml version="1.0"?> 
<AdTrackingFragments> 
<AdTrackingFragment> 
<VAST xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"  
      version="3.0"  
      xsi:noNamespaceSchemaLocation="https://service.videoplaza.com/schema/iab/vast-3.0.xsd"> 
<Ad id="903395"> 
    <InLine> 
      <AdSystem version="1.0">Auditude</AdSystem> 
      <AdTitle/> 
      <Error>https://ad.qa.auditude.com/adserver/?ErrAd1=[ERRORCODE]</Error> 
      <Impression id="urn:aeid:903395">https://ad.qa.auditude.com/adserver/e?type=adimp&amp; 
                 cid=127860991&amp; 
                 z=50183&amp; 
                 a=903395&amp; 
                 s=ef8c51dc&amp; 
                 t=1355309735&amp; 
                 w=100000&amp; 
                 uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                 l=1355280906&amp; 
                 u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                 br=1&amp; 
                 sq=1&amp; 
                 pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                 ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                               ?Cashcash=[CACHEBUSTING] 
                               ?Asset=[ASSETURI] 
      </Impression> 
      <Creatives> 
        <Creative> 
          <Linear> 
            <Duration>00:00:15</Duration> 
            <TrackingEvents> 
              ... 
              <Tracking event="firstQuartile"> 
                https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS&amp; 
                  a=903395&amp; 
                  a1=105&amp; 
                  ref=urn:asset:903395:105&amp; 
                  unit=percent&amp; 
                  progress=25&amp; 
                  cid=127860991&amp; 
                  z=50183&amp; 
                  a=903395&amp; 
                  s=ef8c51dc&amp; 
                  t=1355309735&amp; 
                  w=100000&amp; 
                  uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                  l=1355280906&amp; 
                  u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                  br=1&amp; 
                  sq=1&amp; 
                  pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                  ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                                ?Cashcash=[CACHEBUSTING] 
                                ?Asset=[ASSETURI] 
              </Tracking>                
              <Tracking event="midpoint"> 
                https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS&amp; 
                  a=903395&amp; 
                  a1=105&amp; 
                  ref=urn:asset:903395:105&amp; 
                  unit=percent&amp; 
                  progress=50&amp; 
                  cid=127860991&amp; 
                  z=50183&amp; 
                  a=903395&amp; 
                  s=ef8c51dc&amp; 
                  t=1355309735&amp; 
                  w=100000&amp; 
                  uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                  l=1355280906&amp; 
                  u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                  br=1&amp; 
                  sq=1&amp; 
                  pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                  ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                                ?Cashcash=[CACHEBUSTING] 
                                ?Asset=[ASSETURI] 
              </Tracking> 
              <Tracking event="firstQuartile"> 
                https://www.Tweeeen.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                       ?Cashcash=[CACHEBUSTING] 
                                       ?Asset=[ASSETURI] 
              </Tracking> 
              <Tracking event="midpoint"> 
                https://www.Fiftyyyy.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                        ?Cashcash=[CACHEBUSTING] 
                                        ?Asset=[ASSETURI] 
              </Tracking> 
              ... 
            </TrackingEvents> 
            <VideoClicks> 
              <ClickTracking> 
                https://www.MP4-Vid-ClickTrack.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                                  ?Cashcash=[CACHEBUSTING] 
                                                  ?Asset=[ASSETURI] 
              </ClickTracking> 
              <ClickThrough> 
                https://www.cnn.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                   ?Cashcash=[CACHEBUSTING] 
                                   ?Asset=[ASSETURI] 
              </ClickThrough> 
              ... 
            </VideoClicks> 
            <AdParameters>campaign_id=7012</AdParameters> 
            <MediaFiles> 
              ...            
            </MediaFiles> 
          </Linear> 
        </Creative> 
        <Creative> 
          <CompanionAds> 
            <Companion id="103" width="300" height="250"> 
              <StaticResource creativeType="image/jpeg"> 
                https://ad.qa.auditude.com/adserver/c/z=50183; 
                  l=1355280906; 
                  u=956c3cd141086a1da44dcae8ea4ed14a; 
                  uid=_CxLm0b1SeKD8KXco__5TQ; 
                  cid=127860991; 
                  s=ef8c51dc; 
                  t=1355309735; 
                  br=1; 
                  sq=1; 
                  pod=id%3a1%2cctype%3al%2cptype%3ap%2cdur 
                    %3a400%2clot%3a8%2ccpos%3a1%2cedur%3a400%2celot%3a8; 
                  ax=0%2c0%2c1720%2c0; 
                  w=100000; 
                  a=903395; 
                  a1=103/c300x250.jpeg 
              </StaticResource> 
              <CompanionClickThrough> 
                https://ad.qa.auditude.com/adserver/l/a=903395%3Ba1=103 
                  %3Ba2=1%3Bz=50183%3Bl=1355280906%3Bu=956c3cd141086a1da44dcae8ea4ed14a 
                  %3Bcid=127860991%3Bs=ef8c51dc%3Buid=_CxLm0b1SeKD8KXco__5TQ 
                  %3Bt=1355309735%3Bbr=1%3Bsq=1%3Bpod=id%3a1%2cctype%3al%2cptype 
                  %3ap%2cdur%3a400%2clot%3a8%2ccpos%3a1%2cedur%3a400%2celot%3a8 
                  %3Bax=0%2c0%2c1720%2c0 
              </CompanionClickThrough> 
              <AdParameters>campaign_id=7012</AdParameters> 
            </Companion> 
          </CompanionAds> 
        </Creative> 
        ... 
      </Creatives> 
      <Extensions> 
        <Extension type="Behavior"> 
          ... 
        </Extension> 
      </Extensions> 
    </InLine> 
  </Ad> 
  </VAST> 
</AdTrackingFragment> 
</AdTrackingFragments> 
```
