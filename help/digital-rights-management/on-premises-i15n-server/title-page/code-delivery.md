---
title: Entrega de código/Contenido del paquete
description: Entrega de código/Contenido del paquete
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Entrega de código / Contenido del paquete{#code-delivery-package-contents}

El paquete Adobe Primetime DRM On Premies Individualization Server contiene lo siguiente:

* [!DNL flashaccess.war] - El Servidor De Individualización
* [!DNL flashaccess-kgs.war] - El servidor de generación de claves opcional
* [!DNL /shared] - Contiene:

   * [!DNL adobe-flashaccess-certs.jar]
   * [!DNL AdobeInitial.properties] - Archivo de propiedades de muestra

* [!DNL thirdparty/] - Incluye compatibilidad con Crypto-J como bibliotecas nativas:

   * [!DNL libjsafe.so] (Linux)
   * [!DNL jsafe.dll] (Windows)

* [!DNL adobe-flashaccess-i15n-setup.jar] - Utilidad para cifrar contraseñas de credenciales de servidor
* [!DNL ROOT] - contiene un  [!DNL crossdomain.xml] archivo

* Archivos de caché de ECI: predescargados
* [!DNL addIndivCert.py] - Un script para actualizar la raíz de confianza de un servidor de licencias para admitir las individualizaciones On Premies
* [!DNL CreateMetadata.jar] - Una utilidad para crear metadatos DRM locales
* [!DNL client_sample/] - Una carpeta con un fragmento de código de cliente
* Notas de la versión : para cualquier adición de última hora a la documentación

