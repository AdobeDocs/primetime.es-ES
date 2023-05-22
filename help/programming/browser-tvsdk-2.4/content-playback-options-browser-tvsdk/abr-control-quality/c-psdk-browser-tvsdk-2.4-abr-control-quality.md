---
description: Los flujos HLS y DASH proporcionan diferentes codificaciones (perfiles) de velocidad de bits para la misma ráfaga corta de vídeo. TVSDK del navegador puede seleccionar el nivel de calidad para cada ráfaga en función del ancho de banda disponible.
title: Velocidad de bits adaptable (ABR) para la calidad de vídeo
exl-id: 2506a57b-d77d-4bd1-9e4c-5e00ef1bc8b7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 1%

---

# Información general {#adaptive-bit-rates-abr-for-video-quality-overview}

Los flujos HLS y DASH proporcionan diferentes codificaciones (perfiles) de velocidad de bits para la misma ráfaga corta de vídeo. TVSDK del navegador puede seleccionar el nivel de calidad para cada ráfaga en función del ancho de banda disponible.

TVSDK del explorador monitoriza constantemente la velocidad de bits para garantizar que el contenido se reproduce a la velocidad de bits óptima para la conexión de red actual.

Puede establecer la directiva de conmutación de velocidad de bits adaptable (ABR) y las tasas de bits inicial, mínima y máxima para un flujo de velocidad de bits múltiple (MBR). TVSDK del explorador cambia automáticamente a la velocidad de bits que proporciona la mejor experiencia de reproducción en la configuración especificada.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Velocidad de bits inicial </td> 
   <td colname="col2">La velocidad de bits de reproducción deseada (en bits por segundo) para el primer segmento. Cuando comienza la reproducción, se utiliza el perfil más cercano, que es igual o bueno que la velocidad de bits inicial, para el primer segmento. <p> Si se define una velocidad de bits mínima y la velocidad de bits inicial es inferior a la velocidad mínima, Browser TVSDK selecciona el perfil con la velocidad de bits más baja por encima de la velocidad de bits mínima. Si la tasa inicial está por encima de la tasa máxima, Browser TVSDK selecciona la tasa más alta por debajo de la tasa máxima. </p> <p>Si la velocidad de bits inicial es cero o indefinida, la velocidad de bits inicial viene determinada por la directiva ABR. </p> <p><span class="codeph"> initialBitRate</span> devuelve un valor entero que representa el perfil de byte por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocidad de bits mínima </td> 
   <td colname="col2">La velocidad de bits más baja permitida a la que ABR puede cambiar. La conmutación ABR ignora los perfiles con una velocidad de bits inferior a esta velocidad de bits. <p><span class="codeph"> minBitRate</span> devuelve un valor entero que representa el perfil de bits por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocidad de bits máxima </td> 
   <td colname="col2">La velocidad de bits más alta permitida a la que ABR puede cambiar. La conmutación ABR ignora los perfiles con una velocidad de bits superior a esta velocidad de bits. <p><span class="codeph"> maxBitRate</span> devuelve un valor entero que representa el perfil de bits por segundo. </p> </td> 
  </tr> 
 </tbody> 
</table>

Tenga en cuenta lo siguiente:

* Cuando la velocidad de bits cambia, el TVSDK del explorador se envía `AdobePSDK.ProfileEvent` con el tipo como `AdobePSDK.PSDKEventType.PROFILE_CHANGED`.

* Puede cambiar la configuración de ABR en cualquier momento, y el reproductor cambia para utilizar el perfil que más coincida con la configuración más reciente.

Por ejemplo, si una secuencia tiene los siguientes perfiles:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Si especifica un intervalo de 300000 para 2000000, el TVSDK del explorador solo tiene en cuenta los perfiles 1, 2 y 3. Esto permite que las aplicaciones se ajusten a diversas condiciones de la red, como cambiar de wi-fi a 3G o a varios dispositivos, como un teléfono, una tableta o un equipo de escritorio.

Para definir los parámetros de control ABR:

* Configure los parámetros en la variable `ABRControlParameters` clase.
