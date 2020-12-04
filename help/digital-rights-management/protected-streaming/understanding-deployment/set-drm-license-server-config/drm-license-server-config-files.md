---
seo-title: Archivos de configuración del servidor de licencias
title: Archivos de configuración del servidor de licencias
uuid: 7c7e0f76-2ced-45af-9542-99e06ec31cda
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Archivos de configuración del servidor de licencias{#license-server-configuration-files}

Adobe Primetime DRM Server for Protected Streaming requiere los siguientes tipos de archivos de configuración:

* Archivo de configuración global ( [!DNL flashaccess-global.xml])
* Archivo de configuración del inquilino para cada inquilino ( [!DNL flashaccess-tenant.xml])

Una vez que haya terminado de editar los archivos de configuración, Adobe recomienda que utilice las utilidades proporcionadas con Primetime DRM Server for Protected Streaming para comprobar que los archivos están bien formados.

Consulte *Validador de configuración*.

Si desea evitar que las contraseñas estén disponibles en texto sin formato en los archivos de configuración, debe cifrar todas las contraseñas especificadas en los archivos de configuración global e inquilino mediante la herramienta Scrambler proporcionada por Adobe.

Consulte *Password Scrambler* para obtener más información sobre cómo cifrar contraseñas.
