---
description: Adobe proporciona un servicio DRM en la nube a los clientes de DRM de Adobe Primetime que no desean desarrollar y mantener su propio servidor de licencias DRM de Primetime. Al utilizar este servicio, los clientes pueden reducir la complejidad operativa y de desarrollo relacionada con la emisión de licencias de DRM. Primetime Cloud DRM puede emitir licencias DRM a todos los dispositivos capaces de ejecutar una aplicación de vídeo habilitada para TVSDK del explorador de Primetime, como iOS, Android, Escritorios y Xbox360. Este servicio DRM se aloja y mantiene por Adobe, con tiempo de actividad 24/7.
title: Fondo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# Fondo {#background}

Adobe proporciona un servicio DRM en la nube a los clientes de DRM de Adobe Primetime que no desean desarrollar y mantener su propio servidor de licencias DRM de Primetime. Al utilizar este servicio, los clientes pueden reducir la complejidad operativa y de desarrollo relacionada con la emisión de licencias de DRM. Primetime Cloud DRM puede emitir licencias DRM a todos los dispositivos capaces de ejecutar una aplicación de vídeo habilitada para TVSDK del explorador de Primetime, como iOS, Android, Escritorios y Xbox360. Este servicio DRM se aloja y mantiene por Adobe, con tiempo de actividad 24/7.

>[!NOTE]
>
>Adobe Primetime DRM se llamaba anteriormente Acceso de Adobe y, antes de eso, Flash Access.

## Qué se incluye con Primetime Cloud DRM {#section_788D0DD5F6DB41678FD87CFBD21B25FD}

* Módulo de autenticación/derechos personalizados e instrucciones sobre cómo utilizar la autenticación personalizada para el contenido. Para obtener más documentación, consulte la [!DNL Custom Authentication Entitlement] directorio.
* Certificado de servidor de licencias específico de DRM de la nube ( [!DNL .pem/.cer/.der])

* Certificado de transporte del servidor de licencias específico de DRM de la nube ( [!DNL .pem/.cer/.der])

* Empaquetador sin conexión Java de Primetime
* Ejemplo de directivas DRM para paquetes

   * **policy_24hr** - Licencia de caché en disco durante 24 horas. Después de 24 horas, se debe adquirir una nueva licencia para ver el contenido. Todas las demás directivas de este kit también tienen almacenamiento en caché de licencias de 24 horas.
   * **policy_ios_remotekeyserver** : En dispositivos iOS, la licencia DRM se adquirirá desde Cloud DRM. Además, el cliente adquirirá todas las claves de descifrado de AES de Cloud DRM. La reproducción no está permitida en dispositivos iOS con jailbreak.

   * **policy_ios_localkeyserver** : En dispositivos iOS, la licencia DRM se adquirirá desde Cloud DRM. Además, el cliente adquirirá todas las claves de descifrado AES de HLS de un servidor HTTP local, en lugar de Cloud DRM. La reproducción no está permitida en dispositivos iOS con jailbreak.

   * **policy_adobePass** : el cliente debe autenticarse primero con (anteriormente denominado Adobe Pass) o se denegará una licencia.

* Herramienta Administrador de políticas de Adobe para crear políticas DRM adicionales
* Contenido de vídeo de muestra para su uso en el empaquetado
