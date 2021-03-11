---
title: Archivo de configuración global
description: Archivo de configuración global
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# Archivo de configuración global{#global-configuration-file}

El archivo de configuración flashaccess-global.xml contiene opciones que se aplican a todos los inquilinos del servidor de licencias. Este archivo debe estar ubicado en *LicenseServer.ConfigRoot*. Consulte el directorio de configuraciones para ver un archivo de configuración global de ejemplo. El archivo de configuración global incluye lo siguiente:

* Almacenamiento en caché: controla el almacenamiento en caché de los archivos de configuración en la memoria. Para obtener una explicación de la configuración del almacenamiento en caché, consulte &quot;Actualización de archivos de configuración&quot;.
* Registro: especifica el nivel de registro y la frecuencia con la que se rompen los archivos de registro.
* Contraseña de HSM: solo es necesaria si se utiliza un HSM para almacenar credenciales de servidor.

Consulte los comentarios en el archivo de configuración global de ejemplo ubicado en `<AdobeAccessDVD>\Adobe Access Server for Protected Streaming\configs` para obtener más información.
