---
description: El archivo de configuración flashaccess-tenant.xml incluye opciones que se aplican a un inquilino específico del servidor de licencias.
seo-description: El archivo de configuración flashaccess-tenant.xml incluye opciones que se aplican a un inquilino específico del servidor de licencias.
seo-title: Archivo de configuración del inquilino
title: Archivo de configuración del inquilino
uuid: bc9ee4a1-63b6-4362-9929-3e9fe8251075
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---


# Archivo de configuración del inquilino{#tenant-configuration-file}

El archivo de configuración flashaccess-tenant.xml incluye opciones que se aplican a un inquilino específico del servidor de licencias.

Cada inquilino admite su propia instancia de este archivo de configuración que se encuentra en `<LicenseServer.ConfigRoot>/flashaccessserver/tenants/<tenantname>`. Consulte el `configs/flashaccessserver/tenants/sampletenant` directorio para ver un archivo de configuración de inquilino de ejemplo.

Puede especificar todas las rutas de archivo del archivo de configuración del inquilino como rutas absolutas o como rutas relativas al directorio de configuración del inquilino (`<LicenseServer.ConfigRoot>/flashaccessserver/tenants/<tenantname>`).

El archivo de configuración del inquilino incluye:

* *Credencial* de transporte — Especifica una o varias credenciales de transporte (certificado y clave privada) emitidas por Adobe. Se puede especificar como una ruta a un [!DNL .pfx] archivo y una contraseña, o como un alias para una credencial almacenada en un HSM. Aquí se pueden especificar varias credenciales de este tipo, ya sea como rutas de archivos, alias de claves o ambas.

   Consulte *Gestión de actualizaciones* de certificados en *Uso del SDK de DRM de Adobe Primetime para la protección de contenido* para obtener más información sobre cuándo se necesitan credenciales adicionales.

* *Credencial* del servidor de licencias — Especifica una o varias credenciales del servidor de licencias (certificado y clave privada) que Adobe ha emitido. Puede especificar las credenciales del servidor de licencias como una ruta a un [!DNL .pfx] archivo y una contraseña, o un alias para una credencial almacenada en un HSM. Aquí se pueden especificar varias credenciales de este tipo, ya sea como rutas de archivos, alias de claves o ambas.

   Consulte *Gestión de actualizaciones* de certificados en *Uso del SDK de DRM de Adobe Primetime para la protección de contenido* para obtener más información sobre cuándo se necesitan credenciales adicionales.

* *Certificados* de servidor clave — De forma opcional, especifica el certificado del servidor de licencias de Key Server que Adobe ha emitido. Puede especificar el certificado del servidor de licencias de Key Server como una ruta a un [!DNL .cer] archivo o un alias a un certificado almacenado en un HSM. Esta opción debe especificarse para emitir licencias para contenido empaquetado con una directiva DRM que requiera un envío de clave remota para dispositivos iOS.

* *Autorizadores* personalizados — De forma opcional, especifica las clases de autorizador personalizadas que se van a invocar para cada solicitud de licencia. Si se especifican varios autorizadores, se invocan en el orden en que aparecen.
* *Lista de envases* autorizados — De forma opcional, especifica certificados que identifican entidades autorizadas para empaquetar contenido para este servidor de licencias. Si no se especifica ningún certificado de empaquetador, el servidor emite licencias para contenido empaquetado por cualquier empaquetador. Si el servidor recibe una solicitud de licencia de un empaquetador no autorizado, se deniega la solicitud.
* *Versión* mínima del cliente admitida Consulte Uso del SDK de Adobe Primetime DRM para la protección de contenido.

* *Reglas de uso*

   * *Almacenamiento en caché* de licencias — De forma opcional, especifica cuánto tiempo puede almacenar la licencia en el cliente. De forma predeterminada, el almacenamiento en caché de licencias está desactivado. Si desea habilitar el almacenamiento en caché de licencias para un período de tiempo limitado, debe establecer la fecha de finalización o el número de segundos para los que se debe almacenar la licencia (comenzando cuando se emita la licencia). Si se establece el número de segundos en 0, se deshabilita la caché de licencias.

      >[!NOTE]
      >
      >Todas las licencias que ha emitido el servidor de flujo protegido incluyen un período de caducidad de 24 horas (86400 segundos). Este valor se aplica implícitamente como límite superior a la fecha o duración de finalización que se haya establecido para el almacenamiento en caché de licencias, con un valor máximo de 86400 segundos, aunque el esquema aplique límites superiores.

   * *Reproducir a la derecha* — Se debe especificar un mínimo de un derecho. Si especifica varios derechos, el cliente utilizará el primer derecho que cumpla todos los requisitos.

      * *Protección* de salida — Controla si se debe proteger la salida a dispositivos de procesamiento externos.
      * *Restricciones* de aplicaciones AIR y SWF — Lista de permitidos opcional de aplicaciones SWF y AIR que pueden reproducir el contenido (por ejemplo, solo se permiten las aplicaciones especificadas). Las aplicaciones SWF se identifican mediante una URL o mediante el compendio del SWF y el tiempo máximo para permitir la descarga y verificación del compendio.

         Consulte Calculadora de hash *SWF* para obtener información sobre cómo calcular el compendio SWF.

         Un ID de editor y un ID de aplicación opcional, una versión mínima y una versión máxima identifican las aplicaciones de AIR e iOS. Si no especifica ninguna restricción de aplicación, cualquier aplicación SWF o AIR puede reproducir el contenido.

      * *Restricciones* de módulos DRM y Runtime — Especifica el nivel de seguridad mínimo necesario para el módulo DRM/Runtime. Opcionalmente, incluye una lista de bloqueados de versiones que no pueden reproducir el contenido. Las versiones de módulos se identifican mediante atributos, como sistema operativo y/o número de versión.

         Las restricciones del módulo DRM y las restricciones del módulo de tiempo de ejecución ahora admiten los atributos adicionales siguientes:

         * `oemVendor`
         * `model`
         * `screenType`

         Los siguientes atributos ahora son opcionales:

         * `osVersion`
         * `version`
      * *Requisitos* de capacidad del dispositivo — De forma opcional, especifica las capacidades de hardware necesarias para acceder al contenido.
      * *Requisitos* de detección de saltos de cárcel — De forma opcional, especifica que no se permite la reproducción en dispositivos en los que se detecta un salto de página.



Consulte los comentarios en el archivo de configuración del inquilino de ejemplo para obtener más información.
