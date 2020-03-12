---
seo-title: Actualización del servidor Adobe Primetime DRM para flujo protegido
title: Actualización del servidor Adobe Primetime DRM para flujo protegido
uuid: 5c507ae3-d1d9-40ad-ba97-501ec92b45dc
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Actualización del servidor Adobe Primetime DRM para flujo protegido{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

Si desea actualizar un servidor que ejecute Primetime DRM Server para flujo protegido, debe reemplazar el `flashaccessserver.war` archivo que se ha implementado en el servidor de aplicaciones por el archivo que se ha incluido con la última DRM de Primetime.

Si desea utilizar las nuevas opciones de configuración, debe actualizar la del servidor `flashaccess-tenant.xml`. También debe actualizar [!DNL jsafe.dll] o [!DNL libjsafe.so] utilizar la versión incluida con el último DRM de Primetime.
