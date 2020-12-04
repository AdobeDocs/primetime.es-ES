---
description: Los flujos HLS y DASH proporcionan diferentes codificaciones de velocidad de bits (perfiles) para la misma ráfaga corta de vídeo. TVSDK puede seleccionar el nivel de calidad de cada ráfaga en función del ancho de banda disponible.
seo-description: Los flujos HLS y DASH proporcionan diferentes codificaciones de velocidad de bits (perfiles) para la misma ráfaga corta de vídeo. TVSDK puede seleccionar el nivel de calidad de cada ráfaga en función del ancho de banda disponible.
seo-title: Velocidad de bits adaptable (ABR) para la calidad de vídeo
title: Velocidad de bits adaptable (ABR) para la calidad de vídeo
uuid: e5752d7e-fa7d-407c-96df-c3830a35c66e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---


# Velocidad de bits adaptable (ABR) para la calidad de vídeo{#adaptive-bit-rates-abr-for-video-quality}

Los flujos HLS y DASH proporcionan diferentes codificaciones de velocidad de bits (perfiles) para la misma ráfaga corta de vídeo. TVSDK puede seleccionar el nivel de calidad de cada ráfaga en función del ancho de banda disponible.

TVSDK supervisa constantemente la velocidad de bits para asegurarse de que el contenido se reproduce a la velocidad de bits óptima para la conexión de red actual.

Puede establecer la directiva de conmutación de velocidad de bits adaptable (ABR) y las velocidades de bits inicial, mínima y máxima para un flujo de velocidad de bits múltiple (MBR). TVSDK cambia automáticamente a la velocidad de bits que proporciona la mejor experiencia de reproducción en la configuración especificada.

<table id="table_AF838E082235406AA359BF1C1A77F85F"> 
 <tbody> 
  <tr> 
   <td colname="col01"> Velocidad de bits inicial </td> 
   <td colname="col2"> <p>Velocidad de bits de reproducción deseada (en bits por segundo) para el primer segmento. Cuando se reproducen inicios, se utiliza el perfil más cercano, que es igual o bueno a la velocidad de bits inicial, para el primer segmento. </p> <p> Si se define una velocidad de bits mínima y la velocidad de bits inicial es inferior a la velocidad mínima, TVSDK selecciona el perfil con la velocidad de bits más baja por encima de la velocidad de bits mínima. Si la velocidad inicial es superior a la velocidad máxima, TVSDK selecciona la velocidad más alta por debajo de la velocidad máxima. </p> <p>Si la velocidad de bits inicial es cero o indefinida, la velocidad de bits inicial viene determinada por la directiva ABR. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocidad de bits mínima </td> 
   <td colname="col2"> <p>La velocidad de bits más baja permitida a la que puede cambiar el ABR. El cambio de ABR ignora los perfiles con una velocidad de bits inferior a esta velocidad de bits. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col01"> Velocidad de bits máxima </td> 
   <td colname="col2"> <p>La velocidad de bits máxima permitida a la que puede cambiar el ABR. El cambio de ABR ignora los perfiles con una velocidad de bits superior a esta velocidad de bits. </p> </td> 
  </tr> 
 </tbody> 
</table>

Tenga en cuenta la siguiente información:

* TVSDK no distribuye eventos a partir del cambio de velocidad de bits.
* Puede cambiar la configuración de ABR en cualquier momento y el reproductor cambiará para utilizar el perfil que más se adapte a la configuración más reciente.

Por ejemplo, si un flujo tiene los siguientes perfiles:

* 1: 300000
* 2: 700000
* 3: 1500000
* 4: 2400000
* 5: 4000000

Si especifica un intervalo de 300000 a 2000000, TVSDK solo tendrá en cuenta los perfiles 1, 2 y 3. Esto permite que las aplicaciones se ajusten a diversas condiciones de red, como cambiar de Wi-Fi a 3G o a varios dispositivos como un teléfono, una tablet o un equipo de escritorio.

## Configurar velocidades de bits adaptables {#section_572FCE4CC28D4DF8BD9C461F00B3CA17}

Para configurar los parámetros de velocidad de bits adaptables de TVSDK:

1. Configure una instancia de `PTABRControlParameters` para establecer la configuración inicial, mínima y máxima de velocidad de bits.

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

1. Actualice la instancia `PTMediaPlayer` con la instancia `PTABRControlParameters` configurada.

   ```
   // assuming self.player is the PTMediaPlayer instance 
   self.player.abrControlParameters = abrMetaData;
   ```

Recuerde lo siguiente:

* La aplicación debe establecer la propiedad `abrControlParameters` en `PTMediaPlayer` antes de configurar una instancia `PTMediaPlayerItem` para que la configuración de velocidad de bits inicial y mínima surta efecto.

   Tras los inicios de reproducción de contenido, la configuración de una nueva instancia solo afecta al ajuste de velocidad de bits máxima.

* Para actualizar la configuración de velocidad de bits máxima durante la reproducción, cree una nueva instancia `PTABRControlParameters` y configúrela en la instancia del reproductor.
* Puede actualizar la configuración de velocidad de bits máxima durante la reproducción solo en iOS 8.0 y posterior. Para versiones anteriores, se utiliza el valor `maxBitrate` que se estableció antes de iniciar la reproducción del contenido.

