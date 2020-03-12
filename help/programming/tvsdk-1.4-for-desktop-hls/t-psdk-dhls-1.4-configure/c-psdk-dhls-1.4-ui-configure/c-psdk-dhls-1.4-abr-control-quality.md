---
description: Los flujos HLS y DASH proporcionan diferentes codificaciones de velocidad de bits (perfiles) para la misma ráfaga corta de vídeo. TVSDK puede seleccionar el nivel de calidad de cada ráfaga en función del ancho de banda disponible.
seo-description: Los flujos HLS y DASH proporcionan diferentes codificaciones de velocidad de bits (perfiles) para la misma ráfaga corta de vídeo. TVSDK puede seleccionar el nivel de calidad de cada ráfaga en función del ancho de banda disponible.
seo-title: Velocidad de bits adaptable (ABR) para la calidad de vídeo
title: Velocidad de bits adaptable (ABR) para la calidad de vídeo
uuid: e3d5ef90-067d-48e0-a025-081de931d842
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Velocidad de bits adaptable (ABR) para la calidad de vídeo{#adaptive-bit-rates-abr-for-video-quality}

Los flujos HLS y DASH proporcionan diferentes codificaciones de velocidad de bits (perfiles) para la misma ráfaga corta de vídeo. TVSDK puede seleccionar el nivel de calidad de cada ráfaga en función del ancho de banda disponible.

TVSDK supervisa constantemente la velocidad de bits para asegurarse de que el contenido se reproduce a la velocidad de bits óptima para la conexión de red actual.

Puede establecer la directiva de conmutación de velocidad de bits adaptable (ABR) y las velocidades de bits inicial, mínima y máxima para un flujo de velocidad de bits múltiple (MBR). TVSDK cambia automáticamente a la velocidad de bits que proporciona la mejor experiencia de reproducción en la configuración especificada.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Velocidad de bits inicial </td> 
   <td colname="col2"> <p>Velocidad de bits de reproducción deseada (en bits por segundo) para el primer segmento. Cuando se inicia la reproducción, se utiliza el perfil más cercano, que es igual o bueno a la velocidad de bits inicial, para el primer segmento. </p> <p> Si se define una velocidad de bits mínima y la velocidad de bits inicial es inferior a la velocidad mínima, TVSDK selecciona el perfil con la velocidad de bits más baja por encima de la velocidad de bits mínima. Si la velocidad inicial es superior a la velocidad máxima, TVSDK selecciona la velocidad más alta por debajo de la velocidad máxima. </p> <p>Si la velocidad de bits inicial es cero o indefinida, la velocidad de bits inicial viene determinada por la directiva ABR. </p> <p> <span class="apiname"> ABRInitialBitRate </span> devuelve un valor entero que representa el perfil byte por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocidad de bits mínima </td> 
   <td colname="col2"> <p>La velocidad de bits más baja permitida a la que puede cambiar el ABR. El cambio de ABR ignora los perfiles con una velocidad de bits inferior a esta velocidad de bits. </p> <p> <span class="apiname"> ABRMinBitRate </span> devuelve un valor entero que representa el perfil bits por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocidad de bits máxima </td> 
   <td colname="col2"> <p>La velocidad de bits máxima permitida a la que puede cambiar el ABR. El cambio de ABR ignora los perfiles con una velocidad de bits superior a esta velocidad de bits. </p> <p> <span class="apiname"> ABRMaxBitRate </span> devuelve un valor entero que representa el perfil bits por segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Política de conmutación ABR </td> 
   <td colname="col2"> La reproducción cambia gradualmente al perfil de velocidad de bits más alta cuando es posible. Puede establecer la directiva para el cambio ABR, que determina la rapidez con la que TVSDK cambia entre perfiles. El valor predeterminado es <span class="codeph"> MODERATE_POLICY </span>. <p>Cuando TVSDK decide cambiar a una velocidad de bits más alta, el reproductor selecciona el perfil de velocidad de bits ideal para cambiar a según la directiva ABR actual: 
     <ul id="ul_058D0FFC944C476A83BB9E756B95DEBD"> 
      <li id="li_C690A12DC34C4754B01C2D0616FB6A0A"> <span class="codeph"> CONSERVATIVE_POLICY </span>: Cambia al perfil con la siguiente velocidad de bits más alta cuando el ancho de banda es un 50 % superior a la velocidad de bits actual. </li> 
      <li id="li_FF5BDB099B554940AC296938C7A12B81"> <span class="codeph"> MODERATE_POLICY </span>: Cambia al siguiente perfil de velocidad de bits más alta cuando el ancho de banda es un 20% mayor que la velocidad de bits actual. </li> 
      <li id="li_E602508429864C279BF78360E95718A6"> <span class="codeph"> AGGRESSIVE_POLICY </span>: Cambia inmediatamente al perfil de velocidad de bits más alta cuando el ancho de banda es superior a la velocidad de bits actual. </li> 
     </ul> </p> <p>Si la velocidad de bits inicial es cero o no se especifica, pero se especifica una política, la reproducción comienza con el perfil de velocidad de bits más bajo para el perfil conservador, el perfil más cercano a la velocidad de bits media de los perfiles disponibles para el moderado y el perfil de velocidad de bits más alto para el agresivo. </p> <p>La directiva funciona con las restricciones de las velocidades de bits mínimas y máximas, si se especifican estas velocidades. </p> <p> <span class="codeph"> ABRPolicy </span> devuelve la configuración actual de la enumeración <span class="codeph"> ABRControlParameters </span> : CONSERVATIVE_POLICY, MODERATE_POLICY o AGGRESSIVE_POLICY. </p> </td> 
  </tr> 
 </tbody> 
</table>

Tenga en cuenta la siguiente información:

* El mecanismo de conmutación por error de TVSDK puede anular su configuración, ya que TVSDK favorece una reproducción continua en lugar de cumplir estrictamente los parámetros de control.
* Cuando cambia la velocidad de bits, TVSDK se distribuye `ProfileEvent.PROFILE_CHANGED`.
* Puede cambiar la configuración de ABR en cualquier momento y el reproductor cambiará para utilizar el perfil que más se adapte a la configuración más reciente.

Por ejemplo, si un flujo tiene los siguientes perfiles:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Si especifica un intervalo de 300000 a 2000000, TVSDK solo tendrá en cuenta los perfiles 1, 2 y 3. Esto permite que las aplicaciones se ajusten a diversas condiciones de red, como el cambio de wi-fi a 3G o a varios dispositivos como un teléfono, una tablet o un equipo de escritorio.

Para definir los parámetros de control ABR, realice una de las siguientes acciones:

* Utilice la clase `ABRControlParameterBuilder` auxiliar para establecer cualquier subconjunto de parámetros (funciona en `ABRControlParameter` segundo plano)

* Defina los parámetros de la `ABRControlParameter` clase.

## Configurar velocidades de bits adaptables mediante ABRControlParametersBuilder {#section_3DDE397A7CE445E1832EBAA46CE5C069}

El uso de la clase `ABRControlParametersBuilder` auxiliar es la forma más sencilla y eficaz de establecer los parámetros ABR.

* El constructor `ABRControlParametersBuilder` establece todos los parámetros ABR en valores predeterminados en el `ABRControlParameters` objeto subyacente.

* Puede restablecer parámetros ABR individuales durante el tiempo de ejecución, siempre y cuando mantenga una referencia a la misma `ABRControlParametersBuilder` instancia.

Esta clase también incluye el método `toABRControlParameters()` auxiliar. Utilice este método para obtener una instancia de `ABRControlParameters` y establecerla en la `mediaPlayer.ABRControlParameters` propiedad. Esto hace que la configuración entre en vigor en el reproductor.

1. Cree una instancia de la clase auxiliar y establezca los parámetros en el Reproductor de medios `ABRControlParametersBuilder` .

   >[!NOTE]
   >
   >Por ejemplo, en el siguiente ejemplo se inicializan todos los parámetros con los valores predeterminados y, a continuación, se establece únicamente la política en conservador y se restringe la velocidad máxima de bits a 1000000:    >
   >
   >
   ```>
   >var abrBuilder:ABRControlParametersBuilder =  
   >   new ABRControlParametersBuilder(); 
   >abrBuilder.policy = ABRControlParameters.CONSERVATIVE_POLICY; 
   >abrBuilder.maxBitRate = 1000000; 
   >mediaPlayer.abrControlParameters =  
   >   abrBuilder.toABRControlParameters();
   >```   >
   >



1. Modifique los parámetros de ABR individuales en tiempo de ejecución.

   Para modificar parámetros individuales y dejar el resto de los parámetros tal como estaban:

   ```
   // If later you want to reset the max bit rate to 2000000 
   abrBuilder.maxBitRate = 2000000; 
   mediaPlayer.abrControlParameters =  
     abrBuilder.toABRControlParameters();
   ```

   Para conservar la configuración anterior, debe mantener una referencia a la misma `ABRControlParametersBuilder` instancia que creó en el paso 1.

## Configurar velocidades de bits adaptables mediante ABRControlParameters {#section_02161FD0A73F40ED9CAE17F9AF850483}

Los valores de control de ABR solo se pueden establecer con `ABRControlParameters`, pero se puede construir uno nuevo en cualquier momento.

Esta capacidad de establecer parámetros ABR se admitía antes de la existencia de la `ABRControlParametersBuilder` clase, pero esta capacidad sigue siendo efectiva para establecer parámetros ABR en tiempo de construcción. Sin embargo, para cambiar parámetros individuales después de la construcción, debe utilizar la `ABRControlParametersBuilder` clase.

Se aplican las siguientes condiciones a `ABRControlParameters`:

* Debe proporcionar valores para todos los parámetros en tiempo de construcción.
* No se pueden cambiar valores individuales después del tiempo de construcción.
* Si los parámetros especificados están fuera del rango permitido, se `ArgumentError` genera un error.

1. Decida las velocidades de bits iniciales, mínimas y máximas.
1. Determine la directiva ABR:

   * `CONSERVATIVE_POLICY`
   * `MODERATE_POLICY`
   * `AGGRESSIVE_POLICY`

1. Establezca los valores de parámetro ABR en el constructor y asígnelos al Reproductor de medios `ABRControlParameters` .

   ```
   mediaPlayer.abrControlParameters = new ABRControlParameters( 
       ABRControlParameters.CONSERVATIVE_POLICY, 
       0, // Initial bit rate 
       0, // Minimum bit rate 
       1000000 // Maximum bit rate 
   );
   ```

