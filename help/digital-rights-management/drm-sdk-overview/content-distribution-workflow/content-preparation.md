---
description: Cualquier uso de DRM de Adobe Primetime consiste en dos pasos clave en diferentes puntos del flujo de trabajo. La preparación del contenido debe realizarse una vez por recurso y resulta en la creación de contenido protegido. La adquisición de contenido se realiza varias veces, una por cada consumidor que desea ver ese recurso protegido.
title: Preparación de contenido
exl-id: 6ec8e5a1-3cf4-498b-9cbb-760c525fb9c7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Preparación de contenido{#content-preparation}

Cualquier uso de DRM de Adobe Primetime consiste en dos pasos clave en diferentes puntos del flujo de trabajo. La preparación del contenido debe realizarse una vez por recurso y resulta en la creación de contenido protegido. La adquisición de contenido se realiza varias veces, una por cada consumidor que desea ver ese recurso protegido.

Antes de hacer que el contenido esté disponible para la distribución, primero debe codificarlo en formato de vídeo, crear una o más directivas que especifiquen las reglas de uso del contenido y empaquetar el contenido mediante el SDK de DRM de Adobe Primetime.

Los pasos para codificar, empaquetar y distribuir contenido son los siguientes:

1. Codifique el contenido en el formato de vídeo deseado con las herramientas de codificación disponibles desde el Adobe o desde terceros.
1. Cree políticas que especifiquen las reglas de uso bajo las cuales los consumidores pueden ver el contenido.

   Una directiva es el contenedor de las reglas y restricciones que determinan cómo, cuándo y dónde los consumidores pueden ver el contenido protegido.

   El empaquetador requiere al menos una directiva con al menos una regla de uso. Puede anular la regla de uso y agregar reglas de uso adicionales cuando el servidor de licencias genere la licencia.

1. Empaquete el contenido y especifique qué políticas aplicar.

   El SDK de DRM de Primetime cifra el contenido mediante una clave de cifrado de contenido (CEK) y enlaza una o más políticas al contenido. El resultado es un archivo de contenido protegido que solo puede reproducir un consumidor que haya obtenido una licencia del servidor de licencias correspondiente.

   Durante el empaquetado, el contenido se cifra usando el CEK. El CEK se cifra utilizando la clave pública del servidor de licencias y se incluye en los metadatos DRM de Primetime junto con las directivas. Los metadatos DRM de Primetime se firman con la clave privada del empaquetador y los metadatos se incluyen en el contenido protegido.

1. Poner el contenido protegido a disposición de los consumidores para su distribución.

   El contenido protegido se distribuye generalmente mediante una red de distribución de contenido (CDN). La CDN puede utilizar cualquier mecanismo admitido por el tiempo de ejecución del cliente, como Flash Media Server, HTTP Dynamic Streaming de Adobe para varias secuencias de velocidad de bits o un servidor web HTTP para descarga progresiva.
