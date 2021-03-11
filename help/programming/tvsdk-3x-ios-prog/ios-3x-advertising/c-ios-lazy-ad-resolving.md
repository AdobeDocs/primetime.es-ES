---
description: La resolución de anuncios y la carga de anuncios pueden causar un retraso inaceptable para un usuario que espera a que se inicie la reproducción. La función de resolución de carga de publicidad diferida puede reducir este retraso del inicio. Los anuncios ahora se pueden resolver en un intervalo especificado antes de la posición de la pausa publicitaria. Esto se logra mediante el uso de un enfoque de doble reproductor.
title: Resolución de anuncios justo a tiempo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---


# Resolución de anuncios en el momento {#just-in-time-ad-resolving}

La resolución de anuncios y la carga de anuncios pueden causar un retraso inaceptable para un usuario que espera a que se inicie la reproducción. La función de resolución de carga de publicidad diferida puede reducir este retraso del inicio. Los anuncios ahora se pueden resolver en un intervalo especificado antes de la posición de la pausa publicitaria. Esto se logra mediante el uso de un enfoque de doble reproductor.

**Proceso básico de resolución y carga de anuncios:**

1. TVSDK descarga un manifiesto (lista de reproducción) y *resuelve* todos los anuncios.
1. TVSDK *carga* todos los anuncios y une los segmentos de anuncio en los manifiestos.
1. TVSDK mueve el reproductor al estado PREPARADO y comienza la reproducción del contenido.

El reproductor utiliza las URL del manifiesto para obtener el contenido de la publicidad (creativos), garantiza que el contenido de la publicidad tenga un formato que TVSDK pueda reproducir y TVSDK coloca los anuncios en la cronología. Este proceso básico de resolución y carga de anuncios puede causar un retraso inaceptablemente largo para un usuario que espera reproducir su contenido, especialmente si el manifiesto contiene varias direcciones URL de anuncios.

**Resolución de publicidad diferida:**

1. TVSDK descarga la lista de reproducción.
1. TVSDK *resuelve y carga* cualquier anuncio previo a la emisión, mueve el reproductor al estado PREPARADO y comienza la reproducción del contenido.
1. TVSDK *resuelve* cada pausa publicitaria antes de su posición de basándose en el valor definido en `PTAdMetadata::delayAdLoadingTolerance`.

Por ejemplo, de forma predeterminada `delayAdLoadingTolerance` se establece en 5 segundos. Si un AdBreak está configurado para reproducirse a las 3:00, se resolverá a las 2:55:00. Puede que desee aumentar este valor si cree que la resolución de la publicidad tardará más de 5 segundos.

>[!IMPORTANT]
>
>**Factores a tener en cuenta con la resolución de publicidad diferida:**
>* La resolución de publicidad diferida solo es compatible con flujos de VOD con los modos SERVER_MAP y modo de señalización.
>* La resolución de publicidad diferida no está habilitada de forma predeterminada. Debe establecer `PTAdMetadata::delayAdLoading` = YES para habilitarlo.
>* La resolución de publicidad diferida es incompatible con la función Instant On. Para obtener más información sobre la activación instantánea, consulte [Instant On](../../tvsdk-3x-ios-prog/ios-3x-instant-on-ios.md).
>* El modo Imagen en imagen no es compatible con la resolución de publicidad diferida. Desactive los modos Imagen en imagen si activa la resolución de publicidad diferida.
>* La resolución de anuncios diferidos no afecta a los anuncios previos a la emisión.

>


**Habilitar la resolución de anuncios diferidos**

Puede habilitar o deshabilitar la función de resolución de publicidad diferida mediante el mecanismo de carga de publicidad diferida existente (la resolución de publicidad diferida está deshabilitada de forma predeterminada).

Puede habilitar la resolución de publicidad diferida configurando `PTAdMetadata::delayAdLoading`= YES al configurar los metadatos de publicidad.

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
