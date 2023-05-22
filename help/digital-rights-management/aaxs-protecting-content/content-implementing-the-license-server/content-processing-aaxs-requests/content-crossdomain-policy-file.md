---
title: Archivo de directiva entre dominios
description: Archivo de directiva entre dominios
copied-description: true
exl-id: dbe16692-cdf7-4a91-9303-8afc2d487112
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Archivo de directiva entre dominios {#crossdomain-policy-file}

Si el servidor de licencias está alojado en un dominio diferente al del SWF de reproducción de vídeo, es necesario un archivo de política entre dominios (cross-domain.xml) para permitir que el SWF solicite licencias del servidor de licencias. Un archivo de directiva entre dominios es un archivo XML que proporciona una forma para que el servidor indique que sus datos y documentos están disponibles para los archivos de SWF proporcionados por otros dominios. Cualquier archivo de SWF servido desde un dominio especificado en el archivo de directiva entre dominios del servidor de licencias puede acceder a los datos o recursos de ese servidor de licencias.

El Adobe recomienda que los desarrolladores sigan las prácticas recomendadas al implementar el archivo de directivas entre dominios, ya que solo permite a los dominios de confianza acceder al servidor de licencias y limita el acceso al subdirectorio de licencias en el servidor web.

Para obtener más información sobre los archivos de directivas entre dominios, consulte las siguientes ubicaciones:

* Controles de sitios Web (archivos de directivas)
* Especificación de archivo de política entre dominios: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)
