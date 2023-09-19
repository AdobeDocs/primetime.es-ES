---
description: Los flujos HLS y DASH proporcionan diferentes codificaciones (perfiles) de velocidad de bits para la misma ráfaga corta de vídeo. TVSDK puede seleccionar el nivel de calidad para cada ráfaga en función del ancho de banda disponible.
title: Velocidad de bits adaptable (ABR) para la calidad de vídeo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 0%

---

# Velocidad de bits adaptable (ABR) para la calidad de vídeo{#adaptive-bit-rates-abr-for-video-quality}

Los flujos HLS y DASH proporcionan diferentes codificaciones (perfiles) de velocidad de bits para la misma ráfaga corta de vídeo. TVSDK puede seleccionar el nivel de calidad para cada ráfaga en función del ancho de banda disponible.

TVSDK supervisa constantemente la velocidad de bits para garantizar que el contenido se reproduce a la velocidad de bits óptima para la conexión de red actual.

Puede establecer la directiva de conmutación de velocidad de bits adaptable (ABR) y las tasas de bits inicial, mínima y máxima para un flujo de velocidad de bits múltiple (MBR). TVSDK cambia automáticamente a la velocidad de bits que proporciona la mejor experiencia de reproducción en la configuración especificada.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Velocidad de bits inicial </td> 
   <td colname="col2"> <p>La velocidad de bits de reproducción deseada (en bits por segundo) para el primer segmento. Cuando comienza la reproducción, se utiliza el perfil más cercano, que es igual o mayor que la velocidad de bits inicial, para el primer segmento. </p> <p> Si se define una velocidad de bits mínima y la velocidad de bits inicial es inferior a la velocidad mínima, TVSDK selecciona el perfil con la velocidad de bits más baja por encima de la velocidad de bits mínima. Si la tasa inicial está por encima de la tasa máxima, TVSDK selecciona la tasa más alta por debajo de la tasa máxima. </p> <p>Si la velocidad de bits inicial es cero o indefinida, la velocidad de bits inicial viene determinada por la directiva ABR. </p> <p> <span class="apiname"> ABRInitialBitRate </span> devuelve un valor entero que representa el perfil de byte por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocidad de bits mínima </td> 
   <td colname="col2"> <p>La velocidad de bits más baja permitida a la que ABR puede cambiar. La conmutación ABR ignora los perfiles con una velocidad de bits inferior a esta velocidad de bits. </p> <p> <span class="apiname"> ABRMinBitRate </span> devuelve un valor entero que representa el perfil de bits por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocidad de bits máxima </td> 
   <td colname="col2"> <p>La velocidad de bits más alta permitida a la que ABR puede cambiar. La conmutación ABR ignora los perfiles con una velocidad de bits superior a esta velocidad de bits. </p> <p> <span class="apiname"> ABRMaxBitRate </span> devuelve un valor entero que representa el perfil de bits por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> directiva de cambio ABR </td> 
   <td colname="col2"> La reproducción cambia gradualmente al perfil de velocidad de bits más alta cuando es posible. Puede establecer la directiva para el cambio ABR, que determina la rapidez con la que TVSDK cambia entre perfiles. El valor predeterminado es <span class="codeph"> POLÍTICA_MODERADA </span>. <p>Cuando TVSDK decide cambiar a una velocidad de bits más alta, el reproductor selecciona el perfil de velocidad de bits ideal al que cambiar en función de la directiva ABR actual: 
     <ul id="ul_058D0FFC944C476A83BB9E756B95DEBD"> 
      <li id="li_C690A12DC34C4754B01C2D0616FB6A0A"> <span class="codeph"> CONSERVATIVE_POLICY </span>: cambia al perfil con la siguiente velocidad de bits más alta cuando el ancho de banda es un 50 % más alto que la velocidad de bits actual. </li> 
      <li id="li_FF5BDB099B554940AC296938C7A12B81"> <span class="codeph"> POLÍTICA_MODERADA </span>: cambia al siguiente perfil de velocidad de bits más alta cuando el ancho de banda es un 20 % mayor que la velocidad de bits actual. </li> 
      <li id="li_E602508429864C279BF78360E95718A6"> <span class="codeph"> AGGRESSIVE_POLICY </span>: cambia inmediatamente al perfil de velocidad de bits más alta cuando el ancho de banda es mayor que la velocidad de bits actual. </li> 
     </ul> </p> <p>Si la velocidad de bits inicial es cero o no se especifica, pero se especifica una directiva, la reproducción comienza con el perfil de velocidad de bits más bajo para los perfiles conservadores, el perfil más cercano a la velocidad de bits media de los perfiles disponibles para los perfiles moderados y el perfil de velocidad de bits más alto para los agresivos. </p> <p>La directiva funciona en las restricciones de las tasas de bits mínima y máxima, si se especifican estas tasas. </p> <p> <span class="codeph"> ABRPolicy </span> devuelve la configuración actual desde el <span class="codeph"> ABRControlParameters </span> enum: CONSERVATIVE_POLICY, MODERATE_POLICY o AGGRESSIVE_POLICY. </p> </td> 
  </tr> 
 </tbody> 
