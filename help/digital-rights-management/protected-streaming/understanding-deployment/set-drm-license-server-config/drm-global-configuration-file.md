---
description: El archivo de configuración flashaccess-global.xml incluye opciones que se aplican a todos los inquilinos del servidor de licencias.
title: Archivo de configuración global
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# Archivo de configuración global{#global-configuration-file}

El archivo de configuración flashaccess-global.xml incluye opciones que se aplican a todos los inquilinos del servidor de licencias.

Debe colocar el archivo de configuración en [!DNL LicenseServer.ConfigRoot] directorio.

Consulte la [!DNL configs] para ver un ejemplo de un archivo de configuración global.

El archivo de configuración global incluye:

* Almacenamiento en caché: controla el almacenamiento en caché de los archivos de configuración en la memoria.

  Consulte *Actualización de archivos de configuración* para obtener información sobre la configuración de almacenamiento en caché.
* Registro: especifica el nivel de registro y la frecuencia con la que se acumulan los archivos de registro.
* Contraseña de HSM: sólo es necesaria si se utiliza un HSM para almacenar las credenciales del servidor.

Consulte los comentarios en el archivo de configuración global de ejemplo que se encuentra en Primetime DRM `<DVD>`\Servidor DRM de Adobe Primetime para transmisión protegida\configs para obtener más información.
