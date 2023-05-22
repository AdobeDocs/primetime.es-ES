---
title: Archivo de configuración de inquilino
description: Archivo de configuración de inquilino
copied-description: true
exl-id: 0f6cafbe-99d9-43bc-9a7f-d87c4da1f37f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---

# Archivo de configuración de inquilino {#tenant-configuration-file}

El archivo de configuración flashaccess-tenant.xml contiene opciones que se aplican a un inquilino específico del servidor de licencias. Cada inquilino tiene su propia instancia de este archivo de configuración ubicado en *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*inquilino*. Consulte la [!DNL configs/flashaccessserver/tenants/sampletenant] para un archivo de configuración de inquilino de ejemplo.

Puede especificar todas las rutas de archivo en el archivo de configuración del inquilino como rutas absolutas o rutas relativas al directorio de configuración del inquilino (*LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*inquilino*).

El archivo de configuración de inquilino incluye:

* **Credencial de transporte** — especifica una o varias credenciales de transporte (certificado y clave privada) emitidas por el Adobe. Se puede especificar como una ruta a un archivo .pfx y una contraseña, o un alias para una credencial almacenada en un HSM. Aquí se pueden especificar varias credenciales de este tipo, como rutas de archivo, alias de clave o ambos. Consulte &quot;[Administrar actualizaciones de certificados](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-cert-updates.md)&quot; en *Uso del SDK de acceso a Adobe para proteger el contenido* para obtener más información sobre cuándo se necesitan credenciales adicionales.
* **Credenciales del servidor de licencias** — especifica una o varias credenciales del servidor de licencias (certificado y clave privada) emitidas por el Adobe. Se puede especificar como una ruta a un archivo .pfx y una contraseña, o un alias para una credencial almacenada en un HSM. Aquí se pueden especificar varias credenciales de este tipo, como rutas de archivo, alias de clave o ambos. Consulte Gestión de actualizaciones de certificados en *Uso del SDK de acceso a Adobe para proteger el contenido *para obtener más información sobre cuándo se necesitan credenciales adicionales.
* **Certificados de servidor clave** — Opcional. Especifica el certificado del servidor de licencias del servidor de claves emitido por el Adobe. Se puede especificar como ruta a un archivo .cer o como alias a un certificado almacenado en un HSM. Esta opción debe especificarse para emitir licencias para contenido empaquetado con una directiva que requiera la entrega de claves remotas para dispositivos iOS.
* **Autorizadores personalizados** — Opcional. Especifica las clases de autorizador personalizadas que se invocan para cada solicitud de licencia. Si se especifican varios autorizadores, se invocan en el orden indicado. Para obtener más información, consulte &quot;[Extensiones de autorización personalizadas](../../aaxs-protected-streaming/custom-authorization-extensions.md)&quot;.
* **Lista de empaquetadores autorizados** — Opcional. Especifica certificados que identifican entidades autorizadas para empaquetar contenido para este servidor de licencias. Si no se especifican certificados de empaquetador, el servidor emite licencias para el contenido empaquetado por cualquier empaquetador.
* **Versión de cliente mínima admitida** (Consulte *Uso del SDK de acceso a Adobe para proteger el contenido*).
* **Reglas de uso**

   * **Almacenamiento en caché de licencias** — Opcional. Especifica cuánto tiempo se puede almacenar la licencia en el cliente. De forma predeterminada, el almacenamiento en caché de licencias está deshabilitado. Para habilitar el almacenamiento en caché de licencias durante un período de tiempo limitado, establezca la fecha de finalización o el número de segundos durante los cuales se debe almacenar la licencia (a partir del momento en que se emite la licencia). Si establece el número de segundos en 0, se deshabilita el almacenamiento de licencias en caché.

      Tenga en cuenta que todas las licencias emitidas por el servidor para transmisión protegida tienen un periodo de caducidad de 24 horas (86400 segundos). Por lo tanto, este valor se aplica implícitamente como un límite superior a la fecha de finalización o duración establecida para el almacenamiento en caché de licencias, con un valor máximo de 86400 segundos, aunque el esquema aplique límites más altos.

   * **Reproducir a la derecha** — Se debe especificar al menos un derecho. Si se especifican varios derechos, el cliente utilizará el primer derecho para el que cumpla todos los requisitos.

      * **Protección de salida** — controla si la salida a dispositivos de renderización externos debe protegerse.
      * **Restricciones de aplicaciones de AIR y SWF** — lista de permitidos opcional de las aplicaciones de SWF y AIR que pueden reproducir el contenido (es decir, solo se permiten las aplicaciones especificadas). Las aplicaciones de SWF se identifican mediante una dirección URL o por el resumen del SWF y el tiempo máximo para permitir la descarga y verificación del compendio. Para obtener información sobre el cálculo del resumen de SWF, consulte la sección &quot;Calculadora de hash de SWF&quot;. Las aplicaciones de AIR y iOS se identifican mediante un ID de editor y un ID de aplicación opcional, una versión mínima y una versión máxima. Si no se especifican restricciones de aplicación, cualquier SWF o aplicación de AIR puede reproducir el contenido.
      * **Restricciones del módulo DRM y Runtime** — especifica el nivel de seguridad mínimo requerido para el módulo DRM/Runtime. Opcionalmente incluye una lista de bloqueados de versiones a las que no se les permite reproducir el contenido. Las versiones de los módulos se identifican mediante atributos como el sistema operativo o un número de versión. Las restricciones del módulo DRM y las restricciones del módulo Runtime ahora admiten los siguientes atributos adicionales:

         * `oemVendor`
         * `model`
         * `screenType`

         Los siguientes atributos ahora son opcionales:

         * `osVersion`
         * `version`
      * **Requisitos de capacidad del dispositivo** — especifica opcionalmente las capacidades de hardware necesarias para acceder al contenido.
      * **Requisitos de detección de jailbreak** — especifica de forma opcional que no se permite la reproducción en los dispositivos en los que se detecta una fuga.



Consulte los comentarios en el archivo de configuración del inquilino de ejemplo para obtener más información.
