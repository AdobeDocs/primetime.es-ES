---
title: Archivo de directiva DRM de dominio cruzado
description: Archivo de directiva DRM de dominio cruzado
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# Archivo de directiva DRM de dominio cruzado {#crossdomain-drm-policy-file}

Si el servidor de licencias está alojado en un dominio diferente al SWF de reproducción de vídeo, se necesita un archivo de directiva DRM entre dominios ( [!DNL crossdomain.xml]) para permitir que el SWF solicite licencias a un servidor de licencias. Un archivo de directiva DRM entre dominios está representado por un archivo XML que permite al servidor indicar que sus datos y documentos están disponibles para archivos SWF servidos desde otros dominios. Cualquier archivo SWF servido desde un dominio especificado en el archivo de directiva DRM entre dominios del servidor de licencias puede acceder a los datos o recursos desde ese servidor de licencias.

Adobe recomienda que los desarrolladores sigan las prácticas recomendadas al implementar el archivo de directivas entre dominios permitiendo que los dominios de confianza accedan al servidor de licencias y limitando el acceso al subdirectorio de licencias en el servidor web.

Para obtener más información sobre los archivos de directiva DRM entre dominios, consulte las siguientes ubicaciones:

* Controles de sitios web (archivos de directivas DRM)
* Especificación de archivo de directiva DRM entre dominios: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

