---
title: Introducción
description: Introducción
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Introducción {#getting-started}

Este documento proporciona los pasos para una configuración y una implementación rápidas de un ecosistema de Adobe Primetime DRM que utiliza la descarga progresiva para distribuir contenido, y el Servidor de Primetime DRM para transmisión protegida para la distribución de licencias. En las siguientes guías se proporcionan detalles adicionales sobre cada paso:

* *Usar el servidor de Primetime DRM para proteger contenido*
* *Uso del servidor DRM de Primetime para la transmisión protegida*

El servidor de Primetime DRM para transmisión protegida es un servidor de funcionalidad mínima que no incluye código fuente. Para un servidor modificable con fuente Java completa, consulte la guía *Using the Primetime DRM Reference Implementations* . Si configura un servidor de licencias de referencia, este reemplaza el paso *Configuración e implementa Primetime DRM Server para flujo protegido (servidor de licencias)*.

## Requisitos previos {#prerequisites}

Antes de comenzar, complete las siguientes tareas:

* Obtenga dos equipos Windows o Linux:

   * Un equipo será el servidor de licencias.
   * Un equipo será Content Server.

* Instale las siguientes aplicaciones en ambos equipos:

   * Tomcat 6.0.18
   * Java 1.6

## Obtener certificados {#obtain-certificates}

Una vez entregado el software SDK, el administrador de certificados de empresa designado recibirá una invitación para completar el proceso de registro de inscripción de certificados DRM de Adobe Primetime. Para obtener más información, consulte *Primetime DRM Certificate Insubscription Guide*.

1. El administrador nombra al menos a una persona para que actúe como solicitante de certificado.
1. El solicitante de certificado genera una clave privada y una CSR.
1. El solicitante envía una solicitud de certificado.
1. El administrador de la empresa aprueba la solicitud.
1. El administrador de certificados de Adobe confirma el envío.
1. El solicitante recibe el certificado, lo vincula con la clave privada y lo implementa. tal como se describe en .

   Para obtener más información sobre la implementación del certificado, consulte la guía *Implementación del servidor Adobe Primetime DRM para transmisión protegida* .
1. Los pasos del 3 al 6 deben completarse para cada tipo de certificado.

   Para la versión de producción de DRM de Primetime, el solicitante debe realizar solicitudes independientes para los certificados de servidor de licencias, empaquetado y transporte, que son válidos durante dos años.

   Los clientes que utilizan las versiones de evaluación o prueba de DRM de Primetime solo necesitan un certificado válido durante 1 año/90 días, respectivamente.