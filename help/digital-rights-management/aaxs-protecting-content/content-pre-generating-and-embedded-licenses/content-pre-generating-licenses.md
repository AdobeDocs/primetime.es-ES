---
title: Generación previa de licencias
description: Generación previa de licencias
copied-description: true
exl-id: 2be8674c-736f-4ed3-b952-f661bf3ff48f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# Generación previa de licencias{#pre-generating-licenses}

Para generar licencias previamente, utilice `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` para obtener una instancia de `LicenseFactory`. Se debe especificar una credencial de servidor de licencias para firmar las licencias generadas por esta fábrica. Esta clase admite la generación de licencias Hoja sin encadenamiento de licencias y licencias Hoja y Raíz con el [Encadenamiento de licencias mejorado](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md).

Al generar una licencia Leaf, los metadatos de contenido deben especificarse utilizando `initContentInfo()`. Si los metadatos incluyen varias directivas o si desea utilizar una directiva que no estaba en los metadatos, utilice `setSelectedPolicy()` para especificar la directiva que se va a utilizar para generar la licencia. Si utiliza una Lista de actualización de directivas para realizar el seguimiento de las actualizaciones de directivas, puede proporcionar la Lista de actualización de directivas a la Fábrica de licencias antes de inicializar los metadatos mediante `setPolicyUpdateList()`.

Al generar una licencia raíz, los metadatos de contenido se pueden especificar tal como se ha descrito anteriormente. Como alternativa, se puede generar una licencia raíz mediante una directiva ( `setSelectedPolicy()`) y la URL del servidor de licencias ( `setLicenseServerURL()`) en lugar de los metadatos.

>[!NOTE]
>
>Se requiere una URL de servidor de licencias aunque no haya un servidor de licencias de acceso a Adobe desde el que los clientes puedan solicitar una licencia. En este caso, la URL del servidor de licencias debe especificar una URL que identifique al emisor de la licencia.

Si la directiva utiliza el encadenamiento de licencias mejorado, se debe especificar una credencial del servidor de licencias para descifrar la clave de cifrado raíz en la directiva ( `setRootKeyRetrievalInfo()`).

Si la directiva requiere una licencia enlazada al dominio, utilice `setDomainCAs()` para especificar los emisores de dominio desde los que el servidor de licencias aceptará tokens de dominio. Se deben proporcionar uno o más certificados de CA de dominio para validar el destinatario de la licencia.

Si la directiva requiere la entrega de claves remotas para dispositivos iOS, se debe proporcionar el certificado de servidor de claves utilizando `setKeyServerCertificate()`, a menos que se genere una hoja encadenada.

Para generar una licencia, invoque `generateLicense()` y especifique el tipo de licencia (hoja o raíz) y uno o más certificados de destinatario. El certificado de destinatario será un certificado de equipo o de dominio, según los requisitos especificados en la directiva. Si está generando una hoja encadenada, no es necesario un destinatario. Una vez generada la licencia, es posible anular las reglas de uso especificadas en la directiva. Finalmente, invocar `signLicense()` para firmar la licencia y obtener una instancia de `PreGeneratedLicense`. La licencia ahora se puede guardar en un archivo (utilice `getBytes()` para recuperar la licencia serializada) o incrustada en contenido cifrado. Consulte. [Incrustación de licencias](../../aaxs-protecting-content/content-pre-generating-and-embedded-licenses/content-embedding-licenses.md).

Para ver el código de muestra que muestra las licencias generadas previamente, consulte `com.adobe.flashaccess.samples.licensegen.GenerateLicense` en el directorio &quot;samples&quot; de Herramientas de línea de comandos de implementación de referencia.
