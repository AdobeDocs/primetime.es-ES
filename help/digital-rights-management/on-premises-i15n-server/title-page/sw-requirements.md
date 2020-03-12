---
description: 'null'
seo-description: 'null'
seo-title: Requisitos de software
title: Requisitos de software
uuid: 9faa229b-1abf-4b55-b293-247777bcb1db
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Requisitos de software {#software-requirements}

* Tomcat 6
* JDK 1.8

## Envío de código/Contenido del paquete{#code-delivery-package-contents}

El paquete del servidor de individualización local de Adobe Primetime DRM contiene lo siguiente:

* [!DNL flashaccess.war] - El servidor de individualización
* [!DNL flashaccess-kgs.war] - El servidor opcional de generación de claves
* [!DNL /shared] - Contiene:

   * [!DNL adobe-flashaccess-certs.jar]
   * [!DNL AdobeInitial.properties] - Archivo de propiedades de muestra

* [!DNL thirdparty/] - Incluye compatibilidad con Crypto-J como bibliotecas nativas:

   * [!DNL libjsafe.so] (Linux)
   * [!DNL jsafe.dll] (Windows)

* [!DNL adobe-flashaccess-i15n-setup.jar] - Utilidad para cifrar contraseñas de credenciales de servidor
* [!DNL ROOT] - contiene un [!DNL crossdomain.xml] archivo

* Archivos de caché de ECI: descargados previamente
* [!DNL addIndivCert.py] - Una secuencia de comandos para actualizar la raíz de confianza de un servidor de licencias para admitir las personalizaciones de OnPremises
* [!DNL CreateMetadata.jar] - Utilidad para crear metadatos DRM locales
* [!DNL client_sample/] - Una carpeta con un fragmento de código de cliente
* Notas de la versión: para cualquier adición de último momento a la documentación

## Obtención de certificados de servidor de individualización{#obtain-individualization-server-certificates}

Para utilizar el servidor de individualización local, primero debe obtener dos credenciales digitales (certificados):

* *Identificación de credenciales* de transporte - emitida por Adobe
* *Credenciales* de CA de individualización: emitidos por Symantec (VeriSign)

Para obtener estos certificados, envíe una solicitud a través del billete de Zendesk a: [https://adobeprimetime.zendesk.com](https://adobeprimetime.zendesk.com)

Tenga en cuenta que estas credenciales se suman a las necesarias para el funcionamiento de un servidor de licencias DRM Primetime.