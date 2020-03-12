---
description: Cualquier uso de Adobe Primetime DRM consiste en dos pasos clave en diferentes puntos del flujo de trabajo. La preparación del contenido debe realizarse una vez por recurso y resulta en la creación de contenido protegido. La adquisición de contenido se realiza varias veces, una por cada consumidor que desee ver ese recurso protegido.
seo-description: Cualquier uso de Adobe Primetime DRM consiste en dos pasos clave en diferentes puntos del flujo de trabajo. La preparación del contenido debe realizarse una vez por recurso y resulta en la creación de contenido protegido. La adquisición de contenido se realiza varias veces, una por cada consumidor que desee ver ese recurso protegido.
seo-title: Preparación del contenido
title: Preparación del contenido
uuid: edb633f0-b623-41ea-a52a-19017d45fb18
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Preparación del contenido{#content-preparation}

Cualquier uso de Adobe Primetime DRM consiste en dos pasos clave en diferentes puntos del flujo de trabajo. La preparación del contenido debe realizarse una vez por recurso y resulta en la creación de contenido protegido. La adquisición de contenido se realiza varias veces, una por cada consumidor que desee ver ese recurso protegido.

Antes de que el contenido esté disponible para su distribución, primero debe codificar el contenido en el formato de vídeo, crear una o varias políticas que especifiquen las reglas de uso del contenido y empaquetar el contenido con el SDK de DRM de Adobe Primetime.

Los pasos para codificar, empaquetar y distribuir contenido son los siguientes:

1. Codifique el contenido en el formato de vídeo deseado mediante las herramientas de codificación disponibles de Adobe o de terceros.
1. Cree directivas que especifiquen las reglas de uso en las que los consumidores pueden ver el contenido.

   Una política es el contenedor de reglas y restricciones que determinan cómo, cuándo y dónde los consumidores pueden ver el contenido protegido.

   El empaquetador requiere al menos una directiva con al menos una regla de uso. Puede anular la regla de uso y agregar reglas de uso adicionales cuando el servidor de licencias genere la licencia.

1. Empaquete el contenido y especifique qué políticas aplicar.

   Primetime DRM SDK codifica el contenido mediante una clave de codificación de contenido (CEK) y enlaza una o varias directivas al contenido. El resultado es un *archivo de contenido protegido *que sólo puede reproducir un consumidor que haya obtenido una licencia del servidor de licencias correspondiente.

   Durante el empaquetado, el contenido se cifra mediante el CEK. El CEK se cifra mediante la clave pública del servidor de licencias y se incluye en los metadatos de DRM de Primetime junto con las políticas. Los metadatos de DRM de Primetime se firman con la clave privada de Packager y se incluyen en el contenido protegido.

1. Ponga el contenido protegido a disposición de los consumidores para su distribución.

   El contenido protegido se distribuye generalmente mediante una red de distribución de contenido (CDN). La CDN puede utilizar cualquier mecanismo admitido por el tiempo de ejecución del cliente, como Flash Media Server, el flujo dinámico HTTP de Adobe para el flujo de varias velocidades de bits o un servidor web HTTP para la descarga progresiva.

