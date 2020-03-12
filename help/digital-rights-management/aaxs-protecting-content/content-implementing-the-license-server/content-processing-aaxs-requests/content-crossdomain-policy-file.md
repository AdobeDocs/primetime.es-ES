---
seo-title: Archivo de directiva de dominio cruzado
title: Archivo de directiva de dominio cruzado
uuid: fc05aa5e-6fbd-445f-a22a-f795d5a0b3ad
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Archivo de directiva de dominio cruzado {#crossdomain-policy-file}

Si el servidor de licencias está alojado en un dominio distinto del SWF de reproducción de vídeo, se necesita un archivo de política entre dominios (cross-domain.xml) para permitir que el SWF solicite licencias al servidor de licencias. Un archivo de política entre dominios es un archivo XML que proporciona al servidor una forma de indicar que sus datos y documentos están disponibles para archivos SWF que se ofrecen desde otros dominios. Cualquier archivo SWF servido desde un dominio especificado en el archivo de política entre dominios del servidor de licencias puede acceder a los datos o recursos de dicho servidor de licencias.

Adobe recomienda que los desarrolladores sigan las prácticas recomendadas al implementar el archivo de política entre dominios, permitiendo únicamente que los dominios de confianza tengan acceso al servidor de licencias y limitando el acceso al subdirectorio de licencias en el servidor web.

Para obtener más información sobre los archivos de política entre dominios, consulte las siguientes ubicaciones:

* Controles del sitio Web (archivos de política)
* Especificación de archivo de directiva entre dominios: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

