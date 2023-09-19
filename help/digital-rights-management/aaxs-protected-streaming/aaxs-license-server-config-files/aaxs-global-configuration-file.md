---
title: Archivo de configuración global
description: Archivo de configuración global
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Archivo de configuración global{#global-configuration-file}

El archivo de configuración flashaccess-global.xml contiene opciones que se aplican a todos los inquilinos del servidor de licencias. Este archivo debe encontrarse en *LicenseServer.ConfigRoot*. Consulte el directorio de configuraciones para ver un ejemplo de archivo de configuración global. El archivo de configuración global incluye lo siguiente:

* Almacenamiento en caché: controla el almacenamiento en caché de los archivos de configuración en la memoria. Para obtener una explicación de la configuración de almacenamiento en caché, consulte &quot;Actualización de archivos de configuración&quot;.
* Registro: especifica el nivel de registro y la frecuencia con la que se acumulan los archivos de registro.
* Contraseña de HSM: sólo es necesaria si se utiliza un HSM para almacenar las credenciales del servidor.

Consulte los comentarios del archivo de configuración global de ejemplo ubicado en `<AdobeAccessDVD>\Adobe Access Server for Protected Streaming\configs` para obtener más información.
