---
description: Los flujos HLS y DASH proporcionan diferentes codificaciones (perfiles) de velocidad de bits para la misma ráfaga corta de vídeo. TVSDK puede seleccionar el nivel de calidad para cada ráfaga en función del ancho de banda disponible.
title: Velocidad de bits adaptable (ABR) para la calidad de vídeo
exl-id: 97862cf7-7315-4ca6-a2b4-f9b98047edd9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# Velocidad de bits adaptable (ABR) para la calidad de vídeo {#adaptive-bit-rates-abr-for-video-quality}

Los flujos HLS y DASH proporcionan diferentes codificaciones (perfiles) de velocidad de bits para la misma ráfaga corta de vídeo. TVSDK puede seleccionar el nivel de calidad para cada ráfaga en función del ancho de banda disponible.

TVSDK supervisa constantemente la velocidad de bits para garantizar que el contenido se reproduce a la velocidad de bits óptima para la conexión de red actual.

Puede establecer la directiva de conmutación de velocidad de bits adaptable (ABR) y las tasas de bits inicial, mínima y máxima para un flujo de velocidad de bits múltiple (MBR). TVSDK cambia automáticamente a la velocidad de bits que proporciona la mejor experiencia de reproducción en la configuración especificada.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Velocidad de bits inicial </td> 
   <td colname="col2"> <p>La velocidad de bits de reproducción deseada (en bits por segundo) para el primer segmento. Cuando comienza la reproducción, se utiliza el perfil más cercano, que es igual o bueno que la velocidad de bits inicial, para el primer segmento. </p> <p> Si se define una velocidad de bits mínima y la velocidad de bits inicial es inferior a la velocidad mínima, TVSDK selecciona el perfil con la velocidad de bits más baja por encima de la velocidad de bits mínima. Si la tasa inicial está por encima de la tasa máxima, TVSDK selecciona la tasa más alta por debajo de la tasa máxima. </p> <p>Si la velocidad de bits inicial es cero o indefinida, la velocidad de bits inicial viene determinada por la directiva ABR. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocidad de bits mínima </td> 
   <td colname="col2"> <p>La velocidad de bits más baja permitida a la que ABR puede cambiar. La conmutación ABR ignora los perfiles con una velocidad de bits inferior a esta velocidad de bits. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocidad de bits máxima </td> 
   <td colname="col2"> <p>La velocidad de bits más alta permitida a la que ABR puede cambiar. La conmutación ABR ignora los perfiles con una velocidad de bits superior a esta velocidad de bits. </p> </td> 
  </tr> 
 </tbody> 
</table>

Tenga en cuenta lo siguiente:

* TVSDK no distribuye eventos desde la conmutación a velocidad de bits.
* Puede cambiar la configuración de ABR en cualquier momento, y el reproductor cambia para utilizar el perfil que más coincida con la configuración más reciente.

Por ejemplo, si una secuencia tiene los siguientes perfiles:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Si especifica un intervalo de 300000 para 2000000, TVSDK solo tiene en cuenta los perfiles 1, 2 y 3. Esto permite que las aplicaciones se ajusten a diversas condiciones de la red, como cambiar de WiFi a 3G o a varios dispositivos, como un teléfono, una tableta o un equipo de escritorio.

## Configurar tasas de bits adaptables {#section_572FCE4CC28D4DF8BD9C461F00B3CA17}

Para configurar los parámetros de velocidad de bits adaptable de TVSDK:

1. Configuración de una instancia de `PTABRControlParameters` para establecer la configuración inicial, mínima y máxima de velocidad de bits.

   Los valores predeterminados se muestran en el siguiente fragmento de código, pero la aplicación puede establecer cualquier valor entero para cada uno de estos parámetros.

   >[!IMPORTANT]
   >
   >Especifique la configuración de velocidad de bits en bits por segundo (bps).

   ```
   // ARC (add autorelease for non-ARC) 
   PTABRControlParameters *abrMetaData =  
       [[PTABRControlParameters alloc] init];  
   
   abrMetaData.initialBitRate = -1; 
   abrMetaData.minBitRate = 0; 
   abrMetaData.maxBitRate = INT_MAX;
   ```

1. Actualice su `PTMediaPlayer` instancia con el configurado `PTABRControlParameters` ejemplo.

   ```
   // assuming self.player is the PTMediaPlayer instance 
   self.player.abrControlParameters = abrMetaData;
   ```

Recuerde lo siguiente:

* La aplicación debe establecer el `abrControlParameters` propiedad en `PTMediaPlayer` antes de configurar un `PTMediaPlayerItem` para que los ajustes de velocidad de bits inicial y mínima surtan efecto.

   Una vez iniciada la reproducción del contenido, la definición de una nueva instancia solo afecta a la configuración de velocidad de bits máxima.

* Para actualizar la configuración de velocidad de bits máxima durante la reproducción, cree un nuevo `PTABRControlParameters` y configúrela en la instancia del reproductor.
* Solo se puede actualizar la configuración de velocidad de bits máxima durante la reproducción en iOS 8.0 y versiones posteriores. Para versiones anteriores, la variable `maxBitrate` valor que se estableció antes de que se iniciara la reproducción del contenido.
