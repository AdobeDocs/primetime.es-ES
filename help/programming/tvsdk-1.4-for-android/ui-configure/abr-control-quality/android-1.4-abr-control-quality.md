---
description: Los flujos HLS y DASH proporcionan diferentes codificaciones de velocidad de bits (perfiles) para la misma ráfaga corta de vídeo. TVSDK puede seleccionar el nivel de calidad de cada ráfaga en función del ancho de banda disponible.
seo-description: Los flujos HLS y DASH proporcionan diferentes codificaciones de velocidad de bits (perfiles) para la misma ráfaga corta de vídeo. TVSDK puede seleccionar el nivel de calidad de cada ráfaga en función del ancho de banda disponible.
seo-title: Velocidad de bits adaptable (ABR) para la calidad de vídeo
title: Velocidad de bits adaptable (ABR) para la calidad de vídeo
uuid: 1de26f34-4eac-4c9c-8f59-8c34d69a2d01
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Información general {#adaptive-bit-rates-abr-for-video-quality-overview}

Los flujos HLS y DASH proporcionan diferentes codificaciones de velocidad de bits (perfiles) para la misma ráfaga corta de vídeo. TVSDK puede seleccionar el nivel de calidad de cada ráfaga en función del ancho de banda disponible.

TVSDK supervisa constantemente la velocidad de bits para asegurarse de que el contenido se reproduce a la velocidad de bits óptima para la conexión de red actual.

Puede establecer la directiva de conmutación de velocidad de bits adaptable (ABR) y las velocidades de bits inicial, mínima y máxima para un flujo de velocidad de bits múltiple (MBR). TVSDK cambia automáticamente a la velocidad de bits que proporciona la mejor experiencia de reproducción en la configuración especificada.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Velocidad de bits inicial </td> 
   <td colname="col2"> <p>Velocidad de bits de reproducción deseada (en bits por segundo) para el primer segmento. Cuando se inicia la reproducción, se utiliza el perfil más cercano, que es igual o bueno a la velocidad de bits inicial, para el primer segmento. </p> <p> Si se define una velocidad de bits mínima y la velocidad de bits inicial es inferior a la velocidad mínima, TVSDK selecciona el perfil con la velocidad de bits más baja por encima de la velocidad de bits mínima. Si la velocidad inicial es superior a la velocidad máxima, TVSDK selecciona la velocidad más alta por debajo de la velocidad máxima. </p> <p>Si la velocidad de bits inicial es cero o indefinida, la velocidad de bits inicial viene determinada por la directiva ABR. </p> <p><span class="codeph"> getABRInitialBitRate</span> devuelve un valor entero que representa el perfil de byte por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocidad de bits mínima </td> 
   <td colname="col2"> <p>La velocidad de bits más baja permitida a la que puede cambiar el ABR. El cambio de ABR ignora los perfiles con una velocidad de bits inferior a esta velocidad de bits. </p> <p><span class="codeph"> getABRMinBitRate</span> devuelve un valor entero que representa el perfil bits por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocidad de bits máxima </td> 
   <td colname="col2"> <p>La velocidad de bits máxima permitida a la que puede cambiar el ABR. El cambio de ABR ignora los perfiles con una velocidad de bits superior a esta velocidad de bits. </p> <p><span class="codeph"> getABRMaxBitRate</span> devuelve un valor entero que representa el perfil bits por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Política de conmutación ABR </td> 
   <td colname="col2"> La reproducción cambia gradualmente al perfil de velocidad de bits más alta cuando es posible. Puede establecer la directiva para el cambio ABR, que determina la rapidez con la que TVSDK cambia entre perfiles. El valor predeterminado es <span class="codeph"> ABR_MODERATE</span>. <p>Cuando TVSDK decide cambiar a una velocidad de bits más alta, el reproductor selecciona el perfil de velocidad de bits ideal para cambiar a según la directiva ABR actual: 
     <ul id="ul_AC9C99D84A3B4A8DBD1A05CC05DEE771"> 
      <li id="li_B79C0AA2CBFB42FF98A257CEC9C400BA"><span class="codeph"> ABR_CONSERVATIVE</span>: Cambia al perfil con la siguiente velocidad de bits más alta cuando el ancho de banda es un 50 % superior a la velocidad de bits actual. </li> 
      <li id="li_38CC3A95D8634F359D0F7C273D0108C0"><span class="codeph"> ABR_MODERATE</span>: Cambia al siguiente perfil de velocidad de bits más alta cuando el ancho de banda es un 20% mayor que la velocidad de bits actual. </li> 
      <li id="li_E845C035420D4B3FB2B179F448F8CA85"><span class="codeph"> ABR_AGGRESSIVE</span>: Cambia inmediatamente al perfil de velocidad de bits más alta cuando el ancho de banda es superior a la velocidad de bits actual. </li> 
     </ul> </p> <p>Si la velocidad de bits inicial es cero o no se especifica, pero se especifica una política, la reproducción comienza con el perfil de velocidad de bits más bajo para el perfil conservador, el perfil más cercano a la velocidad de bits media de los perfiles disponibles para el moderado y el perfil de velocidad de bits más alto para el agresivo. </p> <p>La directiva funciona con las restricciones de las velocidades de bits mínimas y máximas, si se especifican estas velocidades. </p> <p><span class="codeph"> getABRPolicy</span> devuelve la configuración actual de la enumeración <span class="codeph"> ABRControlParameters</span> : 
     <ul id="ul_bd4_5kb_cz"> 
      <li id="li_E7C118AF48994454B7B3C016913DE545"><span class="codeph"> ABR_CONSERVATIVE</span> </li> 
      <li id="li_0A90BB42786449629CE7DD3364B385EE"><span class="codeph"> ABR_MODERATE</span> </li> 
      <li id="li_AFEB9B2862F24A369CA90596184A2883"><span class="codeph"> ABR_AGGRESSIVE</span> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

Tenga en cuenta la siguiente información:

* El mecanismo de conmutación por error de TVSDK puede anular su configuración, ya que TVSDK favorece una reproducción continua en lugar de cumplir estrictamente los parámetros de control.
* Cuando cambia la velocidad de bits, TVSDK distribuye `onProfileChanged` eventos en `PlaybackEventListener`.

* Puede cambiar la configuración de ABR en cualquier momento y el reproductor cambiará para utilizar el perfil que más se adapte a la configuración más reciente.

Por ejemplo, si un flujo tiene los siguientes perfiles:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Si especifica un intervalo de 300000 a 2000000, TVSDK solo tendrá en cuenta los perfiles 1, 2 y 3. Esto permite que las aplicaciones se ajusten a diversas condiciones de red, como el cambio de wi-fi a 3G o a varios dispositivos como un teléfono, una tablet o un equipo de escritorio.

Para definir parámetros de control ABR, establezca los parámetros en la `ABRControlParameter` clase.
