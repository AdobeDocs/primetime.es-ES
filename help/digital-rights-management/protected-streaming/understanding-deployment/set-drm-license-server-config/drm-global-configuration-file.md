---
description: El archivo de configuración flashaccess-global.xml incluye opciones que se aplican a todos los inquilinos del servidor de licencias.
title: Archivo de configuración global
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---


# Archivo de configuración global{#global-configuration-file}

El archivo de configuración flashaccess-global.xml incluye opciones que se aplican a todos los inquilinos del servidor de licencias.

Debe colocar el archivo de configuración en el directorio [!DNL LicenseServer.ConfigRoot].

Consulte el directorio [!DNL configs] para ver un ejemplo de un archivo de configuración global.

El archivo de configuración global incluye:

* Almacenamiento en caché: controla el almacenamiento en caché de los archivos de configuración en la memoria.

   Consulte *Actualización de archivos de configuración* para obtener información sobre la configuración de almacenamiento en caché.
* Registro: especifica el nivel de registro y la frecuencia con la que se rompen los archivos de registro.
* Contraseña de HSM: solo es necesaria si se utiliza un HSM para almacenar credenciales de servidor.

Consulte los comentarios en el archivo de configuración global de ejemplo que se encuentra en Primetime DRM `<DVD>`\Adobe Primetime DRM Server para transmisión protegida\configs para obtener más información.
