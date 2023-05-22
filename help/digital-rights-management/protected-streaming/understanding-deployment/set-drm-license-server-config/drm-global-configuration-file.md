---
description: El archivo de configuración flashaccess-global.xml incluye opciones que se aplican a todos los inquilinos del servidor de licencias.
title: Archivo de configuración global
exl-id: 3e74bce6-1634-469f-9d02-1121e9d50687
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
