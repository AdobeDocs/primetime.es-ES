---
title: Entrega de código / Contenido del paquete
description: Entrega de código / Contenido del paquete
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Entrega de código / Contenido del paquete{#code-delivery-package-contents}

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

