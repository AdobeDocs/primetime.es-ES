---
description: El archivo de configuración flashaccess-tenant.xml incluye opciones que se aplican a un inquilino específico del servidor de licencias.
title: Archivo de configuración de inquilino
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---

# Archivo de configuración de inquilino{#tenant-configuration-file}

El archivo de configuración flashaccess-tenant.xml incluye opciones que se aplican a un inquilino específico del servidor de licencias.

Cada inquilino admite su propia instancia de este archivo de configuración que se encuentra en `<LicenseServer.ConfigRoot>/flashaccessserver/tenants/<tenantname>`. Consulte la `configs/flashaccessserver/tenants/sampletenant` para un archivo de configuración de inquilino de ejemplo.

Puede especificar todas las rutas de archivo en el archivo de configuración del inquilino como rutas absolutas o como rutas relativas al directorio de configuración del inquilino (`<LicenseServer.ConfigRoot>/flashaccessserver/tenants/<tenantname>`).

El archivo de configuración de inquilino incluye:

* *Credencial de transporte* — especifica una o varias credenciales de transporte (certificado y clave privada) emitidas por el Adobe. Se puede especificar como ruta a un [!DNL .pfx] y una contraseña, o un alias para una credencial almacenada en un HSM. Aquí se pueden especificar varias credenciales de este tipo, como rutas de archivo, alias de clave o ambos.

  Consulte *Administrar actualizaciones de certificados* in *Uso del SDK de DRM de Adobe Primetime para proteger el contenido* para obtener más información sobre cuándo se necesitan credenciales adicionales.

* *Credenciales del servidor de licencias* — especifica una o varias credenciales del servidor de licencias (certificado y clave privada) que ha emitido el Adobe. Puede especificar las credenciales del servidor de licencias como una ruta a un [!DNL .pfx] y una contraseña, o un alias para una credencial almacenada en un HSM. Aquí se pueden especificar varias credenciales de este tipo, como rutas de archivo, alias de clave o ambos.

  Consulte *Administrar actualizaciones de certificados* in *Uso del SDK de DRM de Adobe Primetime para proteger el contenido* para obtener más información sobre cuándo se necesitan credenciales adicionales.

* *Certificados de servidor clave* — especifica opcionalmente el certificado de servidor de licencias del servidor de claves que ha emitido el Adobe. Puede especificar el certificado del servidor de licencias del servidor de claves como ruta de acceso a una [!DNL .cer] o un alias a un certificado almacenado en un HSM. Se debe especificar esta opción para emitir licencias para contenido que esté empaquetado con una directiva DRM que requiera la entrega de claves remotas para dispositivos iOS.

* *Autorizadores personalizados* — especifica opcionalmente clases de autorizador personalizadas para invocar para cada solicitud de licencia. Si se especifican varios autorizadores, se invocan en el orden indicado.
* *Lista de empaquetadores autorizados* — especifica opcionalmente certificados que identifican entidades autorizadas para empaquetar contenido para este servidor de licencias. Si no se especifican certificados de empaquetador, el servidor emite licencias para el contenido empaquetado por cualquier empaquetador. Si el servidor recibe una solicitud de licencia de un empaquetador no autorizado, se denegará la solicitud.
* *Versión de cliente mínima admitida* Consulte Uso del SDK de Adobe Primetime DRM para proteger contenido.

* *Reglas de uso*

   * *Almacenamiento en caché de licencias* — Opcionalmente especifica cuánto tiempo se puede almacenar la licencia en el cliente. De forma predeterminada, el almacenamiento en caché de licencias está deshabilitado. Si desea habilitar el almacenamiento en caché de licencias durante un período de tiempo limitado, debe establecer la fecha de finalización o el número de segundos durante los cuales se debe almacenar la licencia (a partir del momento en que se emite la licencia). Si establece el número de segundos en 0, se deshabilita el almacenamiento de licencias en caché.

     >[!NOTE]
     >
     >Todas las licencias que ha emitido el servidor para transmisión protegida incluyen un período de caducidad de 24 horas (86400 segundos). Este valor se aplica implícitamente como un límite superior a la fecha de finalización o duración establecida para el almacenamiento en caché de licencias, con un valor máximo de 86400 segundos, aunque el esquema aplique límites más altos.

   * *Reproducir a la derecha* — Debe especificarse un mínimo de un derecho. Si especifica varios derechos, el cliente utilizará el primero que cumpla todos los requisitos.

      * *Protección de salida* — controla si la salida a dispositivos de renderización externos debe protegerse.
      * *Restricciones de aplicaciones de AIR y SWF* — lista de permitidos opcional de las aplicaciones de SWF y AIR que pueden reproducir el contenido (por ejemplo, solo se permiten las aplicaciones especificadas). Las aplicaciones de SWF se identifican mediante una dirección URL o por el resumen del SWF y el tiempo máximo para permitir la descarga y verificación del compendio.

        Consulte *Calculadora de hash de SWF* para obtener información sobre cómo calcular el compendio de SWF.

        Un ID de editor e ID de aplicación opcional, una versión mínima y una versión máxima identifican las aplicaciones de AIR y iOS. Si no especifica restricciones de aplicación, cualquier SWF o aplicación de AIR puede reproducir el contenido.

      * *Restricciones del módulo DRM y Runtime* — especifica el nivel de seguridad mínimo requerido para el módulo DRM/Runtime. Opcionalmente incluye una lista de bloqueados de versiones a las que no se les permite reproducir el contenido. Las versiones de los módulos se identifican mediante atributos como, por ejemplo, un sistema operativo o un número de versión.

        Las restricciones del módulo DRM y las restricciones del módulo Runtime ahora admiten los siguientes atributos adicionales:

         * `oemVendor`
         * `model`
         * `screenType`

        Los siguientes atributos ahora son opcionales:

         * `osVersion`
         * `version`

      * *Requisitos de capacidad del dispositivo* — especifica opcionalmente las capacidades de hardware necesarias para acceder al contenido.
      * *Requisitos de detección de jailbreak* — especifica de forma opcional que no se permite la reproducción en los dispositivos en los que se detecta una fuga.

Consulte los comentarios en el archivo de configuración del inquilino de ejemplo para obtener más información.
