---
description: Varias CDN permiten configurar una o más ubicaciones de CDN para que publiquen anuncios transcodificados.
title: Compatibilidad con varias CDN
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Compatibilidad con varias CDN {#multi-cdn-support}

Varias CDN permiten configurar una o más ubicaciones de CDN para que publiquen anuncios transcodificados.

De forma predeterminada, todos los recursos transcodificados están alojados en la CDN de Akamai de propiedad del Adobe. Sin embargo, puede elegir cero o más ubicaciones de CDN adicionales propias donde CRS alojará el recurso transcodificado. Por lo tanto, en este caso, sus recursos transcodificados y contenido se pueden servir desde la misma CDN.

Cuando el servidor de manifiesto realiza una búsqueda de solicitudes transcodificadas, utiliza una dirección URL de arranque que contiene varios parámetros de consulta. Si ha configurado un entorno de varias CDN, la URL de arranque también deberá contener la variable `ptcdn` parameter.The manifest server utiliza este parámetro para identificar el servidor CDN desde el que se obtiene la versión transcodificada del anuncio.

También hay compatibilidad con varias CDN para las siguientes soluciones de Primetime:

1. TVSDK para Android
1. TVSDK para HLS de escritorio
1. TVSDK para iOS

## Habilitar compatibilidad con CDN {#section_1BA344F2300B49F291865A7461EDFEAE}

De forma predeterminada, CRS está deshabilitado para todos los clientes

Póngase en contacto con el administrador técnico de cuentas de Adobe para configurar su cuenta de CRS de modo que utilice otras CDN para alojar los recursos de publicidad transcodificados. Deberá proporcionar la siguiente información que CRS necesita para cargar los recursos de publicidad transcodificados en la CDN

1. URL de CDN
1. Detalles de autenticación
1. Formato de URL de salida

Además, el administrador técnico de cuentas de Adobe le proporcionará un apodo para esta CDN. Debe pasarlo como el valor de `ptcdn` en la URL del Bootstrap.

Puede tener varias CDN configuradas en un extremo CRS mediante la compatibilidad con Adobes. Sin embargo, la CDN que se utiliza para seleccionar recursos de publicidad para vincularlos mediante el servidor de manifiesto tendría que ser la que se pasara como valor de `ptcdn` en la URL del Bootstrap.
