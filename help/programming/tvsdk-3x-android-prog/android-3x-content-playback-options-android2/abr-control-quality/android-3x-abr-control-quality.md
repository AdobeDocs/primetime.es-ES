---
description: Los flujos HLS y DASH proporcionan diferentes codificaciones (perfiles) de velocidad de bits para la misma ráfaga corta de vídeo. TVSDK puede seleccionar el nivel de calidad para cada ráfaga en función del nivel de almacenamiento en búfer actual y el ancho de banda disponible.
title: Velocidad de bits adaptable (ABR) para la calidad de vídeo
exl-id: ed062ef9-138d-446a-a454-3cb19c3bb388
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# Información general {#adaptive-bit-rates-abr-for-video-quality-overview}

Los flujos HLS y DASH proporcionan diferentes codificaciones (perfiles) de velocidad de bits para la misma ráfaga corta de vídeo. TVSDK puede seleccionar el nivel de calidad para cada ráfaga en función del nivel de almacenamiento en búfer actual y el ancho de banda disponible.

TVSDK supervisa constantemente la velocidad de bits para garantizar que el contenido se reproduce a la velocidad de bits óptima para la conexión de red actual. Puede establecer la directiva de conmutación de velocidad de bits adaptable (ABR) y las tasas de bits inicial, mínima y máxima para un flujo de velocidad de bits múltiple (MBR). TVSDK cambia automáticamente a la velocidad de bits que proporciona la mejor experiencia de reproducción en la configuración especificada.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Velocidad de bits inicial </td> 
   <td colname="col2"> <p>La velocidad de bits de reproducción deseada (en bits por segundo) para el primer segmento. </p> <p>Cuando comienza la reproducción, se utiliza el perfil más cercano, que es igual o bueno que la velocidad de bits inicial, para el primer segmento. Si se define una velocidad de bits mínima y la velocidad de bits inicial es inferior a la velocidad mínima, TVSDK selecciona el perfil con la velocidad de bits más baja por encima de la velocidad de bits mínima. Si la tasa inicial está por encima de la tasa máxima, TVSDK selecciona la tasa más alta por debajo de la tasa máxima. Si la velocidad de bits inicial es cero o indefinida, la velocidad de bits inicial viene determinada por la directiva ABR. </p> <p><span class="codeph"> getABRInitialBitRate</span> devuelve un valor entero que representa el perfil de byte por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocidad de bits mínima </td> 
   <td colname="col2"> <p>La velocidad de bits más baja permitida a la que ABR puede cambiar. </p> <p>La conmutación ABR ignora los perfiles con una velocidad de bits inferior a esta velocidad de bits. <span class="codeph"> getABRMinBitRate</span> devuelve un valor entero que representa el perfil de bits por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocidad de bits máxima </td> 
   <td colname="col2"> <p>La velocidad de bits más alta permitida a la que ABR puede cambiar. </p> <p>La conmutación ABR ignora los perfiles con una velocidad de bits superior a esta velocidad de bits. <span class="codeph"> getABRMaxBitRate</span> devuelve un valor entero que representa el perfil de bits por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> directiva de cambio ABR </td> 
   <td colname="col2"> <p>La reproducción cambia gradualmente al perfil de velocidad de bits más alta cuando es posible. Puede establecer la directiva para el cambio ABR, que determina la rapidez con la que TVSDK cambia entre perfiles. El valor predeterminado es <span class="codeph"> ABR_MODERATE</span>. </p> <p>Cuando TVSDK decide cambiar a una velocidad de bits más alta, el reproductor selecciona el perfil de velocidad de bits ideal al que cambiar en función de la directiva ABR actual: 
     <ul id="ul_AC9C99D84A3B4A8DBD1A05CC05DEE771"> 
      <li id="li_B79C0AA2CBFB42FF98A257CEC9C400BA"><span class="codeph"> ABR_CONSERVATIVE</span>: cambia al perfil con la siguiente velocidad de bits más alta cuando el ancho de banda es un 50 % más alto que la velocidad de bits actual. </li> 
      <li id="li_38CC3A95D8634F359D0F7C273D0108C0"><span class="codeph"> ABR_MODERATE</span>: cambia al siguiente perfil de velocidad de bits más alta cuando el ancho de banda es un 20 % mayor que la velocidad de bits actual. </li> 
      <li id="li_E845C035420D4B3FB2B179F448F8CA85"><span class="codeph"> ABR_AGRESIVO</span>: cambia inmediatamente al perfil de velocidad de bits más alta cuando el ancho de banda es mayor que la velocidad de bits actual. </li> 
     </ul> </p> <p>Si la velocidad de bits inicial es cero o no se especifica pero se especifica una directiva, la reproducción comienza con el perfil de velocidad de bits más bajo para una directiva conservadora, el perfil más cercano a la velocidad de bits media de los perfiles disponibles para una directiva moderada y el perfil de velocidad de bits más alto para una directiva agresiva. </p> <p>La directiva funciona en las restricciones de las tasas de bits mínima y máxima, si se especifican estas tasas. </p> <p> <span class="codeph"> getABRPolicy</span> devuelve la configuración actual desde el <span class="codeph"> ABRControlParameters</span> enum: <span class="codeph"> ABR_CONSERVATIVE</span>, <span class="codeph"> ABR_MODERATE</span>, o <span class="codeph"> ABR_AGRESIVO</span>. </p> <p>Para obtener más información, consulte el documento API de parámetros de control ABR. </p> </td> 
  </tr> 
 </tbody> 
</table>

Tenga en cuenta lo siguiente:

* El mecanismo de conmutación por error de TVSDK puede anular la configuración, ya que TVSDK prefiere una experiencia de reproducción continua en lugar de cumplir estrictamente los parámetros de control.
* Cuando la velocidad de bits cambia, TVSDK envía `onProfileChanged` eventos en `PlaybackEventListener`.

* Puede cambiar la configuración de ABR en cualquier momento, y el reproductor cambia para utilizar el perfil que más coincida con la configuración más reciente.

Por ejemplo, si una secuencia tiene los siguientes perfiles:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Si especifica un intervalo de 300000 para 2000000, TVSDK solo tiene en cuenta los perfiles 1, 2 y 3. Esto permite que las aplicaciones se ajusten a diversas condiciones de la red, como cambiar de wi-fi a 3G o a varios dispositivos, como un teléfono, una tableta o un equipo de escritorio.

Para establecer los parámetros de control ABR, establezca los parámetros en la variable `ABRControlParameter` clase.
