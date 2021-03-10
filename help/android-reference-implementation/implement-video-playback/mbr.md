---
description: El TVSDK puede reproducir vídeos que tengan varios perfiles con diferentes velocidades de bits, cambiando entre ellos para proporcionar más de un nivel de calidad en función del ancho de banda disponible.
title: Varias tasas de bits
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---


# Varias tasas de bits {#multiple-bit-rates}

El TVSDK puede reproducir vídeos que tengan varios perfiles con diferentes velocidades de bits, cambiando entre ellos para proporcionar más de un nivel de calidad en función del ancho de banda disponible.

Puede establecer las tasas de bits iniciales, mínimas y máximas, así como la directiva de conmutador de velocidad de bits adaptable (ABR) para un flujo de velocidad de bits múltiple (MBR). El TVSDK cambia automáticamente a la velocidad de bits que proporciona la mejor experiencia de reproducción dentro de la configuración especificada.

La implementación de referencia configura los siguientes parámetros ABR en [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html).

| Parámetro | Descripción |
|--- |--- |
| Tasa de bits inicial:  getABRInitialBitRate | Velocidad de bits de reproducción deseada (en bits por segundo) para el primer segmento. Cuando se inicia la reproducción, se utiliza el perfil más cercano (igual o bueno que la velocidad de bits inicial) para el primer segmento.  Si se define una velocidad de bits mínima y la velocidad de bits inicial es inferior al mínimo, el TVSDK selecciona el perfil con la tasa de bits más baja por encima de la tasa de bits mínima. Del mismo modo, si la velocidad inicial es superior a la máxima, el TVSDK selecciona la tasa más alta por debajo del máximo. Si la velocidad de bits inicial es cero o indefinida, la velocidad de bits inicial viene determinada por la directiva ABR.  Devuelve un valor entero que representa el perfil byte por segundo. |
| Velocidad de bits mínima:  getABRMinBitRate | La velocidad de bits más baja permitida a la que puede cambiar el ABR. El cambio de ABR ignora los perfiles con una velocidad de bits inferior a esta. Devuelve un valor entero que representa el perfil de bits por segundo. |
| Velocidad de bits máxima:  getABRMaxBitRate | La velocidad de bits máxima permitida a la que el ABR puede cambiar. El cambio de ABR ignora los perfiles con una velocidad de bits superior a esta. Devuelve un valor entero que representa el perfil de bits por segundo. |
| Política de conmutación ABR:  getABRPolicy | La reproducción cambia gradualmente al perfil de velocidad de bits más alta cuando es posible. Puede establecer la directiva para el cambio ABR, que determina con qué rapidez el TVSDK cambia entre perfiles. El valor predeterminado es Moderar. <ul><li>*Conservador*: Cambia al perfil con la siguiente velocidad de bits más alta cuando el ancho de banda es un 50% superior a la velocidad de bits actual. </li><li>*Moderar*: Cambia al siguiente perfil de velocidad de bits más alta cuando el ancho de banda es un 20% más alto que la velocidad de bits actual.</li><li>*Agresivo*: Cambia inmediatamente al perfil de velocidad de bits más alto cuando el ancho de banda es superior a la velocidad de bits actual</li></ul><br/>Si la velocidad de bits inicial es cero o no se especifica y se especifica una política, la reproducción comienza con el perfil de velocidad de bits más bajo para Conservative, el perfil más cercano a la tasa de bits media de perfiles disponibles para Moderate y el perfil de velocidad de bits más alto para Aggressive.<br/><br/>La directiva funciona dentro de las restricciones de las tasas de bits mínimas y máximas, si se especifican.  Devuelve la configuración actual de la enumeración ABRControlParameters: <ul><li>ABR_CONSERVATIVE</li><li>ABR_MODERATE </li><li>ABR_AGGRESSIVE</li></ul><br>Consulte también  [ABRPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/ABRControlParameters.ABRPolicy.html). |

>[!NOTE]
>
>* El mecanismo de conmutación por error de TVSDK puede anular esta configuración, ya que TVSDK prefiere una experiencia de reproducción continua en lugar de respetar estrictamente los parámetros de control.
>* Cuando cambia la velocidad de bits, el TVSDK envía eventos `onProfileChanged` en `PlaybackEventListener`.


## Habilitación del control ABR personalizado en la implementación de referencia {#section_72A6E7263E1441DD8D7E0690285515E6}

La velocidad de bits adaptable (ABR) está habilitada en el TVSDK de forma predeterminada. Puede utilizar la interfaz de usuario Configuración de Primetime para anular el comportamiento predeterminado de TVSDK en la implementación de referencia configurando el control ABR personalizado.

Para habilitar ABR personalizado a través de la interfaz de usuario Configuración:

* Abra el cuadro de diálogo Configuración de Primetime .
* Seleccione **[!UICONTROL ABR controls]**.

   ![](assets/abr-configuration.jpg)

* Pulse el control [!UICONTROL Enable ON] para que se muestre `OFF`.

El `PlaybackManager` solo establece los parámetros ABR si [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html) devuelve true (ON). Si devuelve false (OFF), el `PlaybackManager` utiliza el control ABR predeterminado, por lo que las tasas de bits inicial, mínima y máxima serán 0 y la directiva ABR será `ABR_MODERATE`.

## Configurar para tasas de bits bajas {#section_5451691CBBD24542AD54A474D222CD39}

Para algunas tasas de reproducción de velocidad de bits baja, el TVSDK, de forma predeterminada, cambia al flujo de solo audio y la reproducción aparece congelada. Puede configurar el reproductor para que nunca encuentre una situación en la que cambie a solo audio.

* Implemente la interfaz [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html):

* Asegúrese de que [getABRMinBitRate](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#getABRMinBitRate()) es mayor que la velocidad de bits de solo audio (superior a 64000).
* Asegúrese de que [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#isABRControlEnabled()) esté activado.