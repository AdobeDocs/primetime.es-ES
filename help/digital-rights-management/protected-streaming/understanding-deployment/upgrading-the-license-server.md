---
title: Actualización del servidor Adobe Primetime DRM para la transmisión protegida
description: Actualización del servidor Adobe Primetime DRM para la transmisión protegida
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Actualización del servidor Adobe Primetime DRM para la transmisión protegida{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

Si desea actualizar un servidor que ejecute el servidor de Primetime DRM para la transmisión protegida, debe reemplazar el archivo `flashaccessserver.war` que se ha implementado en su servidor de aplicaciones por el archivo que se ha incluido con el último DRM de Primetime.

Si desea utilizar las nuevas opciones de configuración, debe actualizar el `flashaccess-tenant.xml` del servidor. También debe actualizar [!DNL jsafe.dll] o [!DNL libjsafe.so] con la versión que se ha incluido con el último DRM de Primetime.
