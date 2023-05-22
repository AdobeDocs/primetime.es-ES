---
title: Implementación de DRM de Adobe Primetime
description: Implementación de DRM de Adobe Primetime
copied-description: true
exl-id: 64a96d70-502c-48b8-9f43-59f4001a7ab6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---

# Implementación de DRM de Adobe Primetime {#configure-adobe-primetime-drm}

Una ventaja clave del SDK de DRM de Adobe Primetime es que se puede instalar en cualquier servidor de aplicaciones Java™ o contenedor de servlets, como Tomcat. También necesita JDK™ 1.5 o superior. Para obtener más información sobre los requisitos de software, consulte Requisitos de plataforma del SDK de DRM de Primetime: [https://www.adobe.com/products/flashaccess/systemreqs/](https://www.adobe.com/products/flashaccess/systemreqs/).

Los pasos de alto nivel para implementar Primetime DRM son los siguientes:

1. Instale y configure el SDK de DRM de Primetime.
1. Obtenga certificados digitales de Adobe.
1. Cree un servidor de licencias con el SDK o implemente el servidor DRM de Primetime para flujo protegido.
1. Cree herramientas de empaquetado de contenido y de administración de políticas para empaquetar contenido, utilice las herramientas de preparación de contenido proporcionadas o conceda una licencia a uno de los empaquetadores de HTTP Dynamic Streaming de Adobe.
1. Defina reglas de uso para el contenido y cree políticas para admitir esas reglas.
1. Empaquete el contenido con las herramientas de empaquetado y administración de directivas.
1. Desarrolle aplicaciones de vídeo con las que los consumidores puedan ver el contenido protegido mediante Flash Player o Adobe AIR, o utilice una OVP (plataforma de vídeo en línea) ya establecida que admita DRM de Primetime.
1. Implemente un archivo de SWF para utilizarlo con el Flash Player en su sitio web o publique el instalador de Adobe AIR para su descarga.

Estos pasos se explican en las secciones siguientes, con referencias a otros documentos que contienen información adicional.

## Implementación en un sistema operativo de 64 bits{#deploying-on-a-bit-operating-system}

Un sistema operativo de 64 bits, como la versión de 64 bits de RedHat o Windows, proporciona un rendimiento mucho mejor que un sistema operativo de 32 bits.

## Instalación del SDK de DRM de Adobe Primetime {#install-adobe-primetime-drm-sdk}

El SDK de DRM de Primetime se proporciona como archivo Java (JAR). Para obtener más información sobre la instalación de Primetime DRM, consulte Uso del SDK de Adobe Primetime DRM para proteger el contenido y las directrices de implementación segura.

## Implementación de un servidor de licencias {#implement-a-license-server}

Con el SDK de DRM de Adobe Primetime, debe crear un servidor de licencias. Cuando el contenido está protegido mediante Primetime DRM, no se puede ver hasta que el servidor de licencias emita una licencia al consumidor. Si se utilizan licencias basadas en identidad, la autenticación basada en contraseña garantiza que solo los consumidores autorizados puedan abrir y ver contenido.

Al implementar un servidor de licencias, debe obtener los certificados digitales necesarios de Adobe. Consulte el documento Inscripción de certificado DRM de Primetime para obtener instrucciones detalladas sobre cómo solicitar certificados.

Para obtener más información sobre la implementación de un servidor de licencias y la obtención de certificados digitales, consulte **Uso del SDK de DRM de Adobe Primetime para proteger el contenido.**

## Crear herramientas de empaquetado de contenido y administración de políticas{#create-content-packaging-and-policy-management-tools}

Con el SDK de DRM de Adobe Primetime, puede crear herramientas de empaquetado de contenido y de administración de directivas. Las API de administración de directivas permiten a los administradores crear, ver detalles y actualizar directivas. Las API de empaquetado incrustan la directiva en el archivo de vídeo y cifran el archivo con la clave de cifrado de contenido.

El SDK de DRM de Primetime incluye una implementación de referencia ( [!DNL AdobePackager.jar]) que proporciona ejemplos de empaquetado de contenido y herramientas de administración de directivas ( [!DNL AdobePolicyManager.jar]).

Para obtener más información sobre la creación de herramientas de empaquetado de contenido y administración de directivas, consulte **Uso del SDK de DRM de Adobe Primetime para proteger el contenido.**

## Creación de políticas y contenido del paquete {#create-policies-and-package-content}

Con las reglas de uso admitidas por el SDK, debe definir y crear directivas que admitan el modelo empresarial de su organización y, a continuación, empaquetar el contenido mediante esas directivas. Una vez que se aplican políticas al contenido durante el empaquetado, puede mantener el control del contenido, independientemente de la amplitud de su distribución.

Las políticas de Adobe Primetime DRM admiten una amplia gama de reglas de uso diferentes, entre las que se incluyen:

* Especificación del número de días durante los cuales una licencia es válida una vez que un consumidor comienza a ver el contenido.
* Permitir el almacenamiento en caché de licencias.
* Especificar los tiempos de ejecución y las versiones de cliente que pueden acceder al contenido (por ejemplo, los usuarios deben tener una aplicación de Adobe AIR determinada o una versión específica del Flash Player).
* Exigir que los consumidores se autentifiquen con un nombre de usuario y una contraseña antes de ver contenido protegido o permitir el acceso anónimo.

Para obtener más información sobre el empaquetado de contenido, consulte *Protección del contenido*. Para obtener más información sobre las reglas de uso y los modelos de negocio que admiten, consulte *Reglas de uso*.

## Desarrollo de aplicaciones para la reproducción de vídeo {#develop-applications-for-video-playback}

Para permitir que los consumidores accedan y vean contenido, desarrolle una aplicación de reproducción de vídeo mediante Flash Player o Adobe AIR. Una vez desarrollada una aplicación de reproducción de vídeo, debe implementarla para los consumidores. Si está desarrollando una aplicación mediante Flash Player, aloje la aplicación en el sitio web de su organización. Si está desarrollando una aplicación con Adobe® AIR®, publique el programa de instalación de la aplicación AIR para que los consumidores puedan descargar e instalar la aplicación en su equipo.

Para obtener más información sobre el desarrollo de aplicaciones de reproducción de vídeo personalizadas para su uso con Adobe Primetime DRM, consulte el capítulo &quot;Trabajo con vídeo&quot; en [Guía para desarrolladores de ActionScript 3.0](https://help.adobe.com/en_US/as3/dev/WS9936fa0d5984e93b3f4f38ec1272a447844-8000.html), el [Centro de tecnología de vídeo Adobe](https://www.adobe.com/devnet/video/)y el Open Source Media Framework.
