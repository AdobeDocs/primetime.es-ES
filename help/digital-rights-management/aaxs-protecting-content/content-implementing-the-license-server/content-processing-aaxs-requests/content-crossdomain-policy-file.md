---
title: Archivo de directiva entre dominios
description: Archivo de directiva entre dominios
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# Archivo de directiva de dominio cruzado {#crossdomain-policy-file}

Si el servidor de licencias está alojado en un dominio diferente al SWF de reproducción de vídeo, es necesario un archivo de directivas entre dominios (cross-domain.xml) para permitir que el SWF solicite licencias del servidor de licencias. Un archivo de directiva entre dominios es un archivo XML que proporciona una forma de que el servidor indique que sus datos y documentos están disponibles para archivos SWF servidos desde otros dominios. Cualquier archivo SWF servido desde un dominio especificado en el archivo de directiva entre dominios del servidor de licencias puede acceder a datos o recursos desde ese servidor de licencias.

Adobe recomienda que los desarrolladores sigan las prácticas recomendadas al implementar el archivo de directivas entre dominios permitiendo que los dominios de confianza accedan al servidor de licencias y limitando el acceso al subdirectorio de licencias en el servidor web.

Para obtener más información sobre los archivos de directivas entre dominios, consulte las siguientes ubicaciones:

* Controles de sitio web (archivos de directiva)
* Especificación de archivos de directivas entre dominios: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

