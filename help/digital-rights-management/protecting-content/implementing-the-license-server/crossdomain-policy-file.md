---
seo-title: Archivo de política DRM de dominio cruzado
title: Archivo de política DRM de dominio cruzado
uuid: cb91a85a-1825-4fd7-a25c-880cdbd5c8b8
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Archivo de política DRM de dominio cruzado {#crossdomain-drm-policy-file}

Si el servidor de licencias está alojado en un dominio distinto del SWF de reproducción de vídeo, se necesita un archivo de política DRM entre dominios ( [!DNL crossdomain.xml]) para permitir que el SWF solicite licencias desde un servidor de licencias. Un archivo de política DRM entre dominios está representado por un archivo XML que permite al servidor indicar que sus datos y documentos están disponibles para los archivos SWF que se ofrecen desde otros dominios. Cualquier archivo SWF servido desde un dominio especificado en el archivo de política DRM entre dominios del servidor de licencias puede acceder a los datos o recursos de dicho servidor de licencias.

Adobe recomienda que los desarrolladores sigan las prácticas recomendadas al implementar el archivo de política entre dominios, permitiendo únicamente que los dominios de confianza tengan acceso al servidor de licencias y limitando el acceso al subdirectorio de licencias en el servidor web.

Para obtener más información sobre los archivos de política DRM entre dominios, consulte las siguientes ubicaciones:

* Controles del sitio web (archivos de política DRM)
* Especificación de archivo de directiva DRM entre dominios: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

