---
description: El servidor de manifiesto devuelve listas de reproducción maestras en formato M3U8, de acuerdo con el estándar HTTP Live Streaming propuesto. Consiste en un conjunto de flujos de transporte variantes (TSs), cada uno con representaciones del mismo contenido para diferentes velocidades de bits y formatos. La inserción de anuncios de Adobe Primetime añade la etiqueta de directiva EXT-X-MARKER, que deben interpretar los reproductores de vídeo del cliente.
title: Directiva EXT-X-MARKER
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---


# Directiva EXT-X-MARKER {#ext-x-marker-directive}

El servidor de manifiesto devuelve listas de reproducción maestras en formato M3U8, de acuerdo con el estándar HTTP Live Streaming propuesto. Consiste en un conjunto de flujos de transporte variantes (TSs), cada uno con representaciones del mismo contenido para diferentes velocidades de bits y formatos. La inserción de anuncios de Adobe Primetime añade la etiqueta de directiva EXT-X-MARKER, que deben interpretar los reproductores de vídeo del cliente.

Para obtener más información sobre la etiqueta EXT-X-MARKER, consulte [Adobe Primetime HTTP Live Streaming Profile](https://wwwimages2.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeHLS_April2014.pdf).

>[!NOTE]
>
>Esta funcionalidad solo está disponible si la URL del servidor de manifiesto de arranque no contiene el parámetro `pttrackingmode`.

>[!NOTE]
>
>La etiqueta EXT-X-MARKER se agrega a los segmentos de anuncios y no a los segmentos de contenido.

El borrador estándar en [HTTP Live Streaming](https://tools.ietf.org/html/draft-pantos-http-live-streaming-23) describe el contenido y el formato de las listas de reproducción de variantes. La etiqueta EXT-X-MARKER indica al cliente que invoque una llamada de retorno. Contiene los siguientes componentes:

* **** Identificador IDUnique (cadena) para este evento de llamada de retorno en el contexto del flujo del programa.

* **** TYPEType (cadena) del evento de llamada de retorno: PodBegin, PodEnd, PrerollPodBegin, PrerollPodEnd o AdBegin

* **** DURACIÓNLongitud de tiempo (en segundos) desde el inicio del segmento con la etiqueta para la que la directiva sigue siendo válida.

* **** OFFSETOopcional. El desplazamiento (en segundos) relativo al principio de la reproducción del segmento, cuando se debe invocar la rellamada.

   * `PodBegin` y  `PrerollPodBegin` contienen información de señalización en el atributo DATA y se activan al principio del segmento. Por lo tanto, la etiqueta `OFFSET` no está disponible aquí.

   * `AdBegin` contiene información de señalización en el atributo DATA y las etiquetas de impresión se activan al principio de ese segmento. Por lo tanto, la etiqueta `OFFSET` tampoco está disponible aquí.

   * `PodEnd` y  `PrerollPodEnd` contienen información de señalización en el atributo DATA , pero se activan al final del segmento actual porque se espera que estas etiquetas se activen al final del último segmento del último anuncio del pod. En este caso, `OFFSET` se establece en `<duration of segment>` para especificar que la señalización se active al final del segmento actual.

* **** Cadena con codificación DATABase64 entre comillas dobles que contienen los datos que se pasarán a la aplicación al invocar la rellamada. Contiene información de seguimiento de anuncios que se ajusta a las especificaciones VMAP1.0 y VAST3.0.

* **** Número de anuncios que se vincularán en la pausa publicitaria.

   Solo aplicable si el componente TIPO está establecido en PodBegin o PrerollPodBegin.

* **** DESGLOSEduración total (en segundos) de la pausa publicitaria rellenada.

   Solo aplicable si el componente TIPO está establecido en PodBegin o PrerollPodBegin.

Al construir la rellamada, interprete los componentes EXT-X-MARKER de la siguiente manera:

* Cuando la etiqueta contenga `OFFSET`, active la rellamada con el desplazamiento especificado en relación con el comienzo de la reproducción del contenido en ese segmento. De lo contrario, se activa la rellamada en cuanto comienza a reproducirse el contenido de ese segmento.
* Utilice `DURATION` para rastrear el progreso del contenido de la publicidad y para solicitar direcciones URL para rastrear eventos.
* Pase `ID`, `TYPE` y `DATA` a la rellamada.

Utilice los valores `PrerollPodBegin` y `PrerollPodEnd` para `TYPE` para decidir qué segmento de TS se reproducirá primero en los flujos en directo/lineales.

>[!NOTE]
>
>Los valores `PrerollPodBegin` y `PrerollPodEnd` solo están disponibles cuando se inserta un anuncio pre-roll en un flujo en vivo.

El servidor de manifiestos incluye etiquetas EXT-X-MARKER en los siguientes segmentos:

* El primer segmento de la pausa publicitaria, para rastrear el comienzo de un pod de anuncios.
* El primer segmento del anuncio, para rastrear el inicio/finalización/progreso de un anuncio individual dentro de un pod de anuncios.
* El último segmento de la pausa publicitaria, para rastrear el final de un pod de anuncios.

El servidor de manifiestos envía un documento XML `VMAP1.0-conformant` para realizar un seguimiento del inicio y el final de cada pausa publicitaria. Es una versión filtrada de la respuesta VMAP1.0 real devuelta por el servidor de publicidad y contiene principalmente los eventos de seguimiento como se muestra aquí:

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

Para cada creador de publicidad que el servidor de manifiesto inserta en el contenido del programa, envía un documento XML compatible con VAST3.0 para rastrear ese anuncio. Cada documento XML contiene un elemento `<InLine>` que describe el elemento creativo de publicidad lineal insertado, o un elemento `<Wrapper>` en el caso de los anuncios envolventes (es decir, los anuncios vinculados o redirigidos) y cualquier publicidad y extensión asociada. Si la respuesta VAST contiene un atributo de secuencia, como cuando el anuncio forma parte de un pod de anuncios, el documento incluye ese atributo. El siguiente es un documento XML de muestra conforme con VAST3.0 para rastrear un anuncio individual:

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
