---
description: Adobe proporciona un servicio de DRM en la nube a los clientes de DRM de Adobe Primetime que no deseen desarrollar y mantener su propio servidor de licencias de DRM de Primetime. Al utilizar este servicio, los clientes pueden reducir la complejidad operativa y de desarrollo en torno a la emisión de licencias DRM. Primetime Cloud DRM puede emitir licencias de DRM a todos los dispositivos capaces de ejecutar una aplicación de vídeo compatible con TVSDK de Primetime Browser, como iOS, Android, Equipos de escritorio y Xbox360. Adobe aloja y mantiene este servicio de DRM, con tiempo de actividad las 24 horas del día, los 7 días de la semana.
seo-description: Adobe proporciona un servicio de DRM en la nube a los clientes de DRM de Adobe Primetime que no deseen desarrollar y mantener su propio servidor de licencias de DRM de Primetime. Al utilizar este servicio, los clientes pueden reducir la complejidad operativa y de desarrollo en torno a la emisión de licencias DRM. Primetime Cloud DRM puede emitir licencias de DRM a todos los dispositivos capaces de ejecutar una aplicación de vídeo compatible con TVSDK de Primetime Browser, como iOS, Android, Equipos de escritorio y Xbox360. Adobe aloja y mantiene este servicio de DRM, con tiempo de actividad las 24 horas del día, los 7 días de la semana.
seo-title: Fondo
title: Fondo
uuid: 11a5b9ea-ebd2-47e0-b078-af2a3e1f7bf6
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Fondo {#background}

Adobe proporciona un servicio de DRM en la nube a los clientes de DRM de Adobe Primetime que no deseen desarrollar y mantener su propio servidor de licencias de DRM de Primetime. Al utilizar este servicio, los clientes pueden reducir la complejidad operativa y de desarrollo en torno a la emisión de licencias DRM. Primetime Cloud DRM puede emitir licencias de DRM a todos los dispositivos capaces de ejecutar una aplicación de vídeo compatible con TVSDK de Primetime Browser, como iOS, Android, Equipos de escritorio y Xbox360. Adobe aloja y mantiene este servicio de DRM, con tiempo de actividad las 24 horas del día, los 7 días de la semana.

>[!NOTE]
>
>Adobe Primetime DRM se llamaba anteriormente Adobe Access y, antes, Flash Access.

## Qué incluye Primetime Cloud DRM {#section_788D0DD5F6DB41678FD87CFBD21B25FD}

* Módulo de autenticación/asignación de derechos personalizados e instrucciones sobre cómo interactuar con la autenticación personalizada para su contenido. Para obtener más documentación, consulte el [!DNL Custom Authentication Entitlement] directorio.
* Certificado de servidor de licencias específico de DRM de nube ( [!DNL .pem/.cer/.der])

* Certificado de transporte de servidor de licencias específico para DRM de nube ( [!DNL .pem/.cer/.der])

* Primetime Java Offline Packager
* Directivas de DRM de muestra para paquetes

   * **policy_24hr** - Licencia de memoria caché en disco durante 24 horas. Después de 24 horas, se debe adquirir una nueva licencia para ver el contenido. Todas las demás directivas de este kit también tienen caché de licencias las 24 horas.
   * **policy_ios_remotekeyserver** : en dispositivos iOS, la licencia DRM se adquirirá de Cloud DRM. Además, el cliente adquirirá todas las claves de descifrado de AES de Cloud DRM. No se permite la reproducción en dispositivos iOS dañados por la cárcel.

   * **policy_ios_localkeyserver** : en dispositivos iOS, la licencia DRM se adquirirá desde Cloud DRM. Además, el cliente adquirirá todas las claves de descifrado HLS AES de un servidor HTTP local, en lugar de Cloud DRM. No se permite la reproducción en dispositivos iOS dañados por la cárcel.

   * **policy_adobePass** : El cliente debe autenticarse primero con (anteriormente denominado Adobe Pass) o se denegará una licencia.

* Herramienta Administrador de políticas de Adobe para crear políticas de DRM adicionales
* Contenido de vídeo de muestra que se va a utilizar para empaquetar

