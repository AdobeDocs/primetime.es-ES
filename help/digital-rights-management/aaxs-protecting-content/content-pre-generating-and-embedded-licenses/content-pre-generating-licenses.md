---
title: Licencias de pregeneración
description: Licencias de pregeneración
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Licencias de pregeneración{#pre-generating-licenses}

Para generar licencias previamente, utilice `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` para obtener una instancia de `LicenseFactory`. Se debe especificar una credencial del servidor de licencias para firmar las licencias generadas por esta fábrica. Esta clase admite la generación de licencias Leaf sin encadenamiento de licencias y licencias Leaf y Root con la [Campaña de licencias mejorada](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md).

Al generar una licencia de hoja, los metadatos de contenido deben especificarse mediante `initContentInfo()`. Si los metadatos incluyen varias directivas o si desea utilizar una directiva que no estaba en los metadatos, utilice `setSelectedPolicy()` para especificar la directiva que se debe utilizar para generar la licencia. Si utiliza una Lista de actualización de directivas para realizar un seguimiento de las actualizaciones de las directivas, puede proporcionar la Lista de actualización de directivas a la Fábrica de licencias antes de inicializar los metadatos mediante `setPolicyUpdateList()`.

Al generar una licencia Root, los metadatos de contenido se pueden especificar como se describe anteriormente. Alternativamente, se puede generar una licencia de raíz mediante una directiva ( `setSelectedPolicy()`) y la URL del servidor de licencias ( `setLicenseServerURL()`) en lugar de los metadatos.

>[!NOTE]
>
>Se requiere una URL de servidor de licencias incluso si no hay ningún servidor de licencias de acceso a Adobe desde el que los clientes puedan solicitar una licencia. En este caso, la URL del servidor de licencias debe especificar una URL que identifique al emisor de la licencia.

Si la directiva utiliza el encadenado de licencias mejorado, debe especificarse una credencial del servidor de licencias para descifrar la clave de cifrado raíz en la directiva ( `setRootKeyRetrievalInfo()`).

Si la directiva requiere una licencia enlazada al dominio, utilice `setDomainCAs()` para especificar los emisores de dominio desde los que el servidor de licencias aceptará tokens de dominio. Se deben proporcionar uno o más certificados de CA de dominio para validar el destinatario de la licencia.

Si la directiva requiere el envío de claves remotas para dispositivos iOS, el certificado de servidor clave debe proporcionarse mediante `setKeyServerCertificate()`, a menos que se genere una hoja encadenada.

Para generar una licencia, invoque `generateLicense()` y especifique el tipo de licencia (hoja o raíz) y uno o más certificados de destinatario. El certificado de destinatario será un certificado de equipo o de dominio, según los requisitos especificados en la directiva. Si está generando una hoja encadenada, no se requiere un destinatario. Una vez generada la licencia, es posible anular las reglas de uso especificadas en la directiva. Finalmente, invoque `signLicense()` para firmar la licencia y obtener una instancia de `PreGeneratedLicense`. La licencia ahora se puede guardar en un archivo (utilice `getBytes()` para recuperar la licencia serializada) o incrustar en contenido cifrado. Consulte [Incrustar licencias](../../aaxs-protecting-content/content-pre-generating-and-embedded-licenses/content-embedding-licenses.md).

Para obtener un ejemplo de código que demuestre las licencias pregeneradas, consulte `com.adobe.flashaccess.samples.licensegen.GenerateLicense` en el directorio Ejemplos de las herramientas de la línea de comandos de implementación de referencia.
