---
description: El archivo de configuración flashaccess-tenant.xml incluye opciones que se aplican a un inquilino específico del servidor de licencias.
title: Archivo de configuración del inquilino
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---


# Archivo de configuración del inquilino{#tenant-configuration-file}

El archivo de configuración flashaccess-tenant.xml incluye opciones que se aplican a un inquilino específico del servidor de licencias.

Cada inquilino admite su propia instancia de este archivo de configuración que se encuentra en `<LicenseServer.ConfigRoot>/flashaccessserver/tenants/<tenantname>`. Consulte el directorio `configs/flashaccessserver/tenants/sampletenant` para ver un archivo de configuración de inquilino de ejemplo.

Puede especificar todas las rutas del archivo en el archivo de configuración del inquilino como rutas absolutas o como rutas relativas al directorio de configuración del inquilino (`<LicenseServer.ConfigRoot>/flashaccessserver/tenants/<tenantname>`).

El archivo de configuración del inquilino incluye:

* *Credencial de transporte* : especifica una o más credenciales de transporte (certificado y clave privada) emitidas por el Adobe. Se puede especificar como una ruta a un archivo [!DNL .pfx] y una contraseña, o un alias para una credencial almacenada en un HSM. Aquí se pueden especificar varias credenciales de este tipo, como rutas de archivo, alias clave o ambas.

   Consulte *Gestión de actualizaciones de certificados* en *Uso del SDK de Adobe Primetime DRM para la protección de contenido* para obtener más información sobre cuándo se necesitan credenciales adicionales.

* *Credencial del servidor de licencias* : especifica una o varias credenciales del servidor de licencias (certificado y clave privada) que el Adobe ha emitido. Puede especificar las credenciales del servidor de licencias como una ruta a un archivo [!DNL .pfx] y una contraseña, o un alias para una credencial almacenada en un HSM. Aquí se pueden especificar varias credenciales de este tipo, como rutas de archivo, alias clave o ambas.

   Consulte *Gestión de actualizaciones de certificados* en *Uso del SDK de Adobe Primetime DRM para la protección de contenido* para obtener más información sobre cuándo se necesitan credenciales adicionales.

* *Certificados clave del servidor* : Opcionalmente, especifica el certificado del servidor de licencias del servidor de claves que ha emitido el Adobe. Puede especificar el certificado del servidor de licencias de Key Server como una ruta a un archivo [!DNL .cer] o un alias a un certificado almacenado en un HSM. Esta opción debe especificarse para emitir licencias para contenido empaquetado con una directiva DRM que requiera la entrega de claves remotas para dispositivos iOS.

* *Autorizadores personalizados* : Opcionalmente, especifica las clases de autorizador personalizadas que se invocarán para cada solicitud de licencia. Si se especifican varios autorizadores, se invocan en el orden en que aparecen.
* *Lista de paquetes autorizados* : Opcionalmente, especifica certificados que identifican entidades autorizadas para empaquetar contenido para este servidor de licencias. Si no se especifica ningún certificado de empaquetador, el servidor emite licencias para contenido empaquetado por cualquier empaquetador. Si el servidor recibe una solicitud de licencia de un empaquetador no autorizado, se deniega la solicitud.
* *Versión mínima del cliente* admitidaConsulte Uso del SDK de Adobe Primetime DRM para la protección de contenido.

* *Reglas de uso*

   * *Almacenamiento en caché de licencias* : Opcionalmente, especifica cuánto tiempo puede almacenar la licencia en el cliente. De forma predeterminada, el almacenamiento en caché de licencias está deshabilitado. Si desea habilitar el almacenamiento en caché de licencias durante un periodo de tiempo limitado, debe establecer la fecha de finalización o el número de segundos para los que se debe almacenar la licencia (comenzando cuando se emite la licencia). Si establece el número de segundos en 0, se deshabilita el almacenamiento en caché de licencias.

      >[!NOTE]
      >
      >Todas las licencias que ha emitido el Servidor para transmisión protegida incluyen un periodo de caducidad de 24 horas (86 400 segundos). Este valor se aplica implícitamente como límite superior a la fecha o duración de finalización que se establezca también para el almacenamiento en caché de licencias, con un valor máximo de 86 400 segundos, aunque el esquema aplique límites superiores.

   * *Reproducir a la derecha* : se debe especificar un mínimo de un derecho. Si especifica varios derechos, el cliente utilizará el primer derecho que cumpla todos los requisitos.

      * *Protección de salida* : controla si se debe proteger la salida a dispositivos de renderización externos.
      * *Restricciones de aplicaciones AIR y SWF* : lista de permitidos opcional de aplicaciones SWF y AIR que pueden reproducir el contenido (por ejemplo, solo se permiten las aplicaciones especificadas). Las aplicaciones SWF se identifican mediante una URL o el compendio del SWF y el tiempo máximo para permitir la descarga y verificación del compendio.

         Consulte *Calculadora de hash SWF* para obtener información sobre cómo calcular el compendio SWF.

         El ID de editor y el ID de aplicación opcional, la versión mínima y la versión máxima identifican las aplicaciones de AIR e iOS. Si no especifica restricciones de aplicación, cualquier aplicación SWF o AIR puede reproducir el contenido.

      * *Restricciones de módulos DRM y Runtime* : especifica el nivel de seguridad mínimo necesario para el módulo DRM/Runtime. Opcionalmente, incluye una lista de bloqueados de versiones que no pueden reproducir el contenido. Las versiones del módulo se identifican mediante atributos como el sistema operativo o un número de versión.

         Las restricciones de módulos DRM y las restricciones de módulos en tiempo de ejecución ahora admiten los siguientes atributos adicionales:

         * `oemVendor`
         * `model`
         * `screenType`

         Los siguientes atributos ahora son opcionales:

         * `osVersion`
         * `version`
      * *Requisitos de capacidad del dispositivo* : Opcionalmente, especifica las capacidades de hardware necesarias para acceder al contenido.
      * *Requisitos de detección de saltos de cárcel* : Opcionalmente, especifica que no se permite la reproducción en los dispositivos en los que se detecta una fuga de correo.



Consulte los comentarios en el archivo de configuración de inquilino de ejemplo para obtener más información.
