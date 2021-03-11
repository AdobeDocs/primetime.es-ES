---
description: Los componentes principales de Primetime DRM constan de un SDK de Java y los entornos de tiempo de ejecución del cliente de Flash Player y Adobe AIR.
title: SDK de Java, Flash Player y cliente de Adobe AIR
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# SDK de Adobe Primetime DRM {#section_522E57DFEEFF4794978FF2D366B83690}

Primetime DRM se entrega como un SDK de Java que proporciona los componentes básicos a partir de los cuales puede crear una implementación de servidor. Con el SDK puede crear una solución de DRM de Primetime adecuada para el modelo empresarial de su organización.

Las API de Java proporcionadas en el SDK se describen en las siguientes subsecciones.

## API de Java para administrar dominios de grupos de dispositivos{#java-apis-for-managing-device-group-domains}

Estas API se utilizan para permitir que el servidor gestione las solicitudes de cliente para unirse a dominios de grupo de dispositivos y salir de ellos.

Un dominio de grupo de dispositivos es una colección lógica de dispositivos que pueden compartir licencias entre sí. Para que esto suceda, cada dispositivo debe unirse/registrarse primero en el mismo dominio. El SDK de DRM de Primetime, que se ejecuta en un servidor, debe gestionar las solicitudes de unión (registro) del dominio del dispositivo, así como las solicitudes de baja (anulación del registro) del dominio del dispositivo. Los dispositivos que no están unidos a ningún dominio recibirán licencias vinculadas a ese dispositivo, que no se pueden compartir con ningún otro dispositivo.

## API de Java para proteger contenido{#java-apis-for-protecting-content}

Estas API se utilizan para definir derechos y preparar el contenido para la distribución. Las API de protección de contenido son:

* Gestión de políticas

   La API de administración de directivas se utiliza para crear y modificar políticas que se aplicarán al contenido. Se pueden crear o actualizar directivas, incluida la obtención o configuración de todas las reglas de uso y la posibilidad de usar parámetros adicionales en un espacio de nombres personalizado.

* Paquete de contenido

   La API de paquetes de contenido se utiliza para cifrar contenido y recuperar metadatos del contenido empaquetado.

## API de Java para emitir licencias{#java-apis-for-issuing-licenses}

Estas API se utilizan cuando un cliente solicita una licencia del servidor. El SDK admite las siguientes solicitudes del cliente:

* Autenticación

   La API de autenticación se puede utilizar para gestionar solicitudes de autenticación y generar tokens de autenticación.

* Generación y adquisición de licencias

   La API de generación y adquisición de licencias se utiliza para generar una licencia para el usuario.

* Compatibilidad con clientes y contenido de la versión 1.5 de Adobe AIR

   Con fines de compatibilidad con versiones anteriores, el SDK tiene API para gestionar solicitudes de aplicaciones de AIR creadas para su uso con clientes de AIR versión 1.5 y anteriores y contenido protegido.

## Implementación de referencia {#reference-implementation}

El SDK incluye una implementación de referencia, una implementación sencilla de Adobe Primetime DRM que muestra cómo utilizar las API de Java. La implementación de referencia proporciona un servidor de licencias, un paquete de carpetas vigiladas, una aplicación de AIR de Primetime DRM Manager y herramientas de línea de comandos para el empaquetado de contenido y la administración de políticas basadas en las API de Java. Para obtener más información sobre la implementación de referencia de DRM de Primetime, consulte Protección de contenido.