---
title: Administradores de funciones
description: Los administradores de funciones proporcionan una forma de controlar las funciones individuales sin atravesar todo el SDK de TVSDK en busca de código para una función que podría estar dispersa en varias ubicaciones.
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Administradores de funciones {#feature-managers}

Los administradores de funciones proporcionan una forma de controlar las funciones individuales sin atravesar todo el SDK de TVSDK en busca de código para una función que podría estar dispersa en varias ubicaciones. Los administradores de características condensan el código en una clase por característica. Los administradores de características esperan los déclencheur de los eventos de TVSDK y, a continuación, informan a la clase que utiliza el administrador de características para controlar el resultado. El administrador de funciones proporciona la información necesaria a la clase.

Los administradores de funciones realizan las siguientes tareas:

* **Funciones de Déclencheur TVSDK.**
Son llamadas a funciones para almacenar en déclencheur una función de TVSDK. Por ejemplo, `PlaybackManager.play()` se invoca cuando la aplicación de reproducción necesita iniciar la reproducción del vídeo.

* **Escucha eventos de TVSDK.**
El administrador de funciones debe escuchar los eventos de TVSDK para adquirir información del TVSDK. Por ejemplo, `AdsManager` escucha eventos de TVSDK Ads para recibir notificaciones cuando se inician las pausas publicitarias.

* **Envía eventos al controlador.**
Una vez que los administradores de funciones reciben y procesan los eventos del TVSDK, notifican al lado del cliente para que se ocupe del evento. Por ejemplo, después de `AdsManager` recibe un evento de inicio de pausa publicitaria, indica al fragmento del reproductor que refleje este cambio en la interfaz de usuario (deshabilite la barra de desplazamiento, muestre la superposición de publicidad, etc.).

La implementación de referencia de Primetime incluye los siguientes administradores de funciones:

| Administrador de funciones | Archivo predeterminado | Función |  |
|---|---|---|---|
| Reproducción de vídeo | PlaybackManager | Reproducción y control de HLS, reproducción y control de DVR, control de búfer y gestión de velocidad de bits múltiples. | Requerido |
| Protección de contenido DRM | DrmManager | Protección de contenido. | Requerido |
| Inserción de publicidad | AdsManager | Inserción de publicidad, incluido Adobe Primetime ad decisioning, pausa publicitaria directa y pausa publicitaria personalizada. | Opcional |
| Subtítulos opcionales | CCManager | Subtítulos opcionales y subtítulos VTT. | Opcional |
| Audio de enlace tardío | Administrador AAM | Audio de enlace tardío. | Opcional |
| QoS | QosManager | Estadísticas de QoS. | Opcional |
| Derecho | EntitlementManager | Integración de derechos de autenticación de Primetime. | Opcional |

La implementación de referencia contiene clases predeterminadas básicas, enumeradas anteriormente, y clases correspondientes con el sufijo Activado. Las clases predeterminadas proporcionan los comportamientos predeterminados de TVSDK, mientras que las clases con el sufijo Activado incluyen todo el código necesario para almacenar en déclencheur la función TVSDK y escuchar los eventos de TVSDK para esa función.

* Para las funciones opcionales, el código predeterminado funciona como si la función estuviera desactivada.
* Las clases con el sufijo Activado funcionan como si la característica estuviera activada.
