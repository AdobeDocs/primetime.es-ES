---
title: Actualización del servidor DRM de Adobe Primetime para flujo protegido
description: Actualización del servidor DRM de Adobe Primetime para flujo protegido
copied-description: true
exl-id: 6edfba1b-46a2-4cbd-bc14-feeef1a36ed6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Actualización del servidor DRM de Adobe Primetime para flujo protegido{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

Si desea actualizar un servidor que ejecute el servidor DRM de Primetime para flujo protegido, debe reemplazar el `flashaccessserver.war` que se ha implementado en el servidor de aplicaciones con el archivo que se ha incluido con el DRM de Primetime más reciente.

Si desea utilizar las nuevas opciones de configuración, debe actualizar el `flashaccess-tenant.xml`. También debe actualizar [!DNL jsafe.dll] o [!DNL libjsafe.so] con la versión que se ha incluido con la última DRM de Primetime.
