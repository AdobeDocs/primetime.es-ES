---
description: Puede configurar el reproductor para que lea las estadísticas de reproducción y dispositivo desde QoSProvider con la frecuencia necesaria.
title: Mostrar las estadísticas de dispositivo y reproducción de QoS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---


# Mostrar las estadísticas de dispositivos y reproducción de QoS {#display-qos-playback-and-device-statistics}

Puede configurar el reproductor para que lea las estadísticas de reproducción y dispositivo desde QoSProvider con la frecuencia necesaria.

La clase `QoSProvider` proporciona varias estadísticas, incluida la velocidad de fotogramas, la velocidad de bits del perfil, el tiempo total empleado en el almacenamiento en búfer, el número de intentos de almacenamiento en búfer, el tiempo que se tardó en obtener el primer byte del primer fragmento de vídeo, el tiempo que se tardó en procesar el primer fotograma, la longitud en búfer y el tiempo de búfer.

La implementación de referencia proporciona una clase `QoSManager` donde puede habilitar la visualización de la superposición de QoS. También puede habilitar la visibilidad de QoS en la interfaz de usuario Configuración :

![](assets/qos-configuration.jpg)

El `QoSManager` rastrea las estadísticas de QoS obteniendo información del dispositivo, adjuntándolas al reproductor multimedia y actualizándolas con la información de QoS más reciente.

**Habilitar o deshabilitar el informe de estadísticas de QoS**

1. Cree un QosManager o habilite los informes de QoS mediante el ManagerFactory.

   * Para crear un QosManager:
      * Esta aplicación necesita utilizar la función de flujo de trabajo de publicidad

   QoSManager qosManager = new QosManagerOn();

   * Para utilizar un ManagerFactory para habilitar la visualización de las estadísticas de QoS:

   qosManager = ManagerFactory.getQosManager(
   <b>true</b>, config, mediaPlayer);

   >[!NOTE]
   >
   >Si se cambia el booleano a `false` , se deshabilita el informe de QoS.

2. Agregar oyentes de eventos:

   `qosManager.addEventListener(qosManagerEventListener);`

3. Cree el proveedor de QoS y adjúntelo al contexto de actividad del reproductor:

   `qosManager.createQOSProvider(getActivity());`

   >[!NOTE]
   >
   >Cuando la actividad del reproductor se vaya a destruir, asegúrese de llamar a [qosManager.destroyQOSProvider](https://help.adobe.com/en_US/primetime/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html#destroyQOSProvider()) para limpiar el proveedor de QOS desconectándolo del reproductor de medios.

**Documentación de API relacionada**

* [QosManager de clase](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html)
* [Clase QosManagerOn](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManagerOn.html)
* [QosManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosManagerEventListener.html)
* [QosItem](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosItem.html)
