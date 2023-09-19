---
title: Notas de la versión de DRM 5.3.1
description: Las notas de la versión 5.3.1 de DRM describen las nuevas funciones y los problemas conocidos de DRM 5.3.1.
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# Notas de la versión de DRM 5.3.1 {#drm-release-notes}

Las notas de la versión 5.3.1 de DRM describen las nuevas funciones y los problemas conocidos de DRM 5.3.1.

## Nuevas funciones de la versión 5.3 {#new-features}

* **Parada segura -** Puede especificar si la reproducción se detiene o continúa al final de una ventana de reproducción.
* **Protección de salida basada en resolución (RBOP):** Puede especificar las restricciones de salida en función de las resoluciones de píxel.
* **Puerta de CDM:** Para admitir HTML5, Adobe ha actualizado el servidor de licencias de implementación de referencia incluido con el SDK de Java de Adobe Primetime DRM (anteriormente DRM de acceso de Adobe) para poder consumir todos los mensajes de protocolo DRM en un único punto final de URL. Esta consolidación de los métodos de URL HTTP es necesaria para cumplir con la especificación de HTML5 EME (Encrypted Media Extension) que a su vez deben implementar los proveedores de DRM de CDM (Content Decryption Module). Anteriormente, estos eran los únicos extremos de URL expuestos por el servidor de licencias de implementación de referencia:

   * /flashaccess/i15n/v3 (Individualización)
   * /flashaccess/license/v5 (Solicitud de licencia)
   * /flashaccess/licenseRet/v5 (devolución de licencia)
   * /flashaccess/getServerVersion/v5 (Obtener versión del servidor)

Ahora, todas las solicitudes (que se originan en un CDM de HTML5) se pueden dirigir a un único punto final: /req

Este cambio es compatible con las plataformas que no son de CDM, como Flash Player, Android y iOS.

* **Reducción de RBOP -** Específico del espacio de HTML 5, RBOP contiene la capacidad de reducción de escala automática, donde si una velocidad de bits que excede la velocidad de bits permitida especificada en la directiva DRM, el contenido se reducirá a la resolución máxima permitida. Por ejemplo, si se transmite un flujo de 1080p a un cliente que muestra el contenido en un monitor no compatible con HDCP, la directiva DRM puede indicar que la resolución máxima debe ser de 720p. Primetime DRM descodificará el flujo de 1080p y luego lo reducirá a 720p antes de procesarlo en pantalla. Si el navegador que reproduce el vídeo se arrastra a un monitor que sí admite HDCP, Primetime DRM dejará de reducir la escala del contenido y permitirá que se reproduzca a 1080.

## Problemas conocidos de la versión 5.3 {#known-issues}

* `Hasher.bat (flashaccess-hasher.jar)` envía mensajes de registro a `flashaccess-global.log.`Debe asegurarse de que la variable `flashaccess-global.log` El archivo está en el mismo directorio que Hasher.bat.

* El resultado de algunos de los `toJSON()`devolución de llamadas `Strings` que no son totalmente compatibles con JSON o que no son totalmente compatibles de forma independiente (es decir, sin composición de estructuras JSON).

* El servidor de claves Xbox acepta solicitudes de claves que tienen un valor de versión distinto de 1.

El servidor de claves de Xbox solo debe admitir solicitudes de claves cuya versión sea igual a 1; sin embargo, actualmente, el servidor acepta solicitudes de claves cuya versión no sea 1.

* El servidor de claves Xbox no valida una directiva correctamente.

El servidor de claves Xbox no debe aceptar directivas que estén fuera de la fecha de validez, pero actualmente, el servidor las acepta independientemente.

* El servidor de claves Xbox debe rechazar una solicitud de clave que contenga metadatos creados con un certificado de empaquetador incorrecto.
* El valor devuelto de algunas estructuras JSON no tiene el formato correcto para las clases relacionadas con la protección de salida basada en la resolución.

Varias clases implementan un método toJSON() que debería devolver una representación compatible con JSON de ese objeto como String, pero actualmente el valor devuelto no es totalmente compatible con JSON.

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en [Formación y asistencia de Adobe Primetime](https://helpx.adobe.com/support/primetime.html) página.
