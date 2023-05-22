---
title: Archivo de configuración global
description: Archivo de configuración global
copied-description: true
exl-id: 5a2f96fe-d39d-4391-a010-200a900b043b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
