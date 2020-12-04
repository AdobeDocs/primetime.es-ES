---
seo-title: Archivo de configuración del inquilino
title: Archivo de configuración del inquilino
uuid: 6e5c82c9-b8f5-4fca-8325-a884b2c779f7
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---


# Archivo de configuración del inquilino {#tenant-configuration-file}

El archivo de configuración flashaccess-tenant.xml contiene opciones que se aplican a un inquilino específico del servidor de licencias. Cada inquilino tiene su propia instancia de este archivo de configuración ubicada en *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*nombre del inquilino*. Consulte el directorio [!DNL configs/flashaccessserver/tenants/sampletenant] para ver un archivo de configuración de inquilino de ejemplo.

Puede especificar todas las rutas de archivo del archivo de configuración del inquilino como rutas absolutas o rutas relativas al directorio de configuración del inquilino (*LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*nombre del inquilino*).

El archivo de configuración del inquilino incluye:

* **Credenciales**  de transporte— Especifica una o varias credenciales de transporte (certificado y clave privada) emitidas por Adobe. Se puede especificar como una ruta a un archivo .pfx y una contraseña, o un alias para una credencial almacenada en un HSM. Aquí se pueden especificar varias credenciales de este tipo, ya sea como rutas de archivos, alias de claves o ambas. Consulte &quot;[Administración de actualizaciones de certificados](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-cert-updates.md)&quot; en *Uso del SDK de Adobe Access para la protección de contenido* para obtener más información sobre cuándo se necesitan credenciales adicionales.
* **Credencial**  del servidor de licencias: Especifica una o varias credenciales del servidor de licencias (certificado y clave privada) emitidas por Adobe. Se puede especificar como una ruta a un archivo .pfx y una contraseña, o un alias para una credencial almacenada en un HSM. Aquí se pueden especificar varias credenciales de este tipo, ya sea como rutas de archivos, alias de claves o ambas. Consulte Gestión de actualizaciones de certificados en *Uso del SDK de Adobe Access para la protección de contenido *para obtener más información sobre cuándo se necesitan credenciales adicionales.
* **Certificados**  de servidor clave— Opcional. Especifica el certificado del servidor de licencias de Key Server emitido por Adobe. Se puede especificar como una ruta a un archivo .cer o un alias a un certificado almacenado en un HSM. Esta opción debe especificarse para poder emitir licencias para contenido empaquetado con una política que requiera envío de claves remotas para dispositivos iOS.
* **Autorizadores**  personalizados: Opcional. Especifica las clases de autorizador personalizadas que se invocarán para cada solicitud de licencia. Si se especifican varios autorizadores, se invocan en el orden en que aparecen. Para obtener más información, consulte &quot;[Extensiones de autorización personalizadas](../../aaxs-protected-streaming/custom-authorization-extensions.md)&quot;.
* **Lista de envases**  autorizados— Opcional. Especifica certificados que identifican entidades autorizadas para empaquetar contenido para este servidor de licencias. Si no se especifica ningún certificado de empaquetador, el servidor emite licencias para contenido empaquetado por cualquier empaquetador.
* **Versión**  mínima del cliente admitida (consulte  *Uso del SDK de Adobe Access para la protección de contenido*).
* **Reglas de uso**

   * **Almacenamiento en caché**  de licencias: Opcional. Especifica cuánto tiempo se puede almacenar la licencia en el cliente. De forma predeterminada, el almacenamiento en caché de licencias está desactivado. Para habilitar el almacenamiento en caché de licencias durante un período de tiempo limitado, establezca la fecha de finalización o el número de segundos durante los que se debe almacenar la licencia (comenzando cuando se emita la licencia). Si se establece el número de segundos en 0, se deshabilita la caché de licencias.

      Tenga en cuenta que todas las licencias emitidas por el servidor para flujo protegido tienen un período de caducidad de 24 horas (86400 segundos). Por lo tanto, este valor se aplica implícitamente como límite superior a cualquier fecha o duración de finalización que se establezca también para el almacenamiento en caché de licencias, con un valor máximo de 86400 segundos, aunque el esquema aplique límites superiores.

   * **Reproducir a la derecha** : Se debe especificar al menos un derecho. Si se especifican varios derechos, el cliente utilizará el primer derecho para el que cumpla todos los requisitos.

      * **Protección**  de salida: Controla si se debe proteger la salida a dispositivos de procesamiento externos.
      * **Restricciones**  de aplicaciones AIR y SWF: Lista de permitidos opcional de aplicaciones SWF y AIR que pueden reproducir el contenido (es decir, solo se permiten las aplicaciones especificadas). Las aplicaciones SWF se identifican mediante una URL o mediante el compendio del SWF y el tiempo máximo para permitir la descarga y verificación del compendio. Para obtener información sobre el cálculo del compendio SWF, consulte la sección &quot;Calculadora de hash SWF&quot;. Las aplicaciones de AIR e iOS se identifican mediante un ID de editor y un ID de aplicación opcional, una versión mínima y una versión máxima. Si no se especifican restricciones de aplicación, cualquier aplicación SWF o AIR puede reproducir el contenido.
      * **Restricciones**  de módulos DRM y Runtime: Especifica el nivel de seguridad mínimo necesario para el módulo DRM/Runtime. Opcionalmente, incluye una lista de bloqueados de versiones que no pueden reproducir el contenido. Las versiones de módulos se identifican mediante atributos como sistema operativo y/o número de versión. Las restricciones del módulo DRM y las restricciones del módulo de tiempo de ejecución ahora admiten los atributos adicionales siguientes:

         * `oemVendor`
         * `model`
         * `screenType`

         Los siguientes atributos ahora son opcionales:

         * `osVersion`
         * `version`
      * **Requisitos**  de capacidad del dispositivo: De forma opcional, especifica las capacidades de hardware necesarias para acceder al contenido.
      * **Requisitos**  de detección de saltos de cárcel: De forma opcional, especifica que no se permite la reproducción en dispositivos en los que se detecta un salto de página.



Consulte los comentarios en el archivo de configuración del inquilino de ejemplo para obtener más información.
