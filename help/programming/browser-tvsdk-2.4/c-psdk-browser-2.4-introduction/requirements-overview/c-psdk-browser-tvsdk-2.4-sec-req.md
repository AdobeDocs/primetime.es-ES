---
description: Hay que tener en cuenta algunas consideraciones de seguridad para el SDK TVSDK del explorador.
seo-description: Hay que tener en cuenta algunas consideraciones de seguridad para el SDK TVSDK del explorador.
seo-title: Consideraciones de seguridad
title: Consideraciones de seguridad
uuid: 78edf2b0-363c-4ab6-b588-ab4748ee6096
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Consideraciones de seguridad{#security-considerations}

Hay que tener en cuenta algunas consideraciones de seguridad para el SDK TVSDK del explorador.

* **Adobe Flash Player**

   * Flash Player no permite el acceso a datos que residen fuera del dominio desde el que se originó el SWF.

      Para permitir el acceso, aloje un archivo de política entre dominios con los permisos adecuados en la raíz del servidor que aloja los datos. En el modo Flash Fallback del Explorador TVSDK (Flash Player versión 23 y posterior), necesita el token de autorización para su dominio. Para generar el token, póngase en contacto con su representante de Adobe.

* **JavaScript**

   * JavaScript sigue la misma política de origen y evita el acceso a los recursos a través de los límites del dominio.

      Para permitir el acceso a estos recursos, el encabezado Access-Control-Allow-Origin (CORS) debe configurarse en los recursos alojados en orígenes que no sean el reproductor. De forma opcional, si el contenido se especifica mediante intervalos de bytes, la solicitud de opciones de verificación previa de CORS debe indicar que el origen permite estas solicitudes.

* **Exploradores y contenido mixto**

   * Los navegadores requieren que el contenido cifrado AES-128 se aloje en un entorno de origen seguro (por ejemplo, HTTPS).

      Dado que la mayoría de los navegadores no admiten contenido mixto, se recomienda que el reproductor, el contenido y los recursos asociados, como los archivos Key/WebVTT, también se alojen en un origen seguro.

      >[!IMPORTANT]
      >
      >A partir de la versión 2.4.5, si el reproductor está alojado a través de HTTPS, el SDK de TVSDK del explorador convierte las llamadas HTTP a HTTPS al utilizar la tecnología MSE.

