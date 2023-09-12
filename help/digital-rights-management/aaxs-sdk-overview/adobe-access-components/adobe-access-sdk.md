---
description: Los componentes principales de Acceso a Adobe constan de un SDK de Java y los entornos de tiempo de ejecución de cliente de Flash Player y Adobe AIR.
title: SDK de Java, Flash Player y cliente de Adobe AIR
exl-id: 2df4da13-8df9-442b-8638-317c41d62fbe
source-git-commit: 8d7a4f69a6400b0c3242d4cb0c5daac81f27db3a
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---

# Componentes de Adobe Access{#adobe-access-components}

Los componentes principales de Acceso a Adobe constan de un SDK de Java y los entornos de tiempo de ejecución de cliente de Flash Player y Adobe AIR.

Para obtener más información sobre la configuración del SDK, consulte Configuración del SDK en *Uso del SDK de acceso a Adobe para proteger el contenido.*

El SDK de acceso a Adobe le permite desarrollar una solución de administración de derechos digitales que se integra con la infraestructura empresarial existente de su organización, como la administración de contenido, la facturación y los sistemas de control de acceso de los usuarios. Flash Player y Adobe AIR le permiten crear e implementar fácilmente aplicaciones a través de las cuales los consumidores pueden acceder y ver grandes bibliotecas de contenido digital.

## SDK de acceso a Adobe {#section_6AA3DC7BAE354472AE179BBC9AF6BD27}

El acceso a Adobe se entrega como un SDK de Java que proporciona los componentes básicos desde los que puede crear una implementación de servidor. Con el SDK puede crear una solución de acceso a Adobe adecuada para el modelo empresarial de su organización.

Las API de Java proporcionadas en el SDK se describen en las siguientes subsecciones.

## API de Java para administrar dominios de grupo de dispositivos {#java-apis-for-managing-device-group-domains}

Estas API se utilizan para permitir que el servidor administre solicitudes de cliente para unirse y abandonar dominios de grupos de dispositivos.

Un dominio de grupo de dispositivos es una colección lógica de dispositivos que pueden compartir licencias entre sí. Para que esto suceda, cada dispositivo debe unirse/registrarse primero en el mismo dominio. El SDK de acceso a Adobe, que se ejecuta en un servidor, debe administrar las solicitudes de unión (registro) al dominio de dispositivo, así como las solicitudes de baja (anulación de registro) del dominio de dispositivo. Los dispositivos que no están unidos a ningún dominio recibirán licencias enlazadas a ese dispositivo, que no se podrán compartir con ningún otro.

## API de Java para proteger contenido {#java-apis-for-protecting-content}

Estas API se utilizan para definir derechos y preparar contenido para su distribución. Las API de protección de contenido son:

* Administración de directivas

  La API de administración de políticas se utiliza para crear y modificar las políticas que se aplican al contenido. Se pueden crear o actualizar directivas, incluida la obtención/configuración de todas las reglas de uso y la autorización de parámetros adicionales en un área de nombres personalizada.

* Empaquetado de contenido

  La API de empaquetado de contenido se utiliza para cifrar contenido y recuperar metadatos del contenido empaquetado.

## API de Java para la emisión de licencias {#java-apis-for-issuing-licenses}

Estas API se utilizan cuando un cliente solicita una licencia al servidor. El SDK admite las siguientes solicitudes del cliente:

* Autenticación

  La API de autenticación se puede utilizar para gestionar solicitudes de autenticación y generar tokens de autenticación.

* Generación y adquisición de licencias

  La API de generación y adquisición de licencias se utiliza para generar una licencia para el usuario.

* Compatibilidad con clientes y contenido de la versión 1.5 de Adobe AIR

  Con fines de compatibilidad con versiones anteriores, el SDK tiene API para gestionar solicitudes de aplicaciones de AIR creadas para utilizarlas con clientes de la versión 1.5 y anteriores de AIR, así como contenido protegido.

## Implementación de referencia {#reference-implementation}

El SDK incluye una implementación de referencia, una implementación sencilla de Acceso a Adobe que muestra cómo utilizar las API de Java. La implementación de referencia proporciona un servidor de licencias, un empaquetador de carpetas inspeccionadas, una aplicación AIR de Adobe Access Manager y herramientas de línea de comandos para el empaquetado de contenido y la administración de directivas basadas en las API de Java. Para obtener más información sobre la implementación de referencia de Acceso a Adobe, consulte *Protección del contenido*.

## Adobe Access Server para flujo protegido {#adobe-access-server-for-protected-streaming}

Para los casos de uso de streaming en los que el contenido está protegido con Acceso de Adobe, como para el HTTP Dynamic Streaming de Adobe, el software también incluye Adobe Access Server para Flujo protegido. Esta solución se puede implementar fácilmente en un contenedor de servlets como Tomcat y puede lograr un alto nivel de escalabilidad y rendimiento para satisfacer las mayores necesidades de distribución de contenido.

## Flash Player de Adobe {#adobe-flash-player}

Flash Player es un complemento ligero para explorador y tiempo de ejecución que ofrece experiencias de usuario coherentes y atractivas, una reproducción de audio/vídeo impresionante y un alcance dominante. El Flash Player de proporciona una reproducción de alta calidad del contenido de vídeo transmitido o descargado. Para los editores de contenido, el Flash Player proporciona los medios para personalizar las pantallas de reproducción que rodean el contenido, lo que permite experiencias de promoción de la marca más profundas y monetización mediante la publicidad mediante titulares y superposiciones. Para los consumidores, el Flash Player presenta una forma intuitiva y visualmente atractiva de ver el contenido de vídeo.

Para obtener más información sobre el Flash Player, visite: [www.adobe.com/go/flashplayer](https://www.adobe.com/go/flashplayer)

## Adobe AIR {#adobe-air}

Adobe AIR es un motor en tiempo de ejecución de varios sistemas operativos que permite a los productores de contenido ampliar sus inversiones existentes en la web al escritorio mediante el diseño de aplicaciones multimedia personalizadas. Basado en tecnologías abiertas de probada eficacia, ofrece una forma fiable y simplificada para que las empresas desarrollen e implementen aplicaciones personalizadas en las que se pueda confiar para ofrecer una experiencia de usuario más segura y agradable. Adobe AIR permite a las empresas integrar fácilmente medios enriquecidos para crear una experiencia de usuario más envolvente e interactiva. Permite a los desarrolladores utilizar herramientas conocidas como software de Flex® de HTML, JavaScript, Flash o Adobe ® para implementar su combinación única de aplicaciones de Internet enriquecidas en Windows, Macintosh o Linux.

Las empresas tienen un control completo de la interfaz de usuario y pueden diseñar una experiencia de usuario para reflejar y reforzar su marca. Con compatibilidad integrada para la reproducción de contenido protegido con el SDK de acceso a Adobe, Adobe AIR ayuda a crear cadenas de distribución de contenido personalizadas y de extremo a extremo.

## Aplicaciones nativas de iOS y Android {#native-ios-and-android-applications}

Aplicaciones nativas de iOS y Android Disponible solo para clientes de Adobe Primetime, Adobe Access DRM 4.0 y versiones posteriores se puede utilizar para proteger el vídeo que se consume dentro de aplicaciones nativas (que no son de Flash) en dispositivos móviles. Para que una aplicación consuma este contenido protegido, debe implementarse mediante las bibliotecas del cliente de Adobe Primetime.

Para obtener más información sobre Adobe Primetime, visite: [https://www.adobe.com/solutions/primetime.html](https://www.adobe.com/solutions/primetime.html)
