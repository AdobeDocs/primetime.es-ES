---
description: Si utiliza Adobe Primetime DRM Professional, puede generar previamente licencias e incrustar licencias en el contenido. Esta función se puede combinar con el encadenamiento de licencias mejorado, de modo que una licencia de hoja se genera previamente y se incrusta en el contenido, y el cliente puede solicitar una licencia de raíz (enlazada a un equipo o dominio) desde un servidor de licencias. Como alternativa, las aplicaciones cliente pueden implementar un flujo de trabajo en el que el dispositivo se registra previamente con un servidor, el servidor genera previamente las licencias enlazadas a dicho dispositivo y el cliente recupera sus licencias desde un simple servidor web HTTP.
title: Generación previa de licencias
exl-id: 6ced7dde-b4bb-470d-bdae-3042f5577b67
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# Generación previa de licencias {#pre-generating-licenses}

Si utiliza Adobe Primetime DRM Professional, puede generar previamente licencias e incrustar licencias en el contenido. Esta función se puede combinar con el encadenamiento de licencias mejorado, de modo que una licencia de hoja se genera previamente y se incrusta en el contenido, y el cliente puede solicitar una licencia de raíz (enlazada a un equipo o dominio) desde un servidor de licencias. Como alternativa, las aplicaciones cliente pueden implementar un flujo de trabajo en el que el dispositivo se registra previamente con un servidor, el servidor genera previamente las licencias enlazadas a dicho dispositivo y el cliente recupera sus licencias desde un simple servidor web HTTP.

Si desea generar licencias previamente, debe utilizar `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` para obtener una instancia de `LicenseFactory`. Debe especificar una credencial de servidor de licencias para firmar las licencias generadas por esta fábrica. Esta clase admite la generación de licencias Hoja sin encadenamiento de licencias y licencias Hoja y Raíz con el [Encadenamiento de licencias mejorado](../../protecting-content/implementing-the-license-server/license-chaining/gen-enhanced-license-chaining.md).

Al generar una licencia de Leaf, debe especificar los metadatos de contenido que se aplican `initContentInfo()`. Si los metadatos incluyen varias políticas de DRM o si desea utilizar una política de DRM que no se haya incluido en los metadatos, debe utilizar `setSelectedPolicy()` para especificar la directiva DRM para generar una licencia. Si utiliza una lista de actualización de directivas DRM para realizar el seguimiento de las actualizaciones de directivas DRM, puede proporcionar la lista de actualización de directivas DRM a la fábrica de licencias antes de inicializar los metadatos con `setPolicyUpdateList()`.

Al generar una licencia de usuario root, debe especificar los metadatos de contenido tal como se ha descrito anteriormente. También puede generar una licencia raíz aplicando una directiva DRM ( `setSelectedPolicy()`) y una URL de servidor de licencias ( `setLicenseServerURL()`) en lugar de metadatos.

>[!NOTE]
>
>Se requiere una URL de servidor de licencias aunque no haya un servidor de licencias DRM de Adobe Primetime desde el que los clientes puedan solicitar una licencia. En este caso, la URL del servidor de licencias debe especificar una URL que identifique al emisor de la licencia.

Si la directiva DRM utiliza el encadenamiento de licencias mejorado, debe especificar una credencial del servidor de licencias para descifrar la clave de cifrado raíz en la directiva DRM ( `setRootKeyRetrievalInfo()`).

Si la directiva DRM requiere una licencia enlazada al dominio, debe utilizar `setDomainCAs()` para especificar los emisores de dominio desde los que el servidor de licencias acepta tokens de dominio. Se deben proporcionar uno o más certificados de CA de dominio para validar el destinatario de la licencia.

Si la directiva DRM requiere la entrega de claves remotas para dispositivos iOS, debe proporcionar el certificado de servidor de claves aplicando `setKeyServerCertificate()` a menos que se genere una hoja encadenada.

Si desea generar una licencia, debe invocar `generateLicense()` y especifique el tipo de licencia (hoja o raíz) y uno o más certificados de destinatario. El certificado de destinatario representa un certificado de equipo o de dominio, según los requisitos especificados en la directiva DRM. Si genera una hoja encadenada, no es necesario un destinatario. Una vez generada la licencia, puede anular las reglas de uso especificadas en la directiva DRM. Finalmente, debe invocar `signLicense()` para firmar la licencia y obtener una instancia de `PreGeneratedLicense`. Ahora se puede guardar la licencia (utilice `getBytes()` para recuperar la licencia serializada o incrustada en contenido cifrado.

Consulte [Incrustación de licencias](../../protecting-content/pre-generating-and-embedded-licenses/embedding-licenses.md).

Consulte `com.adobe.flashaccess.samples.licensegen.GenerateLicense` en el directorio &quot;samples&quot; de las herramientas de línea de comandos de implementación de referencia para obtener código de muestra sobre cómo mostrar las licencias generadas previamente.
