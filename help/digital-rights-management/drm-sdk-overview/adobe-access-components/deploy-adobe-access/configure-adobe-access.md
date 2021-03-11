---
title: Implementación de Adobe Primetime DRM
description: Implementación de Adobe Primetime DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---


# Implementación de Adobe Primetime DRM {#configure-adobe-primetime-drm}

Una ventaja clave del SDK de Adobe Primetime DRM es que puede instalarlo en cualquier servidor de aplicaciones Java™ o contenedor de servlet, como Tomcat. También necesita JDK™ 1.5 o superior. Para obtener más información sobre los requisitos de software, consulte Requisitos de plataforma del SDK de DRM de Primetime: [https://www.adobe.com/products/flashaccess/systemreqs/](https://www.adobe.com/products/flashaccess/systemreqs/).

Los pasos de alto nivel para implementar Primetime DRM son:

1. Instale y configure el SDK de DRM de Primetime.
1. Obtenga certificados digitales de Adobe.
1. Cree un servidor de licencias con el SDK o implemente Servidor de Primetime DRM para transmisión protegida.
1. Cree paquetes de contenido y herramientas de administración de políticas para empaquetar contenido, utilice las herramientas de preparación de contenido proporcionadas o obtenga una licencia de uno de los paquetes de HTTP Dynamic Streaming de Adobe.
1. Defina las reglas de uso del contenido y cree políticas que las apoyen.
1. Empaquete el contenido con las herramientas de administración de políticas y paquetes.
1. Desarrolle aplicaciones de vídeo con las que los consumidores puedan ver el contenido protegido mediante Flash Player o Adobe AIR, o utilice un OVP (plataforma de vídeo en línea) compatible con Primetime DRM.
1. Implemente un archivo SWF para utilizarlo con Flash Player en su sitio web o publique el instalador de Adobe AIR para su descarga.

Estos pasos se amplían en las secciones siguientes, con referencias a otros documentos que contienen información adicional.

## Implementación en un sistema operativo de 64 bits{#deploying-on-a-bit-operating-system}

Un sistema operativo de 64 bits, como la versión de 64 bits de RedHat o Windows, proporciona un rendimiento mucho mejor que un sistema operativo de 32 bits.

## Instalación del SDK de Adobe Primetime DRM {#install-adobe-primetime-drm-sdk}

El SDK de DRM de Primetime se proporciona como archivo Java (JAR). Para obtener más información sobre la instalación de Primetime DRM, consulte Uso del SDK de Adobe Primetime DRM para la protección de contenido y las directrices de implementación segura.

## Implementar un servidor de licencias {#implement-a-license-server}

Con el SDK de Adobe Primetime DRM, debe crear un servidor de licencias. Cuando el contenido está protegido mediante Primetime DRM, no se puede ver hasta que el servidor de licencias emita una licencia al consumidor. Si se utiliza la licencia basada en identidad, la autenticación basada en contraseña garantiza que solo los consumidores autorizados puedan abrir y ver el contenido.

Al implementar un servidor de licencias, debe obtener los certificados digitales necesarios desde el Adobe. Consulte el documento de inscripción de certificados de DRM de Primetime para obtener instrucciones detalladas sobre la solicitud de certificados.

Para obtener más información sobre la implementación de un servidor de licencias y la obtención de certificados digitales, consulte **Uso del SDK de Adobe Primetime DRM para la protección de contenido.**

## Crear paquetes de contenido y herramientas de administración de directivas{#create-content-packaging-and-policy-management-tools}

Con el SDK de Adobe Primetime DRM, puede crear paquetes de contenido y herramientas de administración de directivas. Las API de administración de directivas permiten a los administradores crear, ver detalles y actualizar directivas. Las API de empaquetado incrustan la directiva en un archivo de vídeo y cifran el archivo mediante la clave de cifrado de contenido.

El SDK de DRM de Primetime incluye una implementación de referencia ( [!DNL AdobePackager.jar]) que proporciona ejemplos de empaquetado de contenido y herramientas de administración de políticas ( [!DNL AdobePolicyManager.jar]).

Para obtener más información sobre la creación de paquetes de contenido y herramientas de administración de directivas, consulte **Uso del SDK de DRM de Adobe Primetime para la protección de contenido.**

## Crear políticas y contenido de paquetes {#create-policies-and-package-content}

Mediante las reglas de uso admitidas por el SDK, debe definir y crear políticas que apoyen el modelo empresarial de su organización y, a continuación, empaquetar el contenido mediante dichas políticas. Una vez que las políticas se aplican al contenido durante el empaquetado, puede mantener el control del contenido independientemente de su distribución.

Las políticas de Adobe Primetime DRM admiten una amplia gama de reglas de uso diferentes, que incluyen:

* Especificar el número de días de validez de una licencia una vez que el consumidor empieza a ver el contenido.
* Permitiendo el almacenamiento en caché de licencias.
* Especificar los tiempos de ejecución del cliente y las versiones que pueden acceder al contenido (por ejemplo, los usuarios deben tener una aplicación de Adobe AIR determinada o una versión específica del Flash Player).
* Requerir que los consumidores se autentiquen utilizando un nombre de usuario y una contraseña antes de ver el contenido protegido, o permitir el acceso anónimo.

Para obtener más información sobre el contenido del paquete, consulte *Protección del contenido*. Para obtener más información sobre las reglas de uso y los modelos de negocio que admiten, consulte *Reglas de uso*.

## Desarrollar aplicaciones para la reproducción de vídeo {#develop-applications-for-video-playback}

Para permitir a los consumidores acceder y ver contenido, desarrolle una aplicación de reproducción de vídeo con Flash Player o Adobe AIR. Una vez que haya desarrollado una aplicación de reproducción de vídeo, debe implementarla para los consumidores. Si está desarrollando una aplicación con Flash Player, alojarla en el sitio web de su organización. Si está desarrollando una aplicación con Adobe® AIR®, publique el instalador de la aplicación de AIR para que los consumidores puedan descargar e instalar la aplicación en su equipo.

Para obtener más información sobre el desarrollo de aplicaciones de reproducción de vídeo personalizadas para su uso con Adobe Primetime DRM, consulte el capítulo &quot;Trabajo con vídeo&quot; en la [Guía para desarrolladores de ActionScript 3.0](https://help.adobe.com/en_US/as3/dev/WS9936fa0d5984e93b3f4f38ec1272a447844-8000.html), el [Centro de tecnología de vídeo de Adobe](https://www.adobe.com/devnet/video/) y el Open Source Media Framework.