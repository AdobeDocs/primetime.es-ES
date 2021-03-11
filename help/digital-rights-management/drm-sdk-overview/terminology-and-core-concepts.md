---
title: Terminología y conceptos básicos
description: Terminología y conceptos básicos
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---


# Terminología y conceptos principales{#terminology-and-core-concepts}

En este documento se utilizan los siguientes términos y conceptos:

**Consumidor**

El *consumidor* es el usuario final que descarga o transmite contenido.

**Contenido**

** El contenido consiste en archivos digitales de audio o vídeo.

**Clave de cifrado de contenido**

La *Clave de cifrado de contenido* (CEK) es una clave criptográfica utilizada para cifrar el contenido.

**Propietarios de contenido**

*Los* propietarios de contenido son las entidades comerciales propietarias del copyright del contenido. Pueden ser estudios de imágenes en gran escala o productores independientes más pequeños de películas u otros contenidos audiovisuales.

**Paquetes de contenido**

*Los* paquetes de contenido son organizaciones que empaquetan contenido para utilizarlo con Adobe Primetime DRM. Los propietarios de contenido o los distribuidores pueden elegir empaquetar su propio contenido, o pueden obtener los servicios de un tercero para empaquetar su contenido y distribuirlo electrónicamente a través de Internet.

**Certificado digital**

*Los certificados*  digitales (también denominados  *certificados*) vinculan una entidad, como un individuo, una organización o un sistema, a un par de claves pública y privada específico. Los certificados digitales pueden considerarse como credenciales electrónicas que verifican la identidad de un individuo, sistema u organización.

**Firma digital**

Una *firma digital* vincula la identidad del editor al contenido que ha publicado y proporciona un mecanismo para detectar la manipulación. Los algoritmos de firma digital utilizan funciones hash criptográficas y algoritmos de cifrado asimétricos (o pares de claves pública y privada). Algunas firmas digitales también aprovechan los certificados digitales y la infraestructura de claves públicas (PKI) para enlazar claves públicas a las identidades de los propietarios o distribuidores de contenido.

**Distribuidor**

*Los distribuidores*  (también denominados  *distribuidores de* contenido o minoristas*) son entidades comerciales que garantizan los derechos de distribución de los propietarios de contenido para publicar y distribuir contenido a los consumidores. En algunos casos, la misma entidad es el propietario del contenido y el distribuidor de contenido.

**Metadatos de DRM**

Información que el cliente (es decir, Adobe® Flash® Player, Adobe® AIR® runtime y Primetime client) envía para identificar el contenido solicitado.

**Licencia**

Una *licencia *es una estructura de datos que contiene una clave cifrada utilizada para descifrar el contenido asociado a una directiva. La licencia la genera Primetime DRM cuando el consumidor solicita contenido y está enlazado al equipo del consumidor. Con una política como referencia, la licencia define los derechos disponibles para el consumidor que descarga contenido. Para ver el contenido, el consumidor debe obtener una licencia.

**Adquisición de licencia**

*La* adquisición de licencias es el proceso de adquisición de una licencia que permite al consumidor descifrar y ver contenido protegido de acuerdo con un conjunto de reglas de uso. La adquisición de licencias se produce cuando un cliente envía al servidor de licencias información que identifica el contenido solicitado (los *metadatos DRM*) y el certificado del equipo (que identifica el equipo del consumidor) (véase más adelante).

**Servidor de licencias**

El* servidor de licencias *puede integrarse en los sistemas de facturación y autenticación del distribuidor o proveedor de servicios y puede contener lógica empresarial para verificar que el consumidor que solicita contenido protegido está autorizado a ver el contenido. Si el usuario está autorizado a acceder al contenido, el servidor de licencias emite una licencia que permite al cliente de tiempo de ejecución descifrar y reproducir contenido en función de la política y los derechos asociados con la cuenta del consumidor.

Debe crear e implementar un servidor de licencias mediante el SDK de Primetime DRM.

**Política**

Una *directiva* es un contenedor para las reglas de uso que determinan cómo los consumidores pueden utilizar el contenido protegido. Las políticas se definen independientemente del contenido que se va a proteger. Una directiva no aplica derechos hasta que está enlazada al contenido a través de la licencia. Una directiva enumera el conjunto de reglas de uso, es decir, los permisos o &quot;derechos&quot; que los consumidores tienen sobre el contenido que adquieren. Por ejemplo, los propietarios de contenido pueden crear una política que garantice que el contenido protegido solo sea accesible para los consumidores durante un período de tiempo específico. A continuación, esta directiva se aplica a todo el contenido para el que el propietario del contenido desea aplicar esta restricción.

Las directivas se crean mediante el SDK de DRM de Primetime.

**Contenido protegido**

*El contenido protegido*  (también conocido como contenido  *empaquetado*) hace referencia al contenido de vídeo que se ha cifrado mediante el SDK de DRM de Primetime u otras herramientas compatibles.

**Minoristas**

Consulte la entrada para *distribuidores* anteriormente en esta sección.
