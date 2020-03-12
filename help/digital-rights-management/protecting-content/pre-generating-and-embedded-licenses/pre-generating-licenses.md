---
description: Si utiliza Adobe Primetime DRM Professional, puede generar previamente licencias e incrustar licencias en el contenido. Esta función se puede combinar con Encadenado de licencias mejorado, de modo que una licencia de hoja se pregenera e incrusta en el contenido, y el cliente puede solicitar una licencia de raíz (enlazada a un equipo o dominio) desde un servidor de licencias. Como alternativa, las aplicaciones cliente pueden implementar un flujo de trabajo en el que el dispositivo se registra previamente con un servidor, el servidor genera previamente licencias que están enlazadas a ese dispositivo y el cliente recupera sus licencias desde un servidor web HTTP sencillo.
seo-description: Si utiliza Adobe Primetime DRM Professional, puede generar previamente licencias e incrustar licencias en el contenido. Esta función se puede combinar con Encadenado de licencias mejorado, de modo que una licencia de hoja se pregenera e incrusta en el contenido, y el cliente puede solicitar una licencia de raíz (enlazada a un equipo o dominio) desde un servidor de licencias. Como alternativa, las aplicaciones cliente pueden implementar un flujo de trabajo en el que el dispositivo se registra previamente con un servidor, el servidor genera previamente licencias que están enlazadas a ese dispositivo y el cliente recupera sus licencias desde un servidor web HTTP sencillo.
seo-title: Licencias de pregeneración
title: Licencias de pregeneración
uuid: aa7d5038-5a9b-40a2-a240-266622158b43
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Licencias de pregeneración {#pre-generating-licenses}

Si utiliza Adobe Primetime DRM Professional, puede generar previamente licencias e incrustar licencias en el contenido. Esta función se puede combinar con Encadenado de licencias mejorado, de modo que una licencia de hoja se pregenera e incrusta en el contenido, y el cliente puede solicitar una licencia de raíz (enlazada a un equipo o dominio) desde un servidor de licencias. Como alternativa, las aplicaciones cliente pueden implementar un flujo de trabajo en el que el dispositivo se registra previamente con un servidor, el servidor genera previamente licencias que están enlazadas a ese dispositivo y el cliente recupera sus licencias desde un servidor web HTTP sencillo.

Si desea generar licencias previamente, debe utilizar `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` para obtener una instancia de `LicenseFactory`. Debe especificar una credencial del servidor de licencias para firmar las licencias generadas por esta fábrica. Esta clase admite la generación de licencias Leaf sin encadenamiento de licencias y licencias Leaf y Root con la cadena de licencias [Mejorado](../../protecting-content/implementing-the-license-server/license-chaining/gen-enhanced-license-chaining.md).

Al generar una licencia de hoja, debe especificar los metadatos de contenido que se aplican `initContentInfo()`. Si los metadatos incluyen varias directivas DRM o si desea utilizar una directiva DRM que no se ha incluido en los metadatos, debe utilizar `setSelectedPolicy()` para especificar la directiva DRM para generar una licencia. Si utiliza una lista de actualización de directivas de DRM para rastrear las actualizaciones de las directivas de DRM, puede proporcionar la lista de actualización de directivas de DRM a la fábrica de licencias antes de inicializar los metadatos con `setPolicyUpdateList()`.

Al generar una licencia de raíz, debe especificar los metadatos de contenido como se describe anteriormente. También puede generar una licencia raíz aplicando una directiva DRM ( `setSelectedPolicy()`) y una URL de servidor de licencias ( `setLicenseServerURL()`) en lugar de metadatos.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Se requiere una URL de servidor de licencias aunque no haya ningún servidor de licencias DRM de Adobe Primetime desde el que los clientes puedan solicitar una licencia. En este caso, la URL del servidor de licencias debe especificar una URL que identifique al emisor de la licencia.

Si la directiva DRM utiliza el Encadenado de licencias mejorado, debe especificar una credencial del servidor de licencias para descifrar la clave de cifrado raíz en la directiva DRM ( `setRootKeyRetrievalInfo()`).

Si la directiva DRM requiere una licencia enlazada a dominio, debe utilizar `setDomainCAs()` para especificar los emisores de dominio desde los que el servidor de licencias acepta tokens de dominio. Se deben proporcionar uno o más certificados de CA de dominio para validar el destinatario de la licencia.

Si la directiva DRM requiere la entrega de claves remotas para dispositivos iOS, debe proporcionar el certificado de servidor de claves mediante la aplicación `setKeyServerCertificate()` a menos que se genere una hoja encadenada.

Si desea generar una licencia, debe invocar `generateLicense()` y especificar el tipo de licencia (hoja o raíz) y uno o varios certificados de destinatario. El certificado de destinatario representa un certificado de equipo o de dominio, según los requisitos especificados en la directiva DRM. Si genera una hoja encadenada, no se requiere un destinatario. Una vez generada la licencia, puede anular las reglas de uso especificadas en la directiva DRM. Finalmente, debe invocar `signLicense()` para firmar la licencia y obtener una instancia de `PreGeneratedLicense`. Ahora se puede guardar la licencia (utilizarla `getBytes()` para recuperar la licencia serializada o incrustada en contenido cifrado).

Consulte [Incrustación de licencias](../../protecting-content/pre-generating-and-embedded-licenses/embedding-licenses.md).

Consulte `com.adobe.flashaccess.samples.licensegen.GenerateLicense` en el directorio de &quot;muestras&quot; de las herramientas de la línea de comandos de implementación de referencia para obtener código de muestra sobre cómo mostrar las licencias pregeneradas.
