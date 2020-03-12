---
description: La resolución y carga de anuncios puede provocar un retraso inaceptable para un usuario que espera que se inicie la reproducción. La función de resolución de carga de publicidad diferida puede reducir este retraso de inicio. Las publicidades ahora se pueden resolver en un intervalo especificado antes de la posición de la pausa publicitaria. Esto se logra utilizando un enfoque de doble reproductor.
seo-description: La resolución y carga de anuncios puede provocar un retraso inaceptable para un usuario que espera que se inicie la reproducción. La función de resolución de carga de publicidad diferida puede reducir este retraso de inicio. Las publicidades ahora se pueden resolver en un intervalo especificado antes de la posición de la pausa publicitaria. Esto se logra utilizando un enfoque de doble reproductor.
seo-title: Resolución de anuncios justo a tiempo
title: Resolución de anuncios justo a tiempo
uuid: f7b20439-3604-4d69-bdfe-2e0ad26f495b
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Resolución de anuncios justo a tiempo {#just-in-time-ad-resolving}

La resolución y carga de anuncios puede provocar un retraso inaceptable para un usuario que espera que se inicie la reproducción. La función de resolución de carga de publicidad diferida puede reducir este retraso de inicio. Las publicidades ahora se pueden resolver en un intervalo especificado antes de la posición de la pausa publicitaria. Esto se logra utilizando un enfoque de doble reproductor.

**Proceso básico de resolución y carga de anuncios:**

1. TVSDK descarga un manifiesto (lista de reproducción) y *resuelve* todas las publicidades.
1. TVSDK *carga* todas las publicidades y vincula los segmentos de publicidad a los manifiestos.
1. TVSDK mueve el reproductor al estado PREPARADO y comienza la reproducción del contenido.

El reproductor utiliza las direcciones URL del manifiesto para obtener el contenido de la publicidad (elementos creativos), garantiza que el contenido de la publicidad tenga un formato que TVSDK pueda reproducir y TVSDK coloca las publicidades en la línea de tiempo. Este proceso básico de resolución y carga de publicidades puede provocar un retraso inaceptablemente prolongado para un usuario que espera reproducir su contenido, especialmente si el manifiesto contiene varias direcciones URL de publicidad.

**Resolución de publicidad diferida:**

1. TVSDK descarga la lista de reproducción.
1. TVSDK *resuelve y carga* cualquier anuncio previo, mueve el reproductor al estado PREPARADO y comienza la reproducción del contenido.
1. TVSDK *resuelve* cada pausa publicitaria antes de su posición en función del valor definido en `PTAdMetadata::delayAdLoadingTolerance`.

Por ejemplo, de forma predeterminada `delayAdLoadingTolerance` se establece en 5 segundos. Si un AdBreak está configurado para reproducirse a las 3:00, se resolverá a las 2:55:00. Es posible que desee aumentar este valor si cree que la resolución de la publicidad tardará más de 5 segundos.

>[!IMPORTANT]
>
>**Factores a tener en cuenta con la resolución de publicidad diferida:**
>* La resolución diferida de publicidad solo se admite para flujos VOD con modos SERVER_MAP y modo de señalización.
>* La resolución de publicidad diferida no está habilitada de forma predeterminada. Debe establecer `PTAdMetadata::delayAdLoading` = YES para habilitarlo.
>* La resolución diferida de publicidad no es compatible con la función Activar instantáneamente. Para obtener más información sobre la activación instantánea, consulte Activado [instantáneo](../../tvsdk-3x-ios-prog/ios-3x-instant-on-ios.md).
>* El modo Imagen en imagen no es compatible con la resolución de publicidad diferida. Desactive los modos de imagen en imagen si activa la resolución de publicidad diferida.
>* La resolución diferida de los anuncios no afecta a los anuncios anteriores.
>


**Habilitar la resolución diferida de publicidad**

Puede habilitar o deshabilitar la función de resolución de publicidad diferida mediante el mecanismo de carga de publicidad diferida existente (la resolución de publicidad diferida está deshabilitada de forma predeterminada).

Puede habilitar la resolución de publicidad diferida configurando `PTAdMetadata::delayAdLoading`= YES al configurar los metadatos de la publicidad.

**API relevantes para la resolución de publicidad diferida:**

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