</table>

Tenga en cuenta lo siguiente:

* El mecanismo de conmutación por error de TVSDK puede anular la configuración, ya que TVSDK prefiere una experiencia de reproducción continua en lugar de cumplir estrictamente los parámetros de control.
* Cuando la velocidad de bits cambia, TVSDK envía `ProfileEvent.PROFILE_CHANGED`.
* Puede cambiar la configuración de ABR en cualquier momento, y el reproductor cambia para utilizar el perfil que más coincida con la configuración más reciente.

Por ejemplo, si una secuencia tiene los siguientes perfiles:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Si especifica un intervalo de 300000 para 2000000, TVSDK solo tiene en cuenta los perfiles 1, 2 y 3. Esto permite que las aplicaciones se ajusten a diversas condiciones de la red, como cambiar de wi-fi a 3G o a varios dispositivos, como un teléfono, una tableta o un equipo de escritorio.

Para definir los parámetros de control ABR, siga uno de estos procedimientos:

* Utilice el `ABRControlParameterBuilder` clase auxiliar para establecer cualquier subconjunto de los parámetros (funciona con `ABRControlParameter` entre bastidores)

* Configure los parámetros en la variable `ABRControlParameter` clase.

## Configurar tasas de bits adaptables mediante ABRControlParametersBuilder {#section_3DDE397A7CE445E1832EBAA46CE5C069}

Uso del `ABRControlParametersBuilder` La clase auxiliar es la forma más sencilla y eficaz de establecer parámetros ABR.

* El `ABRControlParametersBuilder` establece todos los parámetros ABR en valores predeterminados en el subyacente `ABRControlParameters` objeto.

* Puede restablecer parámetros ABR individuales durante el tiempo de ejecución, siempre y cuando mantenga una referencia al mismo `ABRControlParametersBuilder` ejemplo.

Esta clase también incluye el `toABRControlParameters()` método de ayuda. Utilice este método para obtener una instancia de `ABRControlParameters` y ponlo en la `mediaPlayer.ABRControlParameters` propiedad. Esto hace que la configuración entre en vigor en el reproductor.

1. Crear una instancia de `ABRControlParametersBuilder` y establezca los parámetros en el Reproductor de medios.

   >[!NOTE]
   >
   >Por ejemplo, en el siguiente ejemplo se inicializan todos los parámetros con los valores predeterminados, se establece únicamente la directiva en conservador y se restringe la velocidad de bits máxima a 1000000:
   >
   >```
   >var abrBuilder:ABRControlParametersBuilder =  
   >   new ABRControlParametersBuilder(); 
   >abrBuilder.policy = ABRControlParameters.CONSERVATIVE_POLICY; 
   >abrBuilder.maxBitRate = 1000000; 
   >mediaPlayer.abrControlParameters =  
   >   abrBuilder.toABRControlParameters();
   >```
   >

1. Modificar parámetros ABR individuales en tiempo de ejecución.

   Para modificar parámetros individuales y dejar el resto de los parámetros tal cual:

   ```
   // If later you want to reset the max bit rate to 2000000 
   abrBuilder.maxBitRate = 2000000; 
   mediaPlayer.abrControlParameters =  
     abrBuilder.toABRControlParameters();
   ```

   Para conservar la configuración anterior, debe mantener una referencia a la misma `ABRControlParametersBuilder` instancia que creó en el paso 1.

## Configurar tasas de bits adaptables mediante ABRControlParameters {#section_02161FD0A73F40ED9CAE17F9AF850483}

Sólo puede establecer valores de control ABR con `ABRControlParameters`, pero puede construir una nueva en cualquier momento.

Esta capacidad para establecer parámetros ABR era compatible antes de la existencia del `ABRControlParametersBuilder` , pero esta capacidad sigue siendo eficaz para configurar los parámetros ABR en el momento de la construcción. Sin embargo, para cambiar parámetros individuales después de la construcción, debe utilizar el `ABRControlParametersBuilder` clase.

Las siguientes condiciones se aplican a `ABRControlParameters`:

* Debe proporcionar valores para todos los parámetros en tiempo de construcción.
* No se pueden cambiar valores individuales después del tiempo de construcción.
* Si los parámetros especificados están fuera del intervalo permitido, una variable `ArgumentError` se ha lanzado.

1. Decida la velocidad de bits inicial, mínima y máxima.
1. Determine la directiva ABR:

   * `CONSERVATIVE_POLICY`
   * `MODERATE_POLICY`
   * `AGGRESSIVE_POLICY`

1. Establezca los valores del parámetro ABR en la variable `ABRControlParameters` y asignarlos al reproductor de medios.

   ```
   mediaPlayer.abrControlParameters = new ABRControlParameters( 
       ABRControlParameters.CONSERVATIVE_POLICY, 
       0, // Initial bit rate 
       0, // Minimum bit rate 
       1000000 // Maximum bit rate 
   );
   ```
