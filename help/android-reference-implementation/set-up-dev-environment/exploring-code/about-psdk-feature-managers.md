---
title: Administradores de funciones
description: Los administradores de funciones permiten controlar funciones individuales sin recorrer todo el TVSDK en busca de código para una función que se pueda distribuir en varias ubicaciones.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 2%

---


# Administradores de funcionalidades {#feature-managers}

Los administradores de funciones permiten controlar funciones individuales sin recorrer todo el TVSDK en busca de código para una función que se pueda distribuir en varias ubicaciones. Los administradores de funciones condensan el código en una clase por función. Los administradores de funciones esperan déclencheur de los eventos de TVSDK y luego informan a la clase que utiliza el administrador de funciones para controlar el resultado. El administrador de funciones proporciona la información necesaria a la clase.

Los administradores de funciones realizan las siguientes tareas:

* **Funciones de TVSDK de Déclencheur.**
Son llamadas a funciones para almacenar en déclencheur una función TVSDK. Por ejemplo, 
`PlaybackManager.play()` cuando la aplicación del reproductor necesita iniciar la reproducción de vídeo.

* **Escucha eventos TVSDK.**
El administrador de funciones debe escuchar los eventos TVSDK para adquirir información del TVSDK. Por ejemplo, 
`AdsManager` escucha eventos de TVSDK Ads para recibir notificaciones cuando se inicie una pausa publicitaria.

* **Envía eventos al controlador.**
Una vez que los administradores de funciones reciben y procesan los eventos del SDK de TVSDK, lo notifican al cliente para que gestione el evento. Por ejemplo, después de 
`AdsManager` recibe un evento de inicio de pausa publicitaria, le indica al fragmento del reproductor que refleje este cambio en la interfaz de usuario (desactive la barra de desplazamiento, muestre la superposición de publicidad, etc.).

La implementación de referencia de Primetime incluye los siguientes administradores de funciones:

| Gestor de funciones | Archivo predeterminado | Función |  |
|---|---|---|---|
| Reproducción de vídeo | PlaybackManager | Reproducción y control HLS, reproducción y control DVR, control de búfer y gestión de velocidad de bits múltiples. | Requerido |
| Protección de contenido DRM | DrmManager | Protección de contenido. | Requerido |
| Inserción de publicidad | AdsManager | Inserción de publicidad, incluida la pausa publicitaria directa en Adobe Primetime y en, y la pausa publicitaria personalizada. | Opcional |
| Subtítulos | CCManager | Subtítulos opcionales y VTT. | Opcional |
| Audio de enlace tardío | AAManager | Audio de enlace tardío. | Opcional |
| QoS | QosManager | Estadísticas de QoS. | Opcional |
| Derecho | EntitlementManager | Integración de derechos de autenticación de Primetime. | Opcional |

La implementación de referencia contiene clases predeterminadas básicas, enumeradas arriba, y clases correspondientes con el sufijo Activado. Las clases predeterminadas proporcionan los comportamientos TVSDK predeterminados, mientras que las clases con el sufijo On incluyen todo el código necesario para almacenar en déclencheur la función TVSDK y escuchar los eventos TVSDK para esa función.

* Para las funciones opcionales, el código predeterminado funciona como si la función estuviera desactivada.
* Las clases con el sufijo Activado funcionan como si la función estuviera activada.