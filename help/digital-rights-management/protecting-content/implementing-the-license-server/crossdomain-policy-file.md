---
title: Archivo de directiva DRM entre dominios
description: Archivo de directiva DRM entre dominios
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# Archivo de directiva DRM entre dominios {#crossdomain-drm-policy-file}

Si el servidor de licencias está alojado en un dominio diferente al del SWF de reproducción de vídeo, cree un archivo de directiva DRM entre dominios ( [!DNL crossdomain.xml]) es necesario para permitir que el SWF solicite licencias de un servidor de licencias. Un archivo de directiva DRM entre dominios se representa mediante un archivo XML que permite al servidor indicar que sus datos y documentos están disponibles para archivos de SWF proporcionados por otros dominios. Cualquier archivo de SWF servido desde un dominio especificado en el archivo de directiva DRM entre dominios del servidor de licencias puede acceder a los datos o recursos de ese servidor de licencias.

El Adobe recomienda que los desarrolladores sigan las prácticas recomendadas al implementar el archivo de directivas entre dominios, ya que solo permite a los dominios de confianza acceder al servidor de licencias y limita el acceso al subdirectorio de licencias en el servidor web.

Para obtener más información sobre los archivos de política DRM entre dominios, consulte las siguientes ubicaciones:

* Controles de sitio Web (archivos de directiva DRM)
* Especificación del archivo de política DRM entre dominios: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

