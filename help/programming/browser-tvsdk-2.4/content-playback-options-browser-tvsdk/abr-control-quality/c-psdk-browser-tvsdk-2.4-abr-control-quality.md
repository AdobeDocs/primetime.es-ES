---
description: Los flujos HLS y DASH proporcionan diferentes codificaciones de velocidad de bits (perfiles) para el mismo breve estallido de vídeo. El TVSDK del explorador puede seleccionar el nivel de calidad para cada ráfaga en función del ancho de banda disponible.
title: Velocidad de bits adaptable (ABR) para la calidad de vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 1%

---


# Información general {#adaptive-bit-rates-abr-for-video-quality-overview}

Los flujos HLS y DASH proporcionan diferentes codificaciones de velocidad de bits (perfiles) para el mismo breve estallido de vídeo. El TVSDK del explorador puede seleccionar el nivel de calidad para cada ráfaga en función del ancho de banda disponible.

El SDK de explorador supervisa constantemente la velocidad de bits para garantizar que el contenido se reproduce a la velocidad de bits óptima para la conexión de red actual.

Puede establecer la directiva de conmutación de velocidad de bits adaptable (ABR) y las tasas de bits inicial, mínima y máxima para un flujo de velocidad de bits múltiple (MBR). El TVSDK del explorador cambia automáticamente a la velocidad de bits que proporciona la mejor experiencia de reproducción en la configuración especificada.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Tasa de bits inicial </td> 
   <td colname="col2">Velocidad de bits de reproducción deseada (en bits por segundo) para el primer segmento. Cuando se inicia la reproducción, se utiliza el perfil más cercano, que es igual o bueno que la velocidad de bits inicial, para el primer segmento. <p> Si se define una velocidad de bits mínima y la velocidad de bits inicial es inferior a la tasa mínima, el SDK de explorador selecciona el perfil con la tasa de bits más baja por encima de la tasa de bits mínima. Si la tasa inicial es superior a la tasa máxima, el SDK de explorador selecciona la tasa más alta por debajo de la tasa máxima. </p> <p>Si la velocidad de bits inicial es cero o indefinida, la velocidad de bits inicial viene determinada por la directiva ABR. </p> <p><span class="codeph"> </span> initialBitTrack devuelve un valor entero que representa el perfil byte por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Tasa de bits mínima </td> 
   <td colname="col2">La velocidad de bits más baja permitida a la que puede cambiar el ABR. El cambio de ABR ignora los perfiles con una velocidad de bits inferior a esta velocidad de bits. <p><span class="codeph"> </span> minBitTrack devuelve un valor entero que representa el perfil de bits por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocidad de bits máxima </td> 
   <td colname="col2">La velocidad de bits máxima permitida a la que el ABR puede cambiar. El cambio de ABR ignora los perfiles con una velocidad de bits superior a esta velocidad de bits. <p><span class="codeph"> </span> maxBitRaterDevuelve un valor entero que representa el perfil de bits por segundo. </p> </td> 
  </tr> 
 </tbody> 
</table>

Tenga en cuenta la siguiente información:

* Cuando cambia la velocidad de bits, el SDK de TVSDK del explorador envía `AdobePSDK.ProfileEvent` con el tipo `AdobePSDK.PSDKEventType.PROFILE_CHANGED`.

* Puede cambiar la configuración de ABR en cualquier momento y el reproductor cambia para utilizar el perfil que coincida más con la configuración más reciente.

Por ejemplo, si un flujo tiene los siguientes perfiles:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 400000

Si especifica un intervalo de 300000 a 2000000, el SDK de explorador solo tendrá en cuenta los perfiles 1, 2 y 3. Esto permite que las aplicaciones se ajusten a diversas condiciones de red, como el cambio de wi-fi a 3G o a varios dispositivos, como un teléfono, una tableta o un equipo de escritorio.

Para establecer los parámetros de control ABR:

* Establezca los parámetros en la clase `ABRControlParameters`.

