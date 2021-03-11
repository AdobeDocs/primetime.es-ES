---
description: Multi CDN permite configurar una o más ubicaciones de CDN para que proporcionen anuncios transcodificados.
title: Compatibilidad con varias CDN
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Compatibilidad con Multi CDN {#multi-cdn-support}

Multi CDN permite configurar una o más ubicaciones de CDN para que proporcionen anuncios transcodificados.

De forma predeterminada, todos los recursos transcodificados están alojados en la CDN de Akamai, propiedad de la Adobe. Sin embargo, puede elegir cero o más ubicaciones de CDN adicionales propias donde CRS alojará el recurso transcodificado. Por lo tanto, en este caso, los recursos transcodificados y el contenido se pueden servir desde la misma CDN.

Cuando el servidor de manifiestos realiza una búsqueda de solicitudes transcodificadas, utiliza una URL de arranque que contiene varios parámetros de consulta. Si ha configurado un entorno de varias CDN, la URL de arranque también tendrá que contener el parámetro `ptcdn`. El servidor de manifiesto utiliza este parámetro para identificar el servidor de CDN desde el que obtener la versión transcodificada del anuncio.

La compatibilidad con varias CDN también está disponible para las siguientes soluciones de Primetime:

1. TVSDK para Android
1. TVSDK para Desktop HLS
1. TVSDK para iOS

## Habilitar compatibilidad con CDN {#section_1BA344F2300B49F291865A7461EDFEAE}

De forma predeterminada, CRS está deshabilitado para todos los clientes

Póngase en contacto con el administrador técnico de cuentas de Adobe para configurar su cuenta de CRS para que utilice otras CDN para alojar los activos de anuncios transcodificados. Deberá proporcionar la siguiente información que CRS necesita para cargar los activos de anuncios transcodificados en la CDN

1. URL de CDN
1. Detalles de autenticación
1. Formato de URL de salida

Además, el administrador técnico de cuentas de Adobe le proporcionará un apodo para esta CDN. Debe pasar esto como el valor del parámetro `ptcdn` en la dirección URL del Bootstrap.

Puede tener varias CDN configuradas en el final de CRS mediante la compatibilidad con Adobe. Sin embargo, la CDN que se utiliza para elegir los recursos de publicidad que se van a vincular mediante el servidor de manifiestos tendría que ser la que se pasa como valor del parámetro `ptcdn` en la dirección URL del Bootstrap.
