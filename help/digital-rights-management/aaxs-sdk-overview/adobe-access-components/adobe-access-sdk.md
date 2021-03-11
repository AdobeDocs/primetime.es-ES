---
description: Los componentes principales de Adobe Access consisten en un SDK de Java y los entornos de tiempo de ejecución del cliente de Flash Player y Adobe AIR.
title: SDK de Java, Flash Player y cliente de Adobe AIR
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---


# Componentes de acceso al Adobe{#adobe-access-components}

Los componentes principales de Adobe Access consisten en un SDK de Java y los entornos de tiempo de ejecución del cliente de Flash Player y Adobe AIR.

Para obtener más información sobre la configuración del SDK, consulte Configuración del SDK en *Uso del SDK de acceso al Adobe para la protección de contenido.*

El SDK de acceso a Adobe le permite desarrollar una solución de administración de derechos digitales que se integra con la infraestructura empresarial existente de su organización, como la administración de contenido, la facturación y los sistemas de control de acceso de los usuarios. Flash Player y Adobe AIR le permiten crear e implementar fácilmente aplicaciones a través de las cuales los consumidores pueden acceder y ver grandes bibliotecas de contenido digital.

## SDK de acceso al Adobe {#section_6AA3DC7BAE354472AE179BBC9AF6BD27}

Adobe Access se entrega como un SDK de Java que proporciona los componentes básicos desde los que puede crear una implementación de servidor. Con el SDK puede crear una solución de acceso a Adobe adecuada para el modelo empresarial de su organización.

Las API de Java proporcionadas en el SDK se describen en las siguientes subsecciones.

## API de Java para administrar dominios de grupos de dispositivos {#java-apis-for-managing-device-group-domains}

Estas API se utilizan para permitir que el servidor gestione las solicitudes de cliente para unirse a dominios de grupo de dispositivos y salir de ellos.

Un dominio de grupo de dispositivos es una colección lógica de dispositivos que pueden compartir licencias entre sí. Para que esto suceda, cada dispositivo debe unirse/registrarse primero en el mismo dominio. El SDK de acceso a Adobe, que se ejecuta en un servidor, debe gestionar las solicitudes de unión (registro) del dominio del dispositivo, así como las solicitudes de baja (anulación del registro) del dominio del dispositivo. Los dispositivos que no están unidos a ningún dominio recibirán licencias vinculadas a ese dispositivo, que no se pueden compartir con ningún otro dispositivo.

## API de Java para proteger contenido {#java-apis-for-protecting-content}

Estas API se utilizan para definir derechos y preparar el contenido para la distribución. Las API de protección de contenido son:

* Gestión de políticas

   La API de administración de directivas se utiliza para crear y modificar políticas que se aplicarán al contenido. Se pueden crear o actualizar directivas, incluida la obtención o configuración de todas las reglas de uso y la posibilidad de usar parámetros adicionales en un espacio de nombres personalizado.

* Paquete de contenido

   La API de paquetes de contenido se utiliza para cifrar contenido y recuperar metadatos del contenido empaquetado.

## API de Java para emitir licencias {#java-apis-for-issuing-licenses}

Estas API se utilizan cuando un cliente solicita una licencia del servidor. El SDK admite las siguientes solicitudes del cliente:

* Autenticación

   La API de autenticación se puede utilizar para gestionar solicitudes de autenticación y generar tokens de autenticación.

* Generación y adquisición de licencias

   La API de generación y adquisición de licencias se utiliza para generar una licencia para el usuario.

* Compatibilidad con clientes y contenido de la versión 1.5 de Adobe AIR

   Con fines de compatibilidad con versiones anteriores, el SDK tiene API para gestionar solicitudes de aplicaciones de AIR creadas para su uso con clientes de AIR versión 1.5 y anteriores y contenido protegido.

## Implementación de referencia {#reference-implementation}

El SDK incluye una implementación de referencia, una implementación de acceso a Adobe sencilla que muestra cómo utilizar las API de Java. La implementación de referencia proporciona un servidor de licencias, un paquete de carpetas vigiladas, una aplicación de AIR de Adobe Access Manager y herramientas de línea de comandos para empaquetar contenido y administrar políticas en función de las API de Java. Para obtener más información sobre la implementación de referencia de Acceso a Adobe, consulte *Protección de contenido*.

## Adobe Access Server para transmisión protegida {#adobe-access-server-for-protected-streaming}

Para los casos de uso de flujo continuo en los que el contenido está protegido con Acceso a Adobe, como para el HTTP Dynamic Streaming de Adobe, el software también incluye Adobe Access Server para transmisión protegida. Esta solución se puede implementar fácilmente en un contenedor de servlet como Tomcat y puede lograr un alto nivel de escalabilidad y rendimiento para satisfacer las necesidades de distribución de contenido más grandes.

## Flash Player de Adobe {#adobe-flash-player}

El Flash Player es un complemento y un tiempo de ejecución ligeros del navegador que ofrece experiencias de usuario coherentes y atractivas, una impresionante reproducción de audio/vídeo y un alcance generalizado. Flash Player proporciona una reproducción de alta calidad del contenido de vídeo descargado o transmitido. Para los editores de contenido, Flash Player proporciona los medios para personalizar las pantallas de reproducción que rodean el contenido, lo que permite experiencias de marca y monetización más profundas a través de la publicidad mediante banners y superposiciones. Para los consumidores, Flash Player presenta una forma intuitiva y visualmente atractiva de ver el contenido de vídeo.

Para obtener más información sobre el Flash Player, visite: [www.adobe.com/go/flashplayer](https://www.adobe.com/go/flashplayer)

## Adobe AIR {#adobe-air}

Adobe AIR es un motor de ejecución de sistemas que permite a los productores de contenido ampliar sus inversiones existentes en la web al escritorio mediante el diseño de aplicaciones multimedia personalizadas. Basado en tecnologías abiertas y probadas, proporciona una forma fiable y simplificada para que las empresas desarrollen e implementen aplicaciones personalizadas en las que se pueda confiar para ofrecer una experiencia de usuario más segura y agradable. Adobe AIR permite a las empresas integrar fácilmente medios enriquecidos para crear una experiencia de usuario más inmersiva e interactiva. Permite a los desarrolladores utilizar herramientas conocidas como HTML, JavaScript, Flash o software de Flex® Adobe® para implementar su combinación única de aplicaciones de Internet enriquecidas en Windows, Macintosh o Linux.

Las empresas tienen un control total de la interfaz de usuario y pueden diseñar una experiencia de usuario para reflejar y reforzar su marca. Gracias a la compatibilidad integrada con la reproducción de contenido protegido con el SDK de acceso a Adobe, Adobe AIR ayuda a crear cadenas de distribución de contenido personalizadas y completas.

Para obtener más información sobre Adobe AIR, visite: [www.adobe.com/go/air](https://www.adobe.com/go/air)

## Aplicaciones nativas de iOS y Android {#native-ios-and-android-applications}

Aplicaciones nativas de iOS y Android Disponible solo para clientes de Adobe Primetime, el acceso a Adobe DRM 4.0 y posteriores se puede utilizar para proteger el vídeo que se consume en aplicaciones nativas (que no sean de Flash) en dispositivos móviles. Para que una aplicación consuma este contenido protegido, debe implementarse mediante las bibliotecas de cliente de Adobe Primetime.

Para obtener más información sobre Adobe Primetime, visite: [https://www.adobe.com/solutions/primetime.html](https://www.adobe.com/solutions/primetime.html)