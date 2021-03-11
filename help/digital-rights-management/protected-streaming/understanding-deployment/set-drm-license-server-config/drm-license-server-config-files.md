---
title: Archivos de configuración del servidor de licencias
description: Archivos de configuración del servidor de licencias
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Archivos de configuración del servidor de licencias{#license-server-configuration-files}

El servidor Adobe Primetime DRM para transmisión protegida requiere los siguientes tipos de archivos de configuración:

* Archivo de configuración global ( [!DNL flashaccess-global.xml])
* Archivo de configuración del inquilino para cada inquilino ( [!DNL flashaccess-tenant.xml])

Después de completar la edición de los archivos de configuración, Adobe recomienda que utilice las utilidades proporcionadas con el Servidor DRM de Primetime para la transmisión protegida para comprobar que los archivos están bien formados.

Consulte *Validador de configuración*.

Si desea evitar que las contraseñas estén disponibles en texto sin formato en los archivos de configuración, debe cifrar todas las contraseñas especificadas en los archivos de configuración global e inquilino utilizando la herramienta Scrambler que Adobe ha proporcionado.

Consulte *Contraseña Scrambler* para obtener más información sobre cómo cifrar contraseñas.
