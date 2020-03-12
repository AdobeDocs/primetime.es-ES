---
seo-title: Administradores de funciones
title: Administradores de funciones
uuid: 3d78544e-4819-4122-bfd3-01522a067aa9
description: Los administradores de funciones le permiten controlar funciones individuales sin recorrer todo el TVSDK en busca de código para una función que se pueda dispersar en varias ubicaciones.
seo-description: Los administradores de funciones le permiten controlar funciones individuales sin recorrer todo el TVSDK en busca de código para una función que se pueda dispersar en varias ubicaciones.
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Administradores de funciones {#feature-managers}

Los administradores de funciones le permiten controlar funciones individuales sin recorrer todo el TVSDK en busca de código para una función que se pueda dispersar en varias ubicaciones. Los administradores de funciones condensan el código en una clase por función. Los administradores de funciones esperan activadores de eventos TVSDK y luego informan a la clase que utiliza el administrador de funciones para controlar el resultado. El administrador de funciones proporciona la información necesaria a la clase.

Los administradores de funciones realizan las siguientes tareas:

* **Activa las funciones de TVSDK.**
Son llamadas a funciones para activar una función TVSDK. Por ejemplo, `PlaybackManager.play()` se llama cuando la aplicación del reproductor necesita iniciar la reproducción del vídeo.

* **Escucha eventos TVSDK.**
El administrador de funciones debe escuchar los eventos TVSDK para obtener información del TVSDK. Por ejemplo, `AdsManager` escucha los eventos de anuncios de TVSDK para que se le notifique cuando se inicien las pausas publicitarias.

* **Distribuye eventos al controlador.**
Una vez que los administradores de funciones reciben y procesan los eventos del TVSDK, notifican al cliente que debe gestionar el evento. Por ejemplo, después de `AdsManager` recibir un evento de inicio de pausa publicitaria, indica al fragmento del reproductor que refleje este cambio en la interfaz de usuario (deshabilite la barra de desplazamiento, muestre la superposición de publicidad, etc.).

La implementación de referencia de Primetime incluye los siguientes administradores de funciones:

| Administrador de funciones | Archivo predeterminado | Función |  |
|---|---|---|---|
| Reproducción de vídeo | PlaybackManager | Reproducción y control HLS, reproducción y control DVR, control de búfer y gestión de velocidad de bits múltiple. | Requerido |
| Protección de contenido DRM | DrmManager | Protección del contenido. | Requerido |
| Inserción de publicidad | AdsManager | Inserción de publicidad, incluido Adobe Primetime y toma de decisiones sobre la pausa publicitaria directa, y pausa publicitaria personalizada. | Opcional |
| Subtítulos opcionales | CCManager | Subtítulos opcionales y subtítulos VTT. | Opcional |
| Enlace tardío de audio | AAManager | Enlace de audio tardío. | Opcional |
| QoS | QosManager | Estadísticas de QoS. | Opcional |
| Asignación de derechos | EntitlementManager | Integración de la asignación de derechos de autenticación Primetime. | Opcional |

La implementación de referencia contiene clases predeterminadas básicas, enumeradas arriba, y clases correspondientes con el sufijo Activado. Las clases predeterminadas proporcionan los comportamientos TVSDK predeterminados, mientras que las clases con el sufijo Activado incluyen todo el código necesario para activar la función TVSDK y escuchar los eventos TVSDK para esa función.

* Para las funciones opcionales, el código predeterminado funciona como si la función estuviera desactivada.
* Las clases con el sufijo Activado funcionan como si la función estuviera activada.