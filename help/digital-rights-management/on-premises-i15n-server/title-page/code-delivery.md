---
seo-title: Envío de código/Contenido del paquete
title: Envío de código/Contenido del paquete
uuid: 13de2fd4-9079-496c-a087-25176c118864
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Envío de código/Contenido del paquete{#code-delivery-package-contents}

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

