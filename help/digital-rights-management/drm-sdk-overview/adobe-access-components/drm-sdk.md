---
description: Los componentes principales de Primetime DRM constan de un SDK de Java y los entornos de tiempo de ejecución de cliente de Flash Player y Adobe AIR.
title: SDK de Java, Flash Player y cliente de Adobe AIR
exl-id: 5422d282-da9c-4810-a782-3c3af5fdeb3f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# SDK de DRM de Adobe Primetime {#section_522E57DFEEFF4794978FF2D366B83690}

Primetime DRM se entrega como un SDK de Java que proporciona los bloques de creación a partir de los cuales puede crear una implementación de servidor. Con el SDK puede crear una solución DRM de Primetime adecuada para el modelo empresarial de su organización.

Las API de Java proporcionadas en el SDK se describen en las siguientes subsecciones.

## API de Java para administrar dominios de grupo de dispositivos{#java-apis-for-managing-device-group-domains}

Estas API se utilizan para permitir que el servidor administre solicitudes de cliente para unirse y abandonar dominios de grupos de dispositivos.

Un dominio de grupo de dispositivos es una colección lógica de dispositivos que pueden compartir licencias entre sí. Para que esto suceda, cada dispositivo debe unirse/registrarse primero en el mismo dominio. El SDK de DRM de Primetime, que se ejecuta en un servidor, debe administrar las solicitudes de unión (registro) de dominio de dispositivo, así como las solicitudes de baja (anulación de registro) de dominio de dispositivo. Los dispositivos que no están unidos a ningún dominio recibirán licencias enlazadas a ese dispositivo, que no se podrán compartir con ningún otro.

## API de Java para proteger contenido{#java-apis-for-protecting-content}

Estas API se utilizan para definir derechos y preparar contenido para su distribución. Las API de protección de contenido son:

* Administración de directivas

   La API de administración de políticas se utiliza para crear y modificar las políticas que se aplican al contenido. Se pueden crear o actualizar directivas, incluida la obtención/configuración de todas las reglas de uso y la autorización de parámetros adicionales en un área de nombres personalizada.

* Empaquetado de contenido

   La API de empaquetado de contenido se utiliza para cifrar contenido y recuperar metadatos del contenido empaquetado.

## API de Java para la emisión de licencias{#java-apis-for-issuing-licenses}

Estas API se utilizan cuando un cliente solicita una licencia al servidor. El SDK admite las siguientes solicitudes del cliente:

* Autenticación

   La API de autenticación se puede utilizar para gestionar solicitudes de autenticación y generar tokens de autenticación.

* Generación y adquisición de licencias

   La API de generación y adquisición de licencias se utiliza para generar una licencia para el usuario.

* Compatibilidad con clientes y contenido de la versión 1.5 de Adobe AIR

   Con fines de compatibilidad con versiones anteriores, el SDK tiene API para gestionar solicitudes de aplicaciones de AIR creadas para utilizarlas con clientes de la versión 1.5 y anteriores de AIR, así como contenido protegido.

## Implementación de referencia {#reference-implementation}

El SDK incluye una implementación de referencia, una implementación simple de DRM de Adobe Primetime que muestra cómo utilizar las API de Java. La implementación de referencia proporciona un servidor de licencias, un empaquetador de carpetas inspeccionadas, una aplicación AIR de Primetime DRM Manager y herramientas de línea de comandos para el empaquetado de contenido y la administración de directivas basadas en las API de Java. Para obtener más información sobre la implementación de referencia de DRM de Primetime, consulte Protección del contenido.
