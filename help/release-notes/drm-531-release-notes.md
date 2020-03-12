---
title: Notas de la versión de DRM 5.3.1
seo-title: Notas de la versión de DRM 5.3.1
description: Las notas de la versión de DRM 5.3.1 describen las nuevas funciones y los problemas conocidos de DRM 5.3.1.
seo-description: Las notas de la versión de DRM 5.3.1 describen las nuevas funciones y los problemas conocidos de DRM 5.3.1.
uuid: bb61b79f-a5b3-42ed-8016-495b1ac99ea6
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# Notas de la versión de DRM 5.3.1 {#drm-release-notes}

Las notas de la versión de DRM 5.3.1 describen las nuevas funciones y los problemas conocidos de DRM 5.3.1.

## Nuevas funciones de la versión 5.3 {#new-features}

* **Detención segura:** puede especificar si la reproducción se detiene o continúa al final de una ventana de reproducción.
* **Protección de salida basada en resolución (RBOP):** puede especificar las restricciones de salida en función de las resoluciones de píxeles.
* **CDM Gating -** Para admitir HTML5, Adobe ha actualizado el servidor de licencias de implementación de referencia incluido con el SDK de Java de Adobe Primetime DRM (anteriormente Adobe Access DRM) para poder consumir todos los mensajes de protocolo DRM en un único extremo de URL. Esta consolidación de los métodos de URL HTTP es necesaria para cumplir con la especificación HTML5 EME (Encrypted Media Extension), que a su vez es necesaria para ser implementada por los proveedores de DRM (Content Decryption Module) de CDM. Anteriormente, estos eran los únicos extremos de URL expuestos por el servidor de licencias de implementación de referencia:

   * /flashaccess/i15n/v3 (individualización)
   * /flashaccess/license/v5 (solicitud de licencia)
   * /flashaccess/licenseRet/v5 (devolución de licencia)
   * /flashaccess/getServerVersion/v5 (Get Server Version)

Ahora, todas las solicitudes (procedentes de un MDL HTML5) se pueden dirigir a un único punto final: /req

Este cambio es compatible con versiones anteriores de plataformas que no son del MDL, como Flash Player, Android e iOS.

* **Reducción de escala de RBOP:** específica del espacio HTML5, RBOP contiene capacidad de reducción de escala automática, donde si una velocidad de bits supera la velocidad de bits permitida especificada en la directiva DRM, el contenido se reducirá a la resolución máxima permitida. Por ejemplo, si un flujo 1080p se transmite a un cliente que muestra el contenido en un monitor que no es compatible con HDCP, la directiva DRM puede indicar que la resolución máxima debe ser 720p. Primetime DRM descodificará el flujo 1080p y, a continuación, lo reducirá a 720p antes de procesarlo en pantalla. Si el navegador que reproduce el vídeo se arrastra a un monitor que admite HDCP, Primetime DRM dejará de reducir la escala del contenido y permitirá que se reproduzca a 1080.

## Problemas conocidos en la versión 5.3 {#known-issues}

* `Hasher.bat (flashaccess-hasher.jar)` envía mensajes de registro a `flashaccess-global.log.`Debe asegurarse de que el `flashaccess-global.log` archivo se encuentra en el mismo directorio que Hasher.bat.

* El resultado de algunas de las `toJSON()`llamadas se devuelve `Strings` que no son totalmente compatibles con JSON o totalmente compatibles de forma independiente (es decir, sin la composición de estructuras JSON).

* El servidor de claves Xbox acepta solicitudes de claves que tienen un valor de versión no igual a 1.

El servidor de claves Xbox solo debe admitir solicitudes de claves que tengan la versión igual a 1, pero actualmente, el servidor acepta solicitudes de claves cuando la versión no sea 1.

* El servidor de claves Xbox no valida una directiva correctamente.

El servidor de claves Xbox no debe aceptar directivas que no estén dentro de la fecha de validez, pero actualmente el servidor las acepta independientemente.

* El servidor de claves Xbox debe rechazar una solicitud de clave que contenga metadatos creados con un certificado de empaquetador incorrecto.
* El valor devuelto de algunas estructuras JSON no tiene el formato correcto para clases relacionadas con la protección de salida basadas en resolución.

Varias clases implementan un método toJSON() que debe devolver una representación compatible con JSON de ese objeto como una cadena, pero actualmente el valor devuelto no es totalmente compatible con JSON.

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en la página de información y asistencia [de](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.
