---
seo-title: Implementar acceso a Adobe
title: Implementar acceso a Adobe
uuid: 9f9a9931-f607-4b1a-9209-0236a4c197ca
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---


# Implementar acceso a Adobe {#deploy-adobe-access}

Una ventaja clave del SDK de Adobe Access es que puede instalarlo en cualquier servidor de aplicaciones Java™ o contenedor servlet, como Tomcat. También necesita JDK™ 1.5 o superior. Para obtener más información sobre los requisitos de software, consulte Requisitos de la plataforma del SDK de Adobe Access: [: https://www.adobe.com/products/flashaccess/systemreqs/](https://www.adobe.com/products/flashaccess/systemreqs/).

Los pasos de alto nivel para implementar Adobe Access son:

1. Instale y configure el SDK de Adobe Access.
1. Obtenga certificados digitales de Adobe.
1. Cree un servidor de licencias con el SDK o implemente Adobe Access Server para flujo protegido.
1. Cree herramientas de empaquetado de contenido y administración de políticas para empaquetar contenido, utilizar las herramientas de preparación de contenido proporcionadas o autorizar uno de los empaquetadores de Adobe HTTP Dynamic Streaming.
1. Defina las reglas de uso del contenido y cree políticas que las apoyen.
1. Empaquete el contenido con las herramientas de administración de políticas y empaquetado.
1. Desarrolle aplicaciones de vídeo con las que los consumidores puedan vista de contenido protegido mediante Flash Player o Adobe AIR, o bien, utilice una OVP (Plataforma de vídeo en línea) establecida que admita Acceso a Adobe.
1. Implemente un archivo SWF para utilizarlo con Flash Player en el sitio web o publique el instalador de Adobe AIR para su descarga.

Estos pasos se amplían en las secciones siguientes, con referencias a otros documentos que contienen información adicional.

## Implementación en un sistema operativo de 64 bits {#deploying-on-a-bit-operating-system}

Un sistema operativo de 64 bits, como la versión de 64 bits de RedHat o Windows, proporciona un rendimiento mucho mejor que un sistema operativo de 32 bits.

## Instalación del SDK de Adobe Access {#install-adobe-access-sdk}

El SDK de Adobe Access se proporciona como archivo Java (JAR). Para obtener más información sobre la instalación de Adobe Access, consulte *Uso del SDK de Adobe Access para la protección de contenido* y *Directrices de implementación segura*.

## Implementar un servidor de licencias {#implement-a-license-server}

Con el SDK de Adobe Access, debe crear un servidor de licencias. Cuando el contenido está protegido mediante Adobe Access, no se puede ver hasta que el servidor de licencias emita una licencia para el consumidor. Si se utiliza la licencia basada en la identidad, la autenticación basada en contraseña garantiza que solo los consumidores autorizados puedan abrir y vista el contenido.

Al implementar un servidor de licencias, debe obtener los certificados digitales necesarios de Adobe. Consulte el documento de inscripción de certificados de acceso a Adobe para obtener instrucciones detalladas sobre cómo solicitar certificados.

Para obtener más información sobre la implementación de un servidor de licencias y la obtención de certificados digitales, consulte* Uso del SDK de Adobe Access para la protección de contenido.*

## Crear herramientas de administración de políticas y empaquetado de contenido {#create-content-packaging-and-policy-management-tools}

Con el SDK de Adobe Access, puede crear herramientas de administración de políticas y empaquetado de contenido. Las API de administración de políticas permiten a los administradores crear, vista de detalles y actualización de políticas. Las API de empaquetado incrustan la política en el archivo FLV o F4V y cifran el archivo con la clave de codificación de contenido.

El SDK de Adobe Access incluye una implementación de referencia ( [!DNL AdobePackager.jar]) que proporciona ejemplos de empaquetado de contenido y herramientas de administración de políticas ( [!DNL AdobePolicyManager.jar]).

Para obtener más información sobre la creación de herramientas de administración de políticas y empaquetado de contenido, consulte *Uso del SDK de Adobe Access para la protección de contenido*.

## Crear políticas y contenido de paquete {#create-policies-and-package-content}

Con las reglas de uso admitidas por el SDK, debe definir y crear políticas que admitan el modelo de negocio de su organización y, a continuación, empaquetar el contenido mediante dichas políticas. Una vez que las políticas se aplican al contenido durante el empaquetado, puede mantener el control del contenido independientemente de la amplia distribución que se distribuya.

Las políticas de Adobe Access admiten una amplia gama de reglas de uso diferentes, entre las que se incluyen:

* Especificar el número de días que una licencia es válida una vez que un consumidor comienza a ver el contenido.
* Permitiendo el almacenamiento en caché de licencias.
* Especificar los tiempos de ejecución del cliente y las versiones que pueden acceder al contenido (por ejemplo, los usuarios deben tener una determinada aplicación de Adobe AIR o una versión específica de Flash Player).
* Requerir que los consumidores se autentiquen utilizando un nombre de usuario y una contraseña antes de ver el contenido protegido o permitir el acceso anónimo.

Para obtener más información sobre cómo empaquetar contenido, consulte *Protección de contenido*. Para obtener más información sobre las reglas de uso y los modelos de negocio que admiten, consulte *Reglas de uso*.

## Desarrollar aplicaciones para la reproducción de vídeo {#develop-applications-for-video-playback}

Para permitir a los consumidores acceder y vista de contenido, desarrolle una aplicación de reproducción de vídeo con Flash Player o Adobe AIR. Una vez que haya desarrollado una aplicación de reproducción de vídeo, debe implementarla para los consumidores. Si está desarrollando una aplicación con Flash Player, alojarla en el sitio web de su organización. Si está desarrollando una aplicación con Adobe® AIR®, publique el instalador de la aplicación de AIR para que los consumidores puedan descargar e instalar la aplicación en su equipo.

Para obtener más información sobre el desarrollo de aplicaciones de reproducción de vídeo personalizadas para su uso con Adobe Access, consulte el capítulo &quot;Uso de vídeo&quot; en la [Guía para desarrolladores de ActionScript 3.0](https://help.adobe.com/en_US/as3/dev/WS9936fa0d5984e93b3f4f38ec1272a447844-8000.html)*, *el [Centro de tecnología de vídeo de Adobe](https://www.adobe.com/devnet/video/) y el Open Source Media Framework.