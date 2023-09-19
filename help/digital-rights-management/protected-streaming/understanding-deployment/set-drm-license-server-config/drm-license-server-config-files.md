---
title: Archivos de configuración del servidor de licencias
description: Archivos de configuración del servidor de licencias
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# Archivos de configuración del servidor de licencias{#license-server-configuration-files}

Adobe Primetime DRM Server for Protected Streaming requiere los siguientes tipos de archivos de configuración:

* Archivo de configuración global ( [!DNL flashaccess-global.xml])
* Archivo de configuración de usuario para cada usuario ( [!DNL flashaccess-tenant.xml])

Una vez editados los archivos de configuración, Adobe recomienda utilizar las utilidades proporcionadas con el servidor DRM de Primetime para el flujo protegido para comprobar que los archivos están bien formados.

Consulte *Validador de configuración*.

Si desea evitar que las contraseñas estén disponibles en texto no cifrado en los archivos de configuración, debe cifrar todas las contraseñas especificadas en los archivos de configuración global e inquilino mediante la herramienta Scrambler proporcionada por el Adobe.

Consulte *Descodificador de contraseñas* para obtener más información sobre cómo cifrar contraseñas.
