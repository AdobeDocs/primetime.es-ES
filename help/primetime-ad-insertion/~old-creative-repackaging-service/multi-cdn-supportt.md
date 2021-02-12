---
description: Multi CDN permite configurar una o varias ubicaciones de CDN para ofrecer anuncios transcodificados.
seo-description: Multi CDN permite configurar una o varias ubicaciones de CDN para ofrecer anuncios transcodificados.
seo-title: Compatibilidad con varios CDN
title: Compatibilidad con varios CDN
uuid: 2b6d71f0-61c8-486b-a35a-f7ef3a9519d2
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# Compatibilidad con múltiples CDN {#multi-cdn-support}

Multi CDN permite configurar una o varias ubicaciones de CDN para ofrecer anuncios transcodificados.

De forma predeterminada, todos los recursos transcodificados están alojados en la CDN de Akamai, propiedad del Adobe. Sin embargo, puede elegir cero o más ubicaciones CDN adicionales propias donde CRS alojará el recurso transcodificado. En este caso, los recursos y el contenido transcodificados se pueden proporcionar desde la misma CDN.

Cuando el servidor de manifiesto realiza una búsqueda de solicitudes transcodificadas, utiliza una URL de arranque que contiene varios parámetros de consulta. Si ha configurado un entorno multi-CDN, la dirección URL de arranque también deberá contener el parámetro `ptcdn`. El servidor de manifiesto utiliza este parámetro para identificar el servidor CDN desde el cual obtener la versión transcodificada de la publicidad.

La compatibilidad con Múltiples CDN también está disponible para las siguientes soluciones Primetime:

1. TVSDK para Android
1. TVSDK para HLS de escritorio
1. TVSDK para iOS

## Habilitar compatibilidad con CDN {#section_1BA344F2300B49F291865A7461EDFEAE}

De forma predeterminada, CRS está deshabilitado para todos los clientes

Póngase en contacto con el administrador técnico de cuentas de Adobe para configurar su cuenta de CRS y utilizar otras CDN para alojar los recursos de publicidad transcodificados.Deberá proporcionar la siguiente información que CRS necesite para cargar los recursos de publicidad transcodificados en la CDN

1. URL de CDN
1. Detalles de autenticación
1. Formato de URL de salida

Además, el administrador técnico de cuentas de Adobe le proporcionará un sobrenombre para esta CDN. Debe pasarlo como el valor del parámetro `ptcdn` en la dirección URL del Bootstrap.

Puede tener varias CDN configuradas en el extremo de CRS mediante la compatibilidad con Adobe. Sin embargo, la CDN que se utiliza para elegir los recursos de publicidad que se van a vincular a través del servidor de manifiesto debe ser la que se pasa como el valor del parámetro `ptcdn` en la dirección URL del Bootstrap.
