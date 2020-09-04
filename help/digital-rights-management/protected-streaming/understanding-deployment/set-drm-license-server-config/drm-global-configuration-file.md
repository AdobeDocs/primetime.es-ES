---
description: El archivo de configuración flashaccess-global.xml incluye opciones que se aplican a todos los inquilinos del servidor de licencias.
seo-description: El archivo de configuración flashaccess-global.xml incluye opciones que se aplican a todos los inquilinos del servidor de licencias.
seo-title: Archivo de configuración global
title: Archivo de configuración global
uuid: 294d6cff-be07-4b4b-8aa6-943044a1c56f
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# Archivo de configuración global{#global-configuration-file}

El archivo de configuración flashaccess-global.xml incluye opciones que se aplican a todos los inquilinos del servidor de licencias.

Debe colocar el archivo de configuración en el [!DNL LicenseServer.ConfigRoot] directorio.

Consulte el [!DNL configs] directorio para ver un ejemplo de un archivo de configuración global.

El archivo de configuración global incluye:

* Almacenamiento en caché — Controla el almacenamiento en caché de los archivos de configuración en la memoria.

   Consulte *Actualización de archivos* de configuración para obtener información sobre la configuración de almacenamiento en caché.
* Registro — Especifica el nivel de registro y la frecuencia con la que se desplazan los archivos de registro.
* Contraseña de HSM — Solo es necesario si se utiliza un HSM para almacenar las credenciales del servidor.

Consulte los comentarios del archivo de configuración global de ejemplo que se encuentra en Primetime DRM `<DVD>`\Adobe Primetime DRM Server for Protected Streaming\configs para obtener más información.
