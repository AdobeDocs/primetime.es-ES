---
description: Adobe proporciona un servicio de Cloud DRM a los clientes de Adobe Primetime DRM que no desean desarrollar y mantener su propio servidor de licencias de Primetime DRM. Al utilizar este servicio, los clientes pueden reducir la complejidad operativa y de desarrollo en torno a la emisión de licencias DRM. El DRM de Primetime Cloud puede emitir licencias de DRM en todos los dispositivos capaces de ejecutar una aplicación de vídeo habilitada para TVSDK del explorador Primetime, como iOS, Android, equipos de escritorio y Xbox360. Este servicio de DRM está alojado y mantenido por Adobe, con tiempo activo las 24 horas del día, los 7 días de la semana.
title: Contexto
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Fondo {#background}

Adobe proporciona un servicio de Cloud DRM a los clientes de Adobe Primetime DRM que no desean desarrollar y mantener su propio servidor de licencias de Primetime DRM. Al utilizar este servicio, los clientes pueden reducir la complejidad operativa y de desarrollo en torno a la emisión de licencias DRM. El DRM de Primetime Cloud puede emitir licencias de DRM en todos los dispositivos capaces de ejecutar una aplicación de vídeo habilitada para TVSDK del explorador Primetime, como iOS, Android, equipos de escritorio y Xbox360. Este servicio de DRM está alojado y mantenido por Adobe, con tiempo activo las 24 horas del día, los 7 días de la semana.

>[!NOTE]
>
>Adobe Primetime DRM antes se llamaba Acceso a Adobe y antes de eso, Flash Access.

## Qué se incluye con Primetime Cloud DRM {#section_788D0DD5F6DB41678FD87CFBD21B25FD}

* Módulo de autenticación/derecho personalizado e instrucciones sobre cómo interactuar con la autenticación personalizada para su contenido. Para obtener más documentación, consulte el directorio [!DNL Custom Authentication Entitlement] .
* Certificado de servidor de licencias específico de Cloud DRM ( [!DNL .pem/.cer/.der])

* Certificado de transporte del servidor de licencias específico de Cloud DRM ( [!DNL .pem/.cer/.der])

* Paquete sin conexión Java de Primetime
* Políticas de DRM de muestra para paquetes

   * **policy_24hr** : licencia de caché en disco durante 24 horas. Después de 24 horas, se debe adquirir una nueva licencia para ver el contenido. Todas las demás directivas de este kit también tienen almacenamiento en caché de licencias las 24 horas.
   * **policy_ios_remotekeyserver** : en dispositivos iOS, la licencia DRM se adquirirá de Cloud DRM. Además, el cliente adquirirá todas las claves de descifrado de AES de Cloud DRM. No se permite la reproducción en dispositivos iOS interrumpidos.

   * **policy_ios_localkeyserver** : en dispositivos iOS, la licencia DRM se adquirirá de Cloud DRM. Además, el cliente adquirirá todas las claves de descifrado HLS AES de un servidor HTTP local, en lugar de Cloud DRM. No se permite la reproducción en dispositivos iOS interrumpidos.

   * **policy_adobePass** : el cliente debe autenticarse primero con (antes denominado Adobe Pass) o se denegará una licencia.

* Herramienta Administrador de políticas de Adobe para crear políticas adicionales de DRM
* Contenido de vídeo de muestra para su uso en paquetes

