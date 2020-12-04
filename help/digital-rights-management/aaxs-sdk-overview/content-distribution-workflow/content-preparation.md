---
description: Cualquier uso de Adobe Access consiste en dos pasos clave en diferentes puntos del flujo de trabajo. La preparación del contenido debe realizarse una vez por recurso y resulta en la creación de contenido protegido. La adquisición de contenido se realiza varias veces, una por cada consumidor que desee ver ese recurso protegido.
seo-description: Cualquier uso de Adobe Access consiste en dos pasos clave en diferentes puntos del flujo de trabajo. La preparación del contenido debe realizarse una vez por recurso y resulta en la creación de contenido protegido. La adquisición de contenido se realiza varias veces, una por cada consumidor que desee ver ese recurso protegido.
seo-title: Preparación del contenido
title: Preparación del contenido
uuid: 7a3562c6-6033-4e28-8f0a-18e3cb8987b9
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---


# Preparación del contenido {#content-preparation}

Cualquier uso de Adobe Access consiste en dos pasos clave en diferentes puntos del flujo de trabajo. La preparación del contenido debe realizarse una vez por recurso y resulta en la creación de contenido protegido. La adquisición de contenido se realiza varias veces, una por cada consumidor que desee ver ese recurso protegido.

Antes de que el contenido esté disponible para su distribución, primero debe codificar el contenido en formato de vídeo FLV o F4V, crear una o varias políticas que especifiquen las reglas de uso del contenido y empaquetar el contenido mediante el SDK de Adobe Access.

Los pasos para codificar, empaquetar y distribuir contenido son los siguientes:

1. Codifique el contenido en formato FLV o F4V mediante las herramientas de codificación disponibles en Adobe o de terceros.
1. Cree políticas que especifiquen las reglas de uso en las que los consumidores pueden vista del contenido.

   Una política es el contenedor de las reglas y restricciones que determinan cómo, cuándo y dónde los consumidores pueden ver el contenido protegido.

   El empaquetador requiere al menos una directiva con al menos una regla de uso. Puede anular la regla de uso y agregar reglas de uso adicionales cuando el servidor de licencias genere la licencia.

1. Empaquete el contenido y especifique qué políticas aplicar.

   El SDK de Adobe Access cifra el contenido mediante una clave de cifrado de contenido (CEK) y enlaza una o varias directivas al contenido. El resultado es un *archivo de contenido protegido *que sólo puede reproducir un consumidor que haya obtenido una licencia del servidor de licencias correspondiente.

   Durante el empaquetado, el contenido se cifra mediante el CEK. El CEK se cifra mediante la clave pública del servidor de licencias y se incluye en los metadatos de DRM junto con las políticas. Los metadatos DRM se firman con la clave privada de Packager y los metadatos se incluyen en el contenido protegido.

1. Ponga el contenido protegido a disposición de los consumidores para su distribución.

   El contenido protegido se distribuye generalmente mediante una red de distribución de contenido (CDN). La CDN puede utilizar cualquier mecanismo admitido por el tiempo de ejecución del cliente, como Flash Media Server, HTTP Dynamic Streaming de Adobe para el flujo de varias velocidades de bits o un servidor web HTTP para la descarga progresiva.

