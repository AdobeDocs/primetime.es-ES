---
description: El TVSDK puede reproducir vídeos que tengan varios perfiles con diferentes velocidades de bits, cambiando entre ellos para proporcionar más de un nivel de calidad en función del ancho de banda disponible.
title: Varias velocidades de bits
exl-id: 5f71d69e-993a-4985-accd-7ce2104f837e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# Varias velocidades de bits {#multiple-bit-rates}

El TVSDK puede reproducir vídeos que tengan varios perfiles con diferentes velocidades de bits, cambiando entre ellos para proporcionar más de un nivel de calidad en función del ancho de banda disponible.

Puede establecer las velocidades de bits iniciales, mínimas y máximas, así como la directiva de conmutación de velocidad de bits adaptable (ABR) para un flujo de velocidad de bits múltiple (MBR). TVSDK cambia automáticamente a la velocidad de bits que proporciona la mejor experiencia de reproducción con la configuración especificada.

La implementación de referencia configura los siguientes parámetros ABR en [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html).

| Parámetro | Descripción |
|--- |--- |
| Velocidad de bits inicial: getABRInitialBitRate | La velocidad de bits de reproducción deseada (en bits por segundo) para el primer segmento. Cuando comienza la reproducción, se utiliza el perfil más cercano (igual o bueno que la velocidad de bits inicial) para el primer segmento.  Si se define una velocidad de bits mínima y la velocidad de bits inicial es inferior a la mínima, TVSDK selecciona el perfil con la velocidad de bits más baja por encima de la velocidad de bits mínima. Del mismo modo, si la tasa inicial está por encima de la tasa máxima, TVSDK selecciona la tasa más alta por debajo de la máxima. Si la velocidad de bits inicial es cero o indefinida, la velocidad de bits inicial viene determinada por la directiva ABR.  Devuelve un valor entero que representa el perfil de byte por segundo. |
| Velocidad de bits mínima: getABRMinBitRate | La velocidad de bits más baja permitida a la que ABR puede cambiar. La conmutación ABR ignora los perfiles con una velocidad de bits inferior a esta. Devuelve un valor entero que representa el perfil de bits por segundo. |
| Velocidad de bits máxima: getABRMaxBitRate | La velocidad de bits más alta permitida a la que ABR puede cambiar. La conmutación ABR ignora los perfiles con una velocidad de bits superior a esta. Devuelve un valor entero que representa el perfil de bits por segundo. |
| Política de cambio de ABR: getABRPolicy | La reproducción cambia gradualmente al perfil de velocidad de bits más alta cuando es posible. Puede establecer la directiva para el cambio ABR, que determina la rapidez con la que TVSDK cambia entre perfiles. El valor predeterminado es Moderar. <ul><li>*Conservadora*: cambia al perfil con la siguiente velocidad de bits más alta cuando el ancho de banda es un 50 % más alto que la velocidad de bits actual. </li><li>*Moderar*: cambia al siguiente perfil de velocidad de bits más alta cuando el ancho de banda es un 20 % mayor que la velocidad de bits actual.</li><li>*Agresiva*: cambia inmediatamente al perfil de velocidad de bits más alta cuando el ancho de banda es mayor que la velocidad de bits actual</li></ul><br/>Si la velocidad de bits inicial es cero o no se especifica y se especifica una directiva, la reproducción comienza con el perfil de velocidad de bits más bajo para Conservador, el perfil más cercano a la velocidad de bits media de los perfiles disponibles para Moderado y el perfil de velocidad de bits más alto para Agresivo.<br/><br/>La directiva funciona dentro de las restricciones de las tasas de bits mínima y máxima, si se especifican.  Devuelve el valor actual de la enumeración ABRControlParameters: <ul><li>ABR_CONSERVATIVE</li><li>ABR_MODERATE </li><li>ABR_AGRESIVO</li></ul><br>Consulte también [ABRPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/ABRControlParameters.ABRPolicy.html). |

>[!NOTE]
>
>* El mecanismo de conmutación por error de TVSDK puede anular esta configuración, ya que TVSDK prefiere una experiencia de reproducción continua en lugar de respetar estrictamente los parámetros de control.
>* Cuando la velocidad de bits cambia, el TVSDK se envía `onProfileChanged` eventos en `PlaybackEventListener`.


## Habilitar el control ABR personalizado en la implementación de referencia {#section_72A6E7263E1441DD8D7E0690285515E6}

La velocidad de bits adaptable (ABR) está habilitada en TVSDK de forma predeterminada. Puede utilizar la interfaz de usuario Configuración de Primetime para anular el comportamiento predeterminado de TVSDK en la implementación de referencia configurando el control ABR personalizado.

Para habilitar ABR personalizado a través de la interfaz de usuario Configuración:

* Abra el cuadro de diálogo Configuración de Primetime.
* Seleccionar **[!UICONTROL ABR controls]**.

   ![](assets/abr-configuration.jpg)

* Pulse el botón [!UICONTROL Enable ON] control para que se muestre `OFF`.

El `PlaybackManager` solo establece los parámetros ABR si [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html) devuelve true (ON). Si devuelve el valor &quot;false&quot; (OFF), la variable `PlaybackManager` utiliza el control ABR predeterminado para que las tasas de bits inicial, mínima y máxima sean todas 0 y la directiva ABR sea `ABR_MODERATE`.

## Configurar para tasas de bits bajas {#section_5451691CBBD24542AD54A474D222CD39}

Para algunas tasas de reproducción de velocidad de bits bajas, el TVSDK, de forma predeterminada, cambia al flujo de solo audio y la reproducción parece inmovilizada. Puede configurar el reproductor para que no se encuentre nunca con una situación en la que cambie a solo audio.

* Implementación de [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html) interfaz:

* Asegúrese de que [getABRMinBitRate](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#getABRMinBitRate()) es mayor que la velocidad de bits de sólo audio (mayor que 64000).
* Asegúrese de que [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#isABRControlEnabled()) está activado.
