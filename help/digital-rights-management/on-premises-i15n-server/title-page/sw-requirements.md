---
title: Requisitos de software
description: Requisitos de software
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Requisitos de software {#software-requirements}

* Tomcat 6
* JDK 1.8

## Entrega de código / Contenido del paquete{#code-delivery-package-contents}

El paquete de Adobe Primetime DRM On Premises Individualization Server contiene lo siguiente:

* [!DNL flashaccess.war] - El servidor de individualización
* [!DNL flashaccess-kgs.war] : servidor opcional de generación de claves
* [!DNL /shared] - Contiene:

   * [!DNL adobe-flashaccess-certs.jar]
   * [!DNL AdobeInitial.properties] - Archivo de propiedades de muestra

* [!DNL thirdparty/] - Incluye compatibilidad con Crypto-J como bibliotecas nativas:

   * [!DNL libjsafe.so] (Linux)
   * [!DNL jsafe.dll] (Windows)

* [!DNL adobe-flashaccess-i15n-setup.jar] - Utilidad para cifrar contraseñas de credenciales de servidor
* [!DNL ROOT] - contiene un [!DNL crossdomain.xml] archivo

* Archivos de caché de ECI: predescargados
* [!DNL addIndivCert.py] : secuencia de comandos para actualizar la raíz de confianza de un servidor de licencias para admitir individualizaciones locales
* [!DNL CreateMetadata.jar] : Utilidad para crear metadatos DRM locales
* [!DNL client_sample/] - Una carpeta con un fragmento de código de cliente
* Notas de la versión: para cualquier adición de último minuto a la documentación

## Obtener certificados de servidor de individualización{#obtain-individualization-server-certificates}

Para utilizar el servidor de individualización local, primero debe obtener dos credenciales digitales (certificados):

* *Credencial de transporte de individualización* - emitidos por Adobe
* *Credencial de CA de individualización* - emitido por Symantec (VeriSign)

Para obtener estos certificados, envíe una solicitud a través de Zendesk ticket a: [https://adobeprimetime.zendesk.com](https://adobeprimetime.zendesk.com)

Tenga en cuenta que estas credenciales se añaden a las credenciales necesarias para utilizar un servidor de licencias DRM de Primetime.
