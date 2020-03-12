---
seo-title: Acerca de los archivos CRL
title: Acerca de los archivos CRL
uuid: 672c3ca0-5c5d-4ec7-83b1-f0f8e34c8d09
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Acerca de los archivos CRL {#about-crl-files}

Para funcionar correctamente, los servidores de personalización y licencia necesitan tener varios archivos de lista de revocación de certificados (CRL) en caché en disco en el servidor de aplicaciones en ejecución (por ejemplo, Tomcat). Los nuevos archivos CRL deben descargarse y almacenarse en caché en el disco de forma regular y programada. Si se permite que caduque el período de validez de los archivos CRL en el disco, el servidor de individualización se negará a individualizar los clientes y el servidor de licencias se negará a emitir licencias.

Las CRL almacenadas en caché en disco deben tener nombres de archivo que coincidan con las URL correspondientes. Los caracteres especiales como los dos puntos &#39;:&#39; y &#39;/&#39; se convierten en caracteres de subrayado &#39;_&#39; en los nombres de archivo.

A continuación se muestra una lista de CRL alojadas externamente que utilizan tanto los servidores de personalización como los de licencias:

* **CRL intermedia:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl>]
   * Archivo: [!DNL http___crl2.adobe.com_Adobe_FlashAccessIntermediateCA.crl]
   * Validez: Buena durante aproximadamente 12 meses desde su creación

* **CRL raíz:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl>]
   * Archivo: [!DNL http___crl2.adobe.com_Adobe_FlashAccessRootCA.crl]
   * Validez: Bueno para aproximadamente 5 años desde la creación

* **Última CRL:**

   * URL: [!DNL <ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl>]
   * Archivo: [!DNL http___crl3.adobe.com_AdobeSystemsIncorporatedFlashAccessRuntime_LatestCRL.crl]
   * Validez: Buena para aproximadamente 3 meses desde la creación

Las siguientes son CRL alojadas externamente que solo utilizan los servidores de licencias:

* URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl>]
* Archivo: [!DNL http___crl2.adobe.com_Adobe_FlashAccessIndividualizationCA.crl]
* Validez: Buena para aproximadamente 3 meses desde la creación

* URL: [!DNL <ht<span></span>tps://individualization-crl.primetime.adobe.com/FlashAccessIndividualizationCA.crl>]
* Archivo: [!DNL http___individualization-crl.primetime.adobe.com_FlashAccessIndividualizationCA.crl]
* Validez: Buena para aproximadamente 3 meses desde la creación

* URL: [!DNL <ht<span></span>tps://individualization-crl.s3-website-us-east-1.amazonaws.com/FlashAccessIndividualizationCA.crl]>
* Archivo: [!DNL http___individualization-crl.s3-website-us-east-1.amazonaws.com_FlashAccessIndividualizationCA.crl]
* Validez: Buena para aproximadamente 3 meses desde la creación

Además de las CRL mencionadas, debe crear y mantener una CRL adicional. Esta es la CRL de CA de individualización, tal como se especifica en la sección [Crear CRL](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) de CA de individualización de este documento.

Las listas de revocaciones de certificados (CRL) se actualizarán 45 días antes de que caduquen. Esto le permitirá disponer de tiempo suficiente para adquirir e instalar listas CRL recién generadas desde Internet. Debe asegurarse de actualizar los archivos CRL antes de que caduquen.
