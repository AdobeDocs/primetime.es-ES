---
description: La resolución de anuncios y la carga de anuncios pueden provocar un retraso inaceptable para un usuario que espera a que se inicie la reproducción. La función de resolución de carga diferida de publicidad puede reducir este retraso en el inicio. Los anuncios ahora se pueden resolver en un intervalo especificado antes de la posición de la pausa publicitaria. Esto se logra utilizando un enfoque de doble reproductor.
title: Resolución de anuncios Just-In-Time
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# Resolución de anuncios Just-In-Time {#just-in-time-ad-resolving}

La resolución de anuncios y la carga de anuncios pueden provocar un retraso inaceptable para un usuario que espera a que se inicie la reproducción. La función de resolución de carga diferida de publicidad puede reducir este retraso en el inicio. Los anuncios ahora se pueden resolver en un intervalo especificado antes de la posición de la pausa publicitaria. Esto se logra utilizando un enfoque de doble reproductor.

**Proceso básico de resolución y carga de anuncios:**

1. TVSDK descarga un manifiesto (lista de reproducción) y *resuelve* todos los anuncios.
1. TVSDK *cargas* todos los anuncios y vincula los segmentos de anuncio en los manifiestos.
1. TVSDK mueve el reproductor al estado PREPARADO y comienza la reproducción del contenido.

El reproductor utiliza las direcciones URL del manifiesto para obtener el contenido del anuncio (creativos), garantiza que el contenido del anuncio esté en un formato que TVSDK pueda reproducir y TVSDK coloca los anuncios en la cronología. Este proceso básico de resolución y carga de anuncios puede causar un retraso inaceptablemente largo a un usuario que espera para reproducir su contenido, especialmente si el manifiesto contiene varias direcciones URL de publicidad.

**Resolución de publicidad diferida:**

1. TVSDK descarga la lista de reproducción.
1. TVSDK *resuelve y carga* cualquier anuncio previo a la emisión, mueve el reproductor al estado PREPARADO y comienza la reproducción del contenido.
1. TVSDK *resuelve* cada anuncio se divide antes de su posición en función del valor definido en `PTAdMetadata::delayAdLoadingTolerance`.

Por ejemplo, de forma predeterminada `delayAdLoadingTolerance` se establece en 5 segundos. Si un AdBreak está configurado para reproducirse a las 3:00, se resolverá a las 2:55:00. Puede que desee aumentar este valor si cree que la resolución del anuncio tardará más de 5 segundos.

>[!IMPORTANT]
>
>**Factores a considerar con la resolución de anuncios diferidos:**
>* La resolución de anuncios diferidos solo se admite para flujos de VOD con los modos SERVER_MAP y modo de señalización.
>* La resolución de anuncios diferidos no está activada de forma predeterminada. Debe configurar `PTAdMetadata::delayAdLoading` = SÍ para habilitarlo.
>* La resolución de anuncios diferida no es compatible con la función Encendido instantáneo. Para obtener más información acerca de Instant On, consulte [Instant On](../../tvsdk-3x-ios-prog/ios-3x-instant-on-ios.md).
>* El modo Imagen en imagen no es compatible con la resolución de anuncios diferidos. Desactive los modos de imagen en imagen si activa la resolución de anuncios diferidos.
>* La resolución diferida de los anuncios no afecta a los anuncios previos a la emisión.
>
**Habilitar la resolución de anuncios diferidos**

Puede activar o desactivar la función de resolución de anuncios diferidos mediante el mecanismo de carga de anuncios diferidos existente (la resolución de anuncios diferidos está desactivada de forma predeterminada).

Puede habilitar la resolución de anuncios diferidos estableciendo lo siguiente `PTAdMetadata::delayAdLoading`= SÍ al configurar los metadatos de la publicidad.

**API relevantes para la resolución de anuncios diferidos:**

```
Class:    PTAdMetadata 
Properties: 
  
/** 
 * Property to define whether ad break resolution must be delayed until after stream start or not. 
 * When this value is NO, ads are resolved before stream start and spliced into the content when possible allowing  
   for a seamless playback experience. 
 * When this value is YES, ads are displayed in a secondary video player instance and resolved lazily only when  
   needed. 
 * Default value is NO 
 */ 
@property (nonatomic, assign) BOOL delayAdLoading; 
  
/** 
 * Property to define the lookahead for ad break resolution.  Ad breaks will be resolved when they occur between  
   the playhead time and the specified tolerance. 
 * If set to zero, the ad will be resolved immediately before playing the ad.  This may cause a slight delay in the  
   playback of the ads. 
 * Default value is 5.0 or 5 seconds. 
 */ 
  
@property (nonatomic, assign) NSTimeInterval delayAdLoadingTolerance;
```
