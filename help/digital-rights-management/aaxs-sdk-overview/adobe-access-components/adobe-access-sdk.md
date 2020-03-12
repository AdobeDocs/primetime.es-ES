---
description: Los componentes principales de Adobe Access consisten en un SDK de Java y los entornos de tiempo de ejecución de cliente de Flash Player y Adobe AIR.
seo-description: Los componentes principales de Adobe Access consisten en un SDK de Java y los entornos de tiempo de ejecución de cliente de Flash Player y Adobe AIR.
seo-title: SDK de Java, Flash Player y cliente de Adobe AIR
title: SDK de Java, Flash Player y cliente de Adobe AIR
uuid: 6b6c5aa2-56ee-4476-a05b-dcbbe3b9001e
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Componentes de Adobe Access{#adobe-access-components}

Los componentes principales de Adobe Access consisten en un SDK de Java y los entornos de tiempo de ejecución de cliente de Flash Player y Adobe AIR.

Para obtener más información sobre la configuración del SDK, consulte Configuración del SDK en *Uso del SDK de Adobe Access para la protección de contenido.*

El SDK de Adobe Access le permite desarrollar una solución de administración de derechos digitales que se integra con la infraestructura empresarial existente de su organización, como la administración de contenido, la facturación y los sistemas de control de acceso de usuarios. Flash Player y Adobe AIR le permiten crear e implementar fácilmente aplicaciones a través de las cuales los consumidores pueden acceder y ver grandes bibliotecas de contenido digital.

## SDK de Adobe Access {#section_6AA3DC7BAE354472AE179BBC9AF6BD27}

Adobe Access se entrega como un SDK de Java que proporciona los componentes básicos desde los que puede crear una implementación de servidor. Con el SDK puede crear una solución de Adobe Access que se adapte al modelo empresarial de su organización.

Las API de Java proporcionadas en el SDK se describen en las siguientes subsecciones.

## API de Java para administrar dominios de grupos de dispositivos {#java-apis-for-managing-device-group-domains}

Estas API se utilizan para permitir que el servidor gestione solicitudes de cliente para unirse y salir de dominios de grupo de dispositivos.

Un dominio de grupo de dispositivos es una colección lógica de dispositivos que pueden compartir licencias entre sí. Para que esto suceda, cada dispositivo debe unirse/registrarse primero en el mismo dominio. El SDK de Adobe Access, que se ejecuta en un servidor, debe gestionar las solicitudes de inscripción (registro) del dominio del dispositivo, así como las solicitudes de salida (eliminación del registro) del dominio del dispositivo. Los dispositivos que no están unidos a ningún dominio recibirán licencias vinculadas a ese dispositivo, que no se pueden compartir con ningún otro dispositivo.

## API de Java para proteger contenido {#java-apis-for-protecting-content}

Estas API se utilizan para definir derechos y preparar el contenido para la distribución. Las API de protección de contenido son:

* Gestión de políticas

   La API de administración de políticas se utiliza para crear y modificar políticas que se aplicarán al contenido. Las políticas se pueden crear o actualizar, incluida la obtención o configuración de todas las reglas de uso y la posibilidad de usar parámetros adicionales en un espacio de nombres personalizado.

* Empaquetado de contenido

   La API de empaquetado de contenido se utiliza para cifrar contenido y recuperar metadatos del contenido empaquetado.

## API de Java para la emisión de licencias {#java-apis-for-issuing-licenses}

Estas API se utilizan cuando un cliente solicita una licencia del servidor. El SDK admite las siguientes solicitudes del cliente:

* Autenticación

   La API de autenticación se puede utilizar para gestionar solicitudes de autenticación y generar tokens de autenticación.

* Generación y adquisición de licencias

   La API de generación y adquisición de licencias se utiliza para generar una licencia para el usuario.

* Compatibilidad con el contenido y los clientes de Adobe AIR versión 1.5

   Para lograr la compatibilidad con versiones anteriores, el SDK dispone de API para gestionar solicitudes de aplicaciones de AIR creadas para su uso con la versión 1.5 de AIR y clientes anteriores y contenido protegido.

## Implementación de referencia {#reference-implementation}

El SDK incluye una implementación de referencia, una implementación sencilla de Adobe Access que muestra cómo utilizar las API de Java. La implementación de referencia proporciona un servidor de licencias, un empaquetador de carpetas vigiladas, una aplicación de AIR de Adobe Access Manager y herramientas de línea de comandos para empaquetar contenido y administrar políticas en función de las API de Java. Para obtener más información sobre la implementación de referencia de Adobe Access, consulte *Protección de contenido*.

## Adobe Access Server para flujo continuo protegido {#adobe-access-server-for-protected-streaming}

En los casos de uso de flujo continuo en los que el contenido está protegido con Adobe Access, como en el caso del flujo dinámico HTTP de Adobe, el software también incluye Adobe Access Server para el flujo protegido. Esta solución se puede implementar fácilmente en un contenedor servlet como Tomcat y puede lograr un alto nivel de escalabilidad y rendimiento para satisfacer las mayores necesidades de distribución de contenido.

## Adobe Flash Player {#adobe-flash-player}

Flash Player es un complemento y un tiempo de ejecución de navegador ligero que ofrece una experiencia de usuario coherente y atractiva, una reproducción de audio y vídeo impresionante y un alcance generalizado. Flash Player ofrece una reproducción de alta calidad del contenido de vídeo descargado o transmitido por flujo continuo. Para los editores de contenido, Flash Player proporciona los medios para personalizar las pantallas de reproducción que rodean el contenido, lo que permite una mayor monetización y experiencias de marca mediante la publicidad mediante pancartas y superposiciones. Para los consumidores, Flash Player presenta una manera intuitiva y atractiva de ver el contenido de vídeo.

Para obtener más información sobre Flash Player, visite: [www.adobe.com/go/flashplayer](https://www.adobe.com/go/flashplayer)

## Adobe AIR {#adobe-air}

Adobe AIR es un motor de ejecución de varios sistemas operativos que permite a los productores de contenido ampliar sus inversiones existentes en la web al escritorio mediante el diseño de aplicaciones multimedia personalizadas. Basado en tecnologías de eficacia probada y abierta, ofrece a las empresas una forma fiable y simplificada de desarrollar e implementar aplicaciones personalizadas en las que se puede confiar para ofrecer una experiencia de usuario más segura y agradable. Adobe AIR permite a las empresas integrar fácilmente medios enriquecidos para crear una experiencia de usuario más envolvente e interactiva. Permite a los desarrolladores utilizar herramientas conocidas como el software HTML, JavaScript, Flash o Adobe® Flex® para implementar su combinación única de aplicaciones de Internet enriquecidas en Windows, Macintosh o Linux.

Las empresas tienen un control total de la interfaz de usuario y pueden diseñar una experiencia de usuario para reflejar y reforzar su marca. Gracias a la compatibilidad integrada con la reproducción de contenido protegido con el SDK de Adobe Access, Adobe AIR ayuda a crear cadenas de distribución de contenido personalizadas y completas.

Para obtener más información sobre Adobe AIR, visite: [www.adobe.com/go/air](https://www.adobe.com/go/air)

## Aplicaciones nativas de iOS y Android {#native-ios-and-android-applications}

Aplicaciones nativas de iOS y Android Disponibles solo para clientes de Adobe Primetime, Adobe Access DRM 4.0 y versiones posteriores se pueden usar para proteger vídeos que se consumen en aplicaciones nativas (no Flash) en dispositivos móviles. Para que una aplicación consuma este contenido protegido, debe implementarse mediante las bibliotecas del cliente Adobe Primetime.

Para obtener más información sobre Adobe Primetime, visite: [https://www.adobe.com/solutions/primetime.html](https://www.adobe.com/solutions/primetime.html)