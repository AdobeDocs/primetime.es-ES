---
title: Terminología y conceptos básicos
description: Terminología y conceptos básicos
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# Terminología y conceptos básicos {#terminology-and-core-concepts}

A lo largo de este documento se utilizan los siguientes términos y conceptos:

**Consumidor**

El *consumidor* es el usuario final que descarga o transmite contenido.

**Contenido**

*Contenido* consta de archivos de audio o vídeo digitales.

**Clave de cifrado de contenido**

El *Clave de cifrado de contenido* (CEK) es una clave criptográfica que se utiliza para cifrar el contenido.

**Propietarios de contenido**

*Propietarios de contenido* son las entidades comerciales propietarias de los derechos de autor del contenido. Pueden ser grandes estudios de cine o pequeños productores independientes de películas u otros contenidos audiovisuales.

**Empaquetadores de contenido**

*Empaquetadores de contenido* son organizaciones que empaquetan contenido para utilizarlo con Acceso de Adobe. Los propietarios o distribuidores de contenido pueden optar por empaquetar su propio contenido o pueden contratar los servicios de un tercero para empaquetar su contenido y distribuirlo electrónicamente a través de Internet.

**Certificado digital**

*Certificados digitales* (también denominado *certificados*) enlazar una entidad, como un individuo, organización o sistema, a un par de claves pública y privada específico. Los certificados digitales se pueden considerar como credenciales electrónicas que verifican la identidad de un individuo, sistema u organización.

**Firma digital**

A *firma digital* vincula la identidad del editor al contenido que ha publicado y proporciona un mecanismo para detectar la manipulación. Los algoritmos de firma digital utilizan funciones hash criptográficas y algoritmos de cifrado asimétricos (o par de claves pública y privada). Algunas firmas digitales también aprovechan los certificados digitales y la infraestructura de claves públicas (PKI) para vincular las claves públicas a la identidad de los propietarios o distribuidores de contenido.

**Distribuidor**

*Distribuidores* (también denominado *distribuidores de contenido* o* minoristas*) son entidades comerciales que garantizan los derechos de distribución de los propietarios de contenido para publicar y distribuir contenido a los consumidores. En algunos casos, la misma entidad es tanto el propietario del contenido como el distribuidor de este.

**Metadatos de DRM**

Información que el cliente (es decir, Adobe ® Flash ® Reproductor, tiempo de ejecución de Adobe® AIR® y cliente de Primetime) envía para identificar el contenido solicitado.

**Licencia**

Una licencia es una estructura de datos que contiene una clave cifrada que se utiliza para descifrar contenido asociado a una directiva. La licencia se genera mediante Adobe Access cuando el consumidor solicita contenido y está enlazada al equipo del consumidor. Utilizando una directiva como referencia, la licencia define los derechos disponibles para el consumidor que descarga contenido. Para ver contenido, el consumidor debe obtener una licencia.

**Adquisición de licencia**

*Adquisición de licencia* es el proceso de adquisición de una licencia que permite al consumidor descifrar y ver contenido protegido según un conjunto de reglas de uso. La adquisición de licencia se produce cuando un cliente envía información que identifica el contenido solicitado (la variable *Metadatos de DRM*) y el certificado del equipo (que identifica el equipo del consumidor) al servidor de licencias (consulte a continuación).

**Servidor de licencias**

El servidor de licencias* puede estar integrado en los sistemas de facturación y autenticación del distribuidor o del proveedor de servicios, y puede contener lógica empresarial para verificar que el consumidor que solicita el contenido protegido está autorizado a verlo. Si el usuario tiene autorización para acceder al contenido, el servidor de licencias emite una licencia que permite al cliente de tiempo de ejecución descifrar y reproducir contenido en función de la directiva y los derechos asociados a la cuenta del consumidor.

Debe crear e implementar un servidor de licencias mediante el SDK de acceso a Adobe.

**Política**

A *directiva* es un contenedor de las reglas de uso que determinan cómo los consumidores pueden utilizar el contenido protegido. Las políticas se definen independientemente del contenido que se protege. Una directiva no aplica derechos hasta que se enlaza al contenido mediante la licencia. Una directiva enumera el conjunto de reglas de uso, es decir, los permisos o &quot;derechos&quot; que los consumidores tienen sobre el contenido que adquieren. Por ejemplo, los propietarios de contenido pueden crear una política que garantice que el contenido protegido solo sea accesible para los consumidores durante un período de tiempo específico. Esta directiva se aplica a todo el contenido para el que el propietario del contenido desea aplicar esta restricción.

Las directivas se crean mediante el SDK de acceso al Adobe.

**Contenido protegido**

*Contenido protegido* (también denominado *contenido empaquetado*) hace referencia al contenido de vídeo FLV y F4V que se ha cifrado mediante el SDK de acceso a Adobe u otras herramientas compatibles.

**Minoristas**

Consulte la entrada para *distribuidores* anteriormente en esta sección.
