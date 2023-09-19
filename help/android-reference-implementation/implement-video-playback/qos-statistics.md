---
description: Puede configurar el reproductor para que lea las estadísticas de reproducción y del dispositivo del proveedor de QoS con la frecuencia necesaria.
title: Mostrar estadísticas de reproducción de QoS y de dispositivo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Mostrar estadísticas de reproducción de QoS y de dispositivo {#display-qos-playback-and-device-statistics}

Puede configurar el reproductor para que lea las estadísticas de reproducción y del dispositivo del proveedor de QoS con la frecuencia necesaria.

El `QoSProvider` proporciona varias estadísticas, incluida la velocidad de fotogramas, la velocidad de bits de perfil, el tiempo total empleado en el almacenamiento en búfer, el número de intentos de almacenamiento en búfer, el tiempo que se tardó en obtener el primer byte del primer fragmento de vídeo, el tiempo que se tardó en procesar el primer fotograma, la longitud almacenada actualmente en búfer y el tiempo de búfer.

La implementación de referencia proporciona un `QoSManager` donde puede habilitar la visualización de la superposición de QoS. También puede habilitar la visibilidad de QoS en la interfaz de usuario de Configuración:

![](assets/qos-configuration.jpg)

El `QoSManager` rastrea las estadísticas de QoS al obtener información del dispositivo, adjuntar al reproductor de medios y actualizar con la información de QoS más reciente.

**Habilitar o deshabilitar los informes de estadísticas de QoS**

1. Cree un QosManager o habilite los informes de QoS mediante ManagerFactory.

   * Para crear un QosManager:
      * Esta aplicación necesita utilizar la función de flujo de trabajo de publicidad

   QoSManager qosManager = new QosManagerOn();

   * Para utilizar un ManagerFactory para habilitar la visualización de estadísticas de QoS:

   qosManager = ManagerFactory.getQosManager()
   <b>true</b>, config, mediaPlayer);

   >[!NOTE]
   >
   >Cambiar el valor booleano a `false` deshabilita los informes de QoS.

2. Agregar detectores de eventos:

   `qosManager.addEventListener(qosManagerEventListener);`

3. Cree el proveedor de QoS y adjúntelo al contexto de actividad del reproductor:

   `qosManager.createQOSProvider(getActivity());`

   >[!NOTE]
   >
   >Cuando se vaya a destruir la actividad del reproductor, asegúrese de llamar a [qosManager.deleteQOSProvider](https://help.adobe.com/en_US/primetime/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html#destroyQOSProvider()) para limpiar el proveedor de QOS separándolo del reproductor de medios.

**Documentación de API relacionada**

* [Class QosManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html)
* [Class QosManagerOn](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManagerOn.html)
* [QosManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosManagerEventListener.html)
* [QosItem](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosItem.html)
