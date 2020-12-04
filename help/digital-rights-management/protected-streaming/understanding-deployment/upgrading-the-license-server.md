---
seo-title: Actualización del servidor DRM de Adobe Primetime para flujo protegido
title: Actualización del servidor DRM de Adobe Primetime para flujo protegido
uuid: 5c507ae3-d1d9-40ad-ba97-501ec92b45dc
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Actualización del servidor DRM de Adobe Primetime para flujo protegido{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

Si desea actualizar un servidor que ejecute Primetime DRM Server para flujo protegido, debe reemplazar el archivo `flashaccessserver.war` que se ha implementado en el servidor de aplicaciones por el archivo que se ha incluido con el último DRM de Primetime.

Si desea utilizar las nuevas opciones de configuración, debe actualizar el `flashaccess-tenant.xml` de su servidor. También debe actualizar [!DNL jsafe.dll] o [!DNL libjsafe.so] con la versión que se ha incluido con el último DRM de Primetime.
