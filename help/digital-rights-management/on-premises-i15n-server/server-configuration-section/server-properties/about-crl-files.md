---
title: Acerca de los archivos CRL
description: Acerca de los archivos CRL
copied-description: true
exl-id: 126a323d-9433-4a1e-a617-2d3bbf717cce
source-git-commit: 6a00df9c061da43f6efa49d927873db629568597
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Acerca de los archivos CRL {#about-crl-files}

Para funcionar correctamente, los servidores de individualización y licencias deben tener varios archivos de lista de revocación de certificados (CRL) en la caché del disco en el servidor de aplicaciones en ejecución (por ejemplo, Tomcat). Los nuevos archivos CRL deben descargarse y almacenarse en caché en el disco de forma regular y programada. Si se permite que transcurra el período de validez de los archivos CRL en el disco, el servidor de individualización rechazará la individualización de los clientes y el servidor de licencias se negará a emitir licencias.

Las listas CRL almacenadas en caché en el disco deben tener nombres de archivo que coincidan con las direcciones URL correspondientes. Los caracteres especiales como los dos puntos &quot;:&quot; y las barras &quot;/&quot; se convierten en guiones bajos &quot;_&quot; en los nombres de archivo.

A continuación se muestra una lista de CRL alojadas externamente que utilizan los servidores de individualización y de licencias:

* **CRL intermedio:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl>]
   * Archivo: [!DNL http___crl2.adobe.com_Adobe_FlashAccessIntermediateCA.crl]
   * Validez: válida durante aproximadamente 12 meses desde la creación.

* **CRL raíz:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl>]
   * Archivo: [!DNL http___crl2.adobe.com_Adobe_FlashAccessRootCA.crl]
   * Validez: válida durante aproximadamente 5 años a partir de la creación.

* **Última CRL:**

   * URL: [!DNL <ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl>]
   * Archivo: [!DNL http___crl3.adobe.com_AdobeSystemsIncorporatedFlashAccessRuntime_LatestCRL.crl]
   * Validez: válida durante aproximadamente 3 meses desde la creación.

Para obtener información sobre las CRL alojadas externamente que pueden utilizar los servidores de licencias, póngase en contacto con el Soporte técnico de Adobe.

<!---

Commenting out because of a security vulnerability reported in Jira PSIRT-20689. 

The following are externally hosted CRLs that are used only by the License Servers:

* URL: `https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl`

* File: `http___crl2.adobe.com_Adobe_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

* URL: `https://individualization-crl.primetime.adobe.com/FlashAccessIndividualizationCA.crl`

* File: `http___individualization-crl.primetime.adobe.com_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

* URL: `https://individualization-crl.s3-website-us-east-1.amazonaws.com/FlashAccessIndividualizationCA.crl`

* File: `http___individualization-crl.s3-website-us-east-1.amazonaws.com_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

--->

Además de las CRL alojadas externamente, puede crear y mantener una CRL adicional. Esta es la CRL de la CA de individualización, como se especifica en la [Crear CRL de CA de individualización](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) de este documento.

Se ha programado la actualización de las CRL 45 días antes de que caduquen. Esto debería permitirle disponer de tiempo suficiente para adquirir e instalar CRL recién generadas desde Internet. Debe tener cuidado de actualizar los archivos CRL antes de que caduquen.
