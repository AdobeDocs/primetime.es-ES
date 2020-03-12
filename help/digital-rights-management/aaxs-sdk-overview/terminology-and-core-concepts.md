---
seo-title: Terminología y conceptos básicos
title: Terminología y conceptos básicos
uuid: 89a9e4b0-f5e1-4dc2-9cf8-0c8d7e9b7d62
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Terminología y conceptos básicos {#terminology-and-core-concepts}

En este documento se utilizan los siguientes términos y conceptos:

**Consumidor**

El *consumidor* es el usuario final que descarga o transmite contenido.

**Contenido**

*El contenido* consiste en archivos de audio o vídeo digitales.

**Clave de cifrado de contenido**

La clave *de cifrado de* contenido (CEK) es una clave criptográfica utilizada para cifrar el contenido.

**Propietarios de contenido**

*Los propietarios* de contenido son las entidades comerciales que poseen el copyright del contenido. Pueden ser estudios de gran movimiento o productores independientes más pequeños de películas u otros contenidos audiovisuales.

**Empaquetadores de contenido**

*Los empaquetadores* de contenido son organizaciones que empaquetan contenido para utilizarlo con Adobe Access. Los propietarios de contenido o los distribuidores pueden optar por empaquetar su propio contenido, o pueden contratar los servicios de un tercero para empaquetar su contenido y distribuirlo electrónicamente a través de Internet.

**Certificado digital**

*Los certificados* digitales (también denominados *certificados*) enlazan una entidad, como un individuo, una organización o un sistema, a un par de claves públicas y privadas específico. Los certificados digitales pueden considerarse credenciales electrónicas que verifican la identidad de un individuo, sistema u organización.

**Firma digital**

Una firma ** digital enlaza la identidad del editor con el contenido que ha publicado y proporciona un mecanismo para detectar la manipulación. Los algoritmos de firma digital utilizan funciones de hash criptográficas y algoritmos de cifrado asimétricos (o pares de claves pública y privada). Algunas firmas digitales también aprovechan los certificados digitales y la infraestructura de claves públicas (PKI) para enlazar claves públicas a las identidades de los propietarios o distribuidores de contenido.

**Distribuidor**

*Los distribuidores* (también denominados distribuidores *de* contenido o* minoristas*) son entidades comerciales que garantizan los derechos de distribución de los propietarios de contenido para publicar y distribuir contenido a los consumidores. En algunos casos, la misma entidad es el propietario y el distribuidor de contenido.

**Metadatos de DRM**

Información que el cliente (es decir, Adobe® Flash® Player, Adobe® AIR® Runtime y el cliente Primetime) envía para identificar el contenido solicitado.

**Licencia**

Una *licencia *es una estructura de datos que contiene una clave cifrada utilizada para descifrar el contenido asociado a una política. Adobe Access genera la licencia cuando el consumidor solicita contenido y está vinculado al equipo del consumidor. Con una política como referencia, la licencia define los derechos disponibles para el consumidor que descarga contenido. Para ver el contenido, el consumidor debe obtener una licencia.

**Adquisición de licencias**

*La adquisición* de licencias es el proceso de adquisición de una licencia que permite al consumidor descifrar y ver el contenido protegido de acuerdo con un conjunto de reglas de uso. La adquisición de licencias se produce cuando un cliente envía al servidor de licencias información que identifica el contenido solicitado (los metadatos *de* DRM) y el certificado del equipo (que identifica el equipo del consumidor) (véase más adelante).

**Servidor de licencias**

El servidor de licencias* *puede estar integrado en los sistemas de facturación y autenticación del distribuidor o proveedor de servicios, y puede contener lógica empresarial para verificar que el consumidor que solicita contenido protegido está autorizado a ver el contenido. Si el usuario está autorizado para acceder al contenido, el servidor de licencias emite una licencia que permite al cliente en tiempo de ejecución descifrar y reproducir contenido según la política y los derechos asociados con la cuenta del consumidor.

Debe crear e implementar un servidor de licencias mediante el SDK de Adobe Access.

**Política**

Una *política* es un contenedor para las reglas de uso que determinan cómo los consumidores pueden utilizar el contenido protegido. Las políticas se definen independientemente del contenido que se esté protegiendo. Una política no aplica derechos hasta que se vincula al contenido a través de la licencia. Una política enumera el conjunto de reglas de uso, es decir, los permisos o &quot;derechos&quot; que los consumidores tienen sobre el contenido que adquieren. Por ejemplo, los propietarios de contenido pueden crear una política que garantice que el contenido protegido sólo sea accesible para los consumidores durante un período de tiempo específico. Esta directiva se aplica a todo el contenido para el que el propietario del contenido desea aplicar esta restricción.

Las directivas se crean mediante el SDK de Adobe Access.

**Contenido protegido**

*El contenido* protegido (también denominado contenido ** empaquetado) hace referencia al contenido de vídeo FLV y F4V que se ha cifrado con el SDK de Adobe Access u otras herramientas admitidas.

**Minoristas**

Consulte la entrada para *distribuidores* anteriormente en esta sección.
