---
title: Primeros pasos
description: Primeros pasos
copied-description: true
exl-id: d29d141e-913c-4b9d-979c-91c486414071
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# Primeros pasos {#getting-started}

Este documento proporciona los pasos para una configuración e implementación rápidas de un ecosistema de DRM de Adobe Primetime que utiliza Descarga progresiva para distribuir contenido y el servidor de DRM de Primetime para Streaming protegido para la distribución de licencias. En las siguientes guías se proporcionan detalles adicionales sobre cada paso:

* *Uso del servidor DRM de Primetime para proteger el contenido*
* *Uso del servidor DRM de Primetime para flujo protegido*

El servidor DRM de Primetime para flujo protegido es un servidor de funcionalidad mínima que no incluye código fuente. Para ver un servidor modificable con origen Java completo, consulte la *Uso de las implementaciones de referencia de DRM de Primetime* guía. Si configura un servidor de licencias de referencia, este sustituirá al *Configuración e implementación del servidor DRM de Primetime para flujo protegido (servidor de licencias)* paso.

## Requisitos previos {#prerequisites}

Antes de comenzar, complete las siguientes tareas:

* Obtenga dos equipos Windows o Linux:

   * Un equipo será el servidor de licencias.
   * Un equipo será Content Server.

* Instale las siguientes aplicaciones en ambos equipos:

   * Tomcat 6.0.18
   * Java 1.6

## Obtener certificados {#obtain-certificates}

Una vez entregado el software SDK, el administrador de certificados de compañía designado recibirá una invitación para completar el proceso de registro de certificados DRM de Adobe Primetime. Para obtener más información, consulte la *Guía de inscripción de certificados DRM de Primetime*.

1. El administrador nombra al menos a una persona para que actúe como solicitante de certificado.
1. El solicitante de certificados genera una clave privada y una CSR.
1. El solicitante envía una solicitud de certificado.
1. El administrador de la empresa aprueba la solicitud.
1. El administrador de certificados de Adobe confirma el envío.
1. El solicitante recibe el certificado, lo vincula con la clave privada y lo implementa. tal como se describe en .

   Para obtener más información sobre la implementación del certificado, consulte la *Implementación del servidor DRM de Adobe Primetime para el streaming protegido* guía.
1. Los pasos del 3 al 6 deben completarse para cada tipo de certificado.

   Para la versión de producción DRM de Primetime, el solicitante debe realizar solicitudes independientes para los certificados de servidor de licencias, empaquetado y transporte, que son válidos durante dos años.

   Los clientes que utilizan las versiones de evaluación o prueba de DRM de Primetime solo necesitan un certificado válido para 1 año/90 días, respectivamente.
