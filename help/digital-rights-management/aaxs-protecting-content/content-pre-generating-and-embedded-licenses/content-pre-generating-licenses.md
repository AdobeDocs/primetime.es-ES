---
seo-title: Licencias de pregeneración
title: Licencias de pregeneración
uuid: 31430753-11f1-4ce5-b402-cf4279119a05
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Licencias de pregeneración{#pre-generating-licenses}

Para generar licencias previamente, utilice `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` para obtener una instancia de `LicenseFactory`. Se debe especificar una credencial del servidor de licencias para firmar las licencias generadas por esta fábrica. Esta clase admite la generación de licencias Leaf sin encadenamiento de licencias y licencias Leaf y Root con la cadena de licencias [Mejorado](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md).

Al generar una licencia de hoja, los metadatos de contenido deben especificarse mediante `initContentInfo()`. Si los metadatos incluyen varias directivas, o si desea utilizar una directiva que no estaba en los metadatos, utilice `setSelectedPolicy()` para especificar la directiva que se va a usar para generar la licencia. Si utiliza una lista de actualización de directivas para realizar un seguimiento de las actualizaciones de directivas, puede proporcionar la lista de actualización de directivas a la fábrica de licencias antes de inicializar los metadatos mediante `setPolicyUpdateList()`.

Al generar una licencia de raíz, los metadatos de contenido se pueden especificar como se describe anteriormente. De forma alternativa, se puede generar una licencia raíz mediante una directiva ( `setSelectedPolicy()`) y una URL del servidor de licencias ( `setLicenseServerURL()`) en lugar de los metadatos.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Se requiere una URL de servidor de licencias aunque no haya ningún servidor de licencias de Adobe Access desde el que los clientes puedan solicitar una licencia. En este caso, la URL del servidor de licencias debe especificar una URL que identifique al emisor de la licencia.

Si la directiva utiliza el encadenado de licencias mejorado, se debe especificar una credencial del servidor de licencias para descifrar la clave de cifrado raíz en la directiva ( `setRootKeyRetrievalInfo()`).

Si la política requiere una licencia enlazada a dominio, utilice `setDomainCAs()` para especificar los emisores de dominio desde los que el servidor de licencias aceptará tokens de dominio. Se deben proporcionar uno o más certificados de CA de dominio para validar el destinatario de la licencia.

Si la directiva requiere la entrega de claves remotas para dispositivos iOS, se debe proporcionar el certificado de servidor de claves mediante `setKeyServerCertificate()`el uso de , a menos que se esté generando una hoja encadenada.

Para generar una licencia, invoque `generateLicense()` y especifique el tipo de licencia (hoja o raíz) y uno o varios certificados de destinatario. El certificado de destinatario será un certificado de equipo o de dominio, según los requisitos especificados en la directiva. Si está generando una hoja encadenada, no se requiere un destinatario. Una vez generada la licencia, es posible anular las reglas de uso especificadas en la directiva. Finalmente, invoque `signLicense()` para firmar la licencia y obtener una instancia de `PreGeneratedLicense`. Ahora la licencia se puede guardar en un archivo (utilizar `getBytes()` para recuperar la licencia serializada) o incrustar en contenido cifrado. Consulte [Incrustación de licencias](../../aaxs-protecting-content/content-pre-generating-and-embedded-licenses/content-embedding-licenses.md).

Para obtener un código de muestra que demuestre las licencias pregeneradas, consulte `com.adobe.flashaccess.samples.licensegen.GenerateLicense` en el directorio Reference Implementation Command Line Tools &quot;samples&quot; (Ejemplos).
