---
seo-title: Introducción
title: Introducción
uuid: 2002cf94-c8a7-4820-a560-6d9f7f33ee97
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Introducción {#getting-started}

Este documento proporciona los pasos para una configuración e implementación rápidas de un ecosistema de DRM de Adobe Primetime que utiliza la descarga progresiva para distribuir contenido, y el servidor de DRM de Primetime para flujo protegido para la distribución de licencias. En las siguientes guías se proporcionan más detalles sobre cada paso:

* *Uso del servidor DRM de Primetime para proteger el contenido*
* *Uso del servidor DRM de Primetime para flujo protegido*

Primetime DRM Server for Protected Streaming es un servidor de funcionalidad mínima que no incluye código fuente. Para ver un servidor modificable con el origen Java completo, consulte la guía *Uso de las implementaciones* de referencia de DRM de Primetime. Si configura un servidor de licencias de referencia, este paso sustituye al paso *Configuración e implementa Primetime DRM Server para flujo protegido (servidor de licencias)* .

## Requisitos previos {#prerequisites}

Antes de comenzar, realice las siguientes tareas:

* Obtenga dos equipos con Windows o Linux:

   * Un equipo será el servidor de licencias.
   * Un equipo será Content Server.

* Instale las siguientes aplicaciones en ambos equipos:

   * Tomcat 6.0.18
   * Java 1.6

## Obtención de certificados {#obtain-certificates}

Una vez entregado el software SDK, el administrador de certificados de la empresa designado recibirá una invitación para completar el proceso de registro del certificado DRM de Adobe Primetime. Para obtener más información, consulte la Guía de inscripción de certificados *Primetime DRM*.

1. El administrador nombra al menos a una persona para que actúe como solicitante de certificado.
1. El solicitante de certificado genera una clave privada y un CSR.
1. El solicitante envía una solicitud de certificado.
1. El administrador de la empresa aprueba la solicitud.
1. El administrador de certificados de Adobe confirma el envío.
1. El solicitante recibe el certificado, lo enlaza con la clave privada y lo implementa. tal como se describe en .

   Para obtener más información sobre la implementación del certificado, consulte la guía *Implementación del servidor de DRM de Adobe Primetime para flujo* protegido.
1. Los pasos 3 a 6 deben completarse para cada tipo de certificado.

   Para la versión de producción de DRM Primetime, el solicitante debe realizar solicitudes independientes para los certificados Servidor de licencias, Empaquetado y Transporte, que son válidos durante dos años.

   Los clientes que utilizan las versiones de evaluación o prueba de DRM Primetime solo necesitan un certificado válido durante 1 año/90 días, respectivamente.