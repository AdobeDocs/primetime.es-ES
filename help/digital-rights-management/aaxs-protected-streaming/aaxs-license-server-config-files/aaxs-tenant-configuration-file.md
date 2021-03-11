---
title: Archivo de configuración del inquilino
description: Archivo de configuración del inquilino
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---


# Archivo de configuración del inquilino {#tenant-configuration-file}

El archivo de configuración flashaccess-tenant.xml contiene opciones que se aplican a un inquilino específico del servidor de licencias. Cada inquilino tiene su propia instancia de este archivo de configuración ubicada en *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*nombre del inquilino*. Consulte el directorio [!DNL configs/flashaccessserver/tenants/sampletenant] para ver un archivo de configuración de inquilino de ejemplo.

Puede especificar todas las rutas de archivo del archivo de configuración del inquilino como rutas o rutas absolutas relativas al directorio de configuración del inquilino (*LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*nombre del inquilino*).

El archivo de configuración del inquilino incluye:

* **Credencial de transporte** : especifica una o más credenciales de transporte (certificado y clave privada) emitidas por el Adobe. Se puede especificar como una ruta a un archivo .pfx y una contraseña, o como un alias para una credencial almacenada en un HSM. Aquí se pueden especificar varias credenciales de este tipo, como rutas de archivo, alias clave o ambas. Consulte &quot;[Gestión de actualizaciones de certificados](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-cert-updates.md)&quot; en *Uso del SDK de acceso a Adobe para la protección de contenido* para obtener más información sobre cuándo se necesitan credenciales adicionales.
* **Credencial del servidor de licencias** : especifica una o varias credenciales del servidor de licencias (certificado y clave privada) emitidas por el Adobe. Se puede especificar como una ruta a un archivo .pfx y una contraseña, o como un alias para una credencial almacenada en un HSM. Aquí se pueden especificar varias credenciales de este tipo, como rutas de archivo, alias clave o ambas. Consulte Gestión de actualizaciones de certificados en *Uso del SDK de acceso a Adobe para la protección de contenido *para obtener más información sobre cuándo se necesitan credenciales adicionales.
* **Certificados clave del servidor** : opcional. Especifica el certificado de servidor de licencias del servidor de claves emitido por el Adobe. Se puede especificar como una ruta a un archivo .cer o un alias a un certificado almacenado en un HSM. Esta opción debe especificarse para poder emitir licencias para contenido empaquetado con una directiva que requiera la entrega de claves remotas para dispositivos iOS.
* **Autorizadores**  personalizados: opcional. Especifica las clases de autorizador personalizadas que se invocarán para cada solicitud de licencia. Si se especifican varios autorizadores, se invocan en el orden en que aparecen. Para obtener más información, consulte &quot;[Extensiones de autorización personalizadas](../../aaxs-protected-streaming/custom-authorization-extensions.md)&quot;.
* **Lista de paquetes autorizados** : opcional. Especifica certificados que identifican entidades autorizadas para empaquetar contenido para este servidor de licencias. Si no se especifica ningún certificado de empaquetador, el servidor emite licencias para contenido empaquetado por cualquier empaquetador.
* **Versión**  mínima del cliente admitida (consulte  *Uso del SDK de acceso al Adobe para la protección de contenido*).
* **Reglas de uso**

   * **Almacenamiento en caché de licencias** : opcional. Especifica cuánto tiempo se puede almacenar la licencia en el cliente. De forma predeterminada, el almacenamiento en caché de licencias está deshabilitado. Para habilitar el almacenamiento en caché de licencias durante un periodo de tiempo limitado, establezca la fecha de finalización o el número de segundos para los que se debe almacenar la licencia (comenzando cuando se emita la licencia). Si establece el número de segundos en 0, se deshabilita el almacenamiento en caché de licencias.

      Tenga en cuenta que todas las licencias otorgadas por el servidor para transmisión protegida tienen un periodo de caducidad de 24 horas (86 400 segundos). Por lo tanto, este valor se aplica implícitamente como límite superior a la fecha o duración de finalización que se establezca también para el almacenamiento en caché de licencias, con un valor máximo de 86400 segundos, aunque el esquema aplique límites superiores.

   * **Reproducir a la derecha** : se debe especificar al menos un derecho. Si se especifican varios derechos, el cliente utilizará el primer derecho para el que cumpla todos los requisitos.

      * **Protección de salida** : controla si se debe proteger la salida a dispositivos de renderización externos.
      * **Restricciones de aplicaciones AIR y SWF** : lista de permitidos opcional de aplicaciones SWF y AIR que pueden reproducir el contenido (es decir, solo se permiten las aplicaciones especificadas). Las aplicaciones SWF se identifican mediante una URL o el compendio del SWF y el tiempo máximo para permitir la descarga y verificación del compendio. Para obtener información sobre el cálculo del compendio SWF, consulte la sección &quot;Calculadora de hash SWF&quot;. Las aplicaciones de AIR e iOS se identifican mediante un ID de editor y un ID de aplicación opcional, una versión mínima y una versión máxima. Si no se especifican restricciones de aplicación, cualquier aplicación SWF o AIR puede reproducir el contenido.
      * **Restricciones de módulos DRM y Runtime** : especifica el nivel de seguridad mínimo necesario para el módulo DRM/Runtime. Opcionalmente, incluye una lista de bloqueados de versiones que no pueden reproducir el contenido. Las versiones de los módulos se identifican mediante atributos como el sistema operativo o un número de versión. Las restricciones de módulos DRM y las restricciones de módulos en tiempo de ejecución ahora admiten los siguientes atributos adicionales:

         * `oemVendor`
         * `model`
         * `screenType`

         Los siguientes atributos ahora son opcionales:

         * `osVersion`
         * `version`
      * **Requisitos de capacidad del dispositivo** : Opcionalmente, especifica las capacidades de hardware necesarias para acceder al contenido.
      * **Requisitos de detección de saltos de cárcel** : Opcionalmente, especifica que no se permite la reproducción en los dispositivos en los que se detecta una fuga de correo.



Consulte los comentarios en el archivo de configuración de inquilino de ejemplo para obtener más información.
