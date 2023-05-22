---
title: Archivos de configuración del servidor de licencias
description: Archivos de configuración del servidor de licencias
copied-description: true
exl-id: d48e88a4-caae-4f4e-b870-38da4f3a715e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
