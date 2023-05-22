---
description: Hay que tener en cuenta algunas consideraciones de seguridad para el TVSDK del explorador.
title: Consideraciones de seguridad
exl-id: bc98890a-082a-4e2d-b927-ecb3bd878de9
source-git-commit: 78be1575cc7bd6630a7bf85faa061327e5c414d7
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# Consideraciones de seguridad{#security-considerations}

Hay que tener en cuenta algunas consideraciones de seguridad para el TVSDK del explorador.

* **Flash Player de Adobe**

   * El Flash Player no permite el acceso a los datos que residen fuera del dominio desde el que se originó el SWF.

      Para permitir el acceso, aloje un archivo de directiva entre dominios con los permisos adecuados en la raíz del servidor que aloja los datos. En el modo de reserva de Flash del TVSDK del explorador (versión 23 del Flash Player y posteriores), necesita el token de autorización para su dominio. Para generar el token, póngase en contacto con el representante de Adobe.

* **JavaScript**

   * JavaScript sigue la misma directiva de origen y evita el acceso a los recursos a través de los límites del dominio.

      Para permitir el acceso a estos recursos, el encabezado Access-Control-Allow-Origin (CORS) debe configurarse en los recursos alojados en orígenes distintos al reproductor. De forma opcional, si el contenido se especifica mediante intervalos de bytes, la solicitud de opciones de comprobación previa de CORS debe indicar que el origen permite estas solicitudes.

* **Navegadores y contenido mixto**

   * Los navegadores requieren que el contenido cifrado AES-128 se aloje en un origen seguro (por ejemplo, HTTPS).

      Dado que la mayoría de los navegadores no permiten contenido mixto, recomendamos que el reproductor, el contenido y los recursos asociados, como los archivos Key/ WebVTT, también se alojen a través de un origen seguro.

      >[!IMPORTANT]
      >
      >A partir de la versión 2.4.5, si el reproductor está alojado a través de HTTPS, el TVSDK del explorador convierte las llamadas HTTP a HTTPS cuando se utiliza la tecnología MSE.
