---
seo-title: Licencias de pregeneración
title: Licencias de pregeneración
uuid: 31430753-11f1-4ce5-b402-cf4279119a05
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Licencias de pregeneración{#pre-generating-licenses}

Para generar licencias previamente, utilice `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` para obtener una instancia de `LicenseFactory`. Se debe especificar una credencial del servidor de licencias para firmar las licencias generadas por esta fábrica. Esta clase admite la generación de licencias Leaf sin encadenamiento de licencias y licencias Leaf y Root con la [cadena de licencias mejorada](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md).

Al generar una licencia de hoja, los metadatos de contenido deben especificarse mediante `initContentInfo()`. Si los metadatos incluyen varias directivas o si desea utilizar una directiva que no estaba en los metadatos, utilice `setSelectedPolicy()` para especificar la directiva que se usará para generar la licencia. Si utiliza una Lista de actualización de directiva para realizar el seguimiento de las actualizaciones de directivas, puede proporcionar la Lista de actualización de directiva a la fábrica de licencias antes de inicializar los metadatos mediante `setPolicyUpdateList()`.

Al generar una licencia de raíz, los metadatos de contenido se pueden especificar como se describe anteriormente. De forma alternativa, se puede generar una licencia de raíz mediante una directiva ( `setSelectedPolicy()`) y una URL del servidor de licencias ( `setLicenseServerURL()`) en lugar de los metadatos.

>[!NOTE]
>
>Se requiere una URL de servidor de licencias aunque no haya ningún servidor de licencias de acceso a Adobe desde el que los clientes puedan solicitar una licencia. En este caso, la URL del servidor de licencias debe especificar una URL que identifique al emisor de la licencia.

Si la directiva utiliza el encadenado de licencias mejorado, se debe especificar una credencial del servidor de licencias para descifrar la clave de cifrado raíz en la directiva ( `setRootKeyRetrievalInfo()`).

Si la directiva requiere una licencia enlazada a dominio, utilice `setDomainCAs()` para especificar los emisores de dominio desde los que el servidor de licencias aceptará tokens de dominio. Se deben proporcionar uno o más certificados de CA de dominio para validar el destinatario de licencia.

Si la directiva requiere envío de clave remota para dispositivos iOS, el certificado de servidor de claves debe proporcionarse mediante `setKeyServerCertificate()`, a menos que se genere una hoja encadenada.

Para generar una licencia, invoque `generateLicense()` y especifique el tipo de licencia (hoja o raíz) y uno o varios certificados de destinatario. El certificado de destinatario será un certificado de equipo o de dominio, según los requisitos especificados en la directiva. Si está generando una hoja encadenada, no es necesario un destinatario. Una vez generada la licencia, es posible anular las reglas de uso especificadas en la directiva. Finalmente, invoque `signLicense()` para firmar la licencia y obtener una instancia de `PreGeneratedLicense`. Ahora la licencia se puede guardar en un archivo (utilice `getBytes()` para recuperar la licencia serializada) o incrustar en contenido cifrado. Consulte [Incrustar licencias](../../aaxs-protecting-content/content-pre-generating-and-embedded-licenses/content-embedding-licenses.md).

Para obtener un código de muestra que demuestre las licencias pregeneradas, consulte `com.adobe.flashaccess.samples.licensegen.GenerateLicense` en el directorio &quot;samples&quot; de la línea de comandos de implementación de referencia.
