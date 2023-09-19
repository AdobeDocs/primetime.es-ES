---
title: Actualización del servidor DRM de Adobe Primetime para flujo protegido
description: Actualización del servidor DRM de Adobe Primetime para flujo protegido
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Actualización del servidor DRM de Adobe Primetime para flujo protegido{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

Si desea actualizar un servidor que ejecute el servidor DRM de Primetime para flujo protegido, debe reemplazar el `flashaccessserver.war` que se ha implementado en el servidor de aplicaciones con el archivo que se ha incluido con el DRM de Primetime más reciente.

Si desea utilizar las nuevas opciones de configuración, debe actualizar el `flashaccess-tenant.xml`. También debe actualizar [!DNL jsafe.dll] o [!DNL libjsafe.so] con la versión que se ha incluido con la última DRM de Primetime.
