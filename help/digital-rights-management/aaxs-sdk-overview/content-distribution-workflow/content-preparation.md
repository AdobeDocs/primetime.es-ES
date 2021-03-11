---
description: Cualquier uso de Acceso a Adobe consiste en dos pasos clave en diferentes puntos del flujo de trabajo. La preparación del contenido debe realizarse una vez por recurso y dar como resultado la creación de contenido protegido. La adquisición de contenido se realiza varias veces, una vez por cada consumidor que desee ver ese recurso protegido.
title: Preparación de contenido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---


# Preparación de contenido {#content-preparation}

Cualquier uso de Acceso a Adobe consiste en dos pasos clave en diferentes puntos del flujo de trabajo. La preparación del contenido debe realizarse una vez por recurso y dar como resultado la creación de contenido protegido. La adquisición de contenido se realiza varias veces, una vez por cada consumidor que desee ver ese recurso protegido.

Antes de que el contenido esté disponible para su distribución, primero debe codificarlo en el formato de vídeo FLV o F4V, crear una o más políticas que especifiquen reglas de uso para el contenido y empaquetar el contenido mediante el SDK de acceso a Adobe.

Los pasos para codificar, empaquetar y distribuir contenido son los siguientes:

1. Codifique el contenido en formato FLV o F4V utilizando las herramientas de codificación disponibles en Adobe o de terceros.
1. Cree directivas que especifiquen las reglas de uso en las que los consumidores pueden ver el contenido.

   Una política es el contenedor de reglas y restricciones que determinan cómo, cuándo y dónde los consumidores pueden ver el contenido protegido.

   El empaquetador requiere al menos una directiva con al menos una regla de uso. Puede anular la regla de uso y agregar reglas de uso adicionales, cuando el servidor de licencias genere la licencia.

1. Empaquete el contenido y especifique qué políticas aplicar.

   El SDK de acceso a Adobe cifra el contenido mediante una clave de cifrado de contenido (CEK) y enlaza una o más políticas al contenido. El resultado es un *archivo de contenido protegido *que solo puede reproducir un consumidor que haya obtenido una licencia del servidor de licencias correspondiente.

   Durante el empaquetado, el contenido se cifra utilizando el CEK. El CEK se cifra utilizando la clave pública del servidor de licencias y se incluye en los metadatos de DRM junto con las políticas. Los metadatos de DRM se firman con la clave privada de Packager y los metadatos se incluyen en el contenido protegido.

1. Ponga el contenido protegido a disposición de los consumidores.

   El contenido protegido se distribuye generalmente mediante una red de distribución de contenido (CDN). La CDN puede utilizar cualquier mecanismo compatible con el tiempo de ejecución del cliente, como Flash Media Server, HTTP Dynamic Streaming de Adobe para la transmisión de varias velocidades de bits o un servidor web HTTP para la descarga progresiva.

