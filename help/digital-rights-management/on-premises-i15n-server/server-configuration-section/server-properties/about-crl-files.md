---
title: Acerca de los archivos CRL
description: Acerca de los archivos CRL
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Acerca de los archivos CRL {#about-crl-files}

Para funcionar correctamente, los servidores de Individualización y Licencia deben tener varios archivos de Lista de Revocación de Certificados (CRL) en caché en disco en el servidor de aplicaciones en ejecución (por ejemplo, Tomcat). Los nuevos archivos CRL deben descargarse y almacenarse en caché en disco de forma regular y programada. Si se permite que caduque el periodo de validez de los archivos CRL en el disco, el servidor de individualización se negará a individualizar clientes y el servidor de licencias se negará a emitir licencias.

Las CRL almacenadas en caché en disco deben tener nombres de archivo que coincidan con las URL correspondientes. Los caracteres especiales, como los dos puntos &#39;:&#39; y &#39;/&#39;, se convierten en guiones bajos &#39;_&#39; en los nombres de archivo.

A continuación se muestra una lista de CRL alojadas externamente que utilizan los servidores de Individualización y de Licencias:

* **CRL intermedia:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl>]
   * Archivo: [!DNL http___crl2.adobe.com_Adobe_FlashAccessIntermediateCA.crl]
   * Validez: Bueno durante aproximadamente 12 meses desde la creación

* **CRL raíz:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl>]
   * Archivo: [!DNL http___crl2.adobe.com_Adobe_FlashAccessRootCA.crl]
   * Validez: Positivo aproximadamente 5 años después de la creación

* **Última CRL:**

   * URL: [!DNL <ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl>]
   * Archivo: [!DNL http___crl3.adobe.com_AdobeSystemsIncorporatedFlashAccessRuntime_LatestCRL.crl]
   * Validez: Positivo aproximadamente 3 meses después de la creación

Las siguientes son listas CRL alojadas externamente que solo utilizan los servidores de licencias:

* URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl>]
* Archivo: [!DNL http___crl2.adobe.com_Adobe_FlashAccessIndividualizationCA.crl]
* Validez: Positivo aproximadamente 3 meses después de la creación

* URL: [!DNL <ht<span></span>tps://individualization-crl.primetime.adobe.com/FlashAccessIndividualizationCA.crl>]
* Archivo: [!DNL http___individualization-crl.primetime.adobe.com_FlashAccessIndividualizationCA.crl]
* Validez: Positivo aproximadamente 3 meses después de la creación

* URL: [!DNL <ht<span></span>tps://individualization-crl.s3-website-us-east-1.amazonaws.com/FlashAccessIndividualizationCA.crl]
* Archivo: [!DNL http___individualization-crl.s3-website-us-east-1.amazonaws.com_FlashAccessIndividualizationCA.crl]
* Validez: Positivo aproximadamente 3 meses después de la creación

Además de las CRL mencionadas, debe crear y mantener una CRL adicional. Esta es la CRL de CA de Individualización, tal como se especifica en la sección [Create Individualization CA CRL](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) de este documento.

Las listas CRL se actualizarán 45 días antes de que caduquen. Esto debería permitirle disponer de tiempo suficiente para adquirir e instalar listas CRL recién generadas desde Internet. Debe tener cuidado de actualizar los archivos CRL antes de que caduquen.
