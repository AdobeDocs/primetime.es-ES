---
description: Puede configurar el reproductor para que lea las estadísticas de reproducción y dispositivo desde QoSProvider con la frecuencia necesaria.
seo-description: Puede configurar el reproductor para que lea las estadísticas de reproducción y dispositivo desde QoSProvider con la frecuencia necesaria.
seo-title: Mostrar estadísticas de dispositivos y reproducción de QoS
title: Mostrar estadísticas de dispositivos y reproducción de QoS
uuid: 8fc45a2f-03d4-4fa0-979b-eb816419c4f7
translation-type: tm+mt
source-git-commit: e1c6ab1d50f9262aaf70aef34854cf293fb4f30d
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---


# Mostrar estadísticas de dispositivos y reproducción de QoS {#display-qos-playback-and-device-statistics}

Puede configurar el reproductor para que lea las estadísticas de reproducción y dispositivo desde QoSProvider con la frecuencia necesaria.

La clase `QoSProvider` proporciona varias estadísticas, incluida la velocidad de fotogramas, la velocidad de bits de perfil, el tiempo total empleado en el almacenamiento en búfer, el número de intentos de almacenamiento en búfer, el tiempo que tardó en obtenerse el primer byte del primer fragmento de vídeo, el tiempo que tardó en procesarse el primer fotograma, la longitud almacenada en el búfer actualmente y el tiempo de búfer.

La implementación de referencia proporciona una clase `QoSManager` donde puede habilitar la visualización de la superposición de QoS. También puede activar la visibilidad de QoS en la interfaz de usuario Configuración:

![](assets/qos-configuration.jpg)

El `QoSManager` rastrea las estadísticas de QoS obteniendo información del dispositivo, adjuntándolas al reproductor de medios y actualizándolas con la información de QoS más reciente.

**Habilitar o deshabilitar el sistema de informes de estadísticas de QoS**

1. Cree un QosManager o habilite el sistema de informes de QoS mediante ManagerFactory.

   * Para crear un QosManager:
      * Esta aplicación necesita utilizar la función de flujo de trabajo de publicidad

   QoSManager qosManager = new QosManagerOn();

   * Para utilizar un ManagerFactory para habilitar la visualización de estadísticas de QoS:

   qosManager = ManagerFactory.getQosManager(
   <b>true</b>, config, mediaPlayer);

   >[!NOTE]
   >
   >Si se cambia el valor booleano a `false`, se deshabilita el sistema de informes de QoS.

2. Añadir oyentes de evento:

   `qosManager.addEventListener(qosManagerEventListener);`

3. Cree el proveedor de QoS y adjúntelo al contexto de actividad del reproductor:

   `qosManager.createQOSProvider(getActivity());`

   >[!NOTE]
   >
   >Cuando la actividad del reproductor vaya a destruirse, asegúrese de llamar a [qosManager.destroyQOSProvider](https://help.adobe.com/en_US/primetime/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html#destroyQOSProvider()) para limpiar el proveedor de QOS desconectándolo del reproductor de medios.

**Documentación de API relacionada**

* [QosManager de clase](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html)
* [Clase QosManagerOn](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManagerOn.html)
* [QosManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosManagerEventListener.html)
* [QosItem](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosItem.html)
