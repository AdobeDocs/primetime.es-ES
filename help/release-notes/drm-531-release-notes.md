---
title: Notas de la versión de DRM 5.3.1
description: Las notas de la versión de DRM 5.3.1 describen las nuevas funciones y los problemas conocidos de DRM 5.3.1.
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---


# Notas de la versión de DRM 5.3.1 {#drm-release-notes}

Las notas de la versión de DRM 5.3.1 describen las nuevas funciones y los problemas conocidos de DRM 5.3.1.

## Nuevas funciones de la versión 5.3 {#new-features}

* **Parada segura:** puede especificar si la reproducción se detiene o continúa al final de una ventana de reproducción.
* **Protección de salida basada en resolución (RBOP):** puede especificar las restricciones de salida en función de las resoluciones de píxeles.
* **Gating de CDM:** para admitir HTML5, Adobe ha actualizado el servidor de licencias de implementación de referencia incluido con el SDK de Java de Adobe Primetime DRM (anteriormente DRM de acceso a Adobe) para poder consumir todos los mensajes de protocolo DRM en un único extremo de URL. Esta consolidación de los métodos de URL HTTP es necesaria para cumplir con la especificación HTML5 EME (Encrypted Media Extension) que a su vez es necesaria para que los proveedores de DRM (Content Decryption Module) implementen. Anteriormente, estos eran los únicos extremos de URL expuestos por el servidor de licencias de Implementación de referencia:

   * /flashaccess/i15n/v3 (Individualización)
   * /flashaccess/license/v5 (solicitud de licencia)
   * /flashaccess/licenseRet/v5 (devolución de licencia)
   * /flashaccess/getServerVersion/v5 (obtener versión del servidor)

Ahora, todas las solicitudes (procedentes de un MDL HTML5) se pueden dirigir a un único punto final: /req

Este cambio es compatible con las plataformas que no son del MDL, como Flash Player, Android o iOS.

* **Reducción de escala de RBOP:** específico del espacio HTML5, RBOP contiene la capacidad de reducción automática, donde si una velocidad de bits que supera la velocidad de bits permitida especificada en la política de DRM, el contenido se reducirá a la resolución máxima permitida. Por ejemplo, si un flujo 1080p se transmite a un cliente que muestra el contenido en un monitor que no es compatible con HDCP, la directiva DRM puede indicar que la resolución máxima debe ser 720p. Primetime DRM descodificará el flujo 1080p y luego lo reducirá a 720p antes de procesarlo en pantalla. Si el navegador que reproduce el vídeo se arrastra a un monitor compatible con HDCP, Primetime DRM dejará de reducir la escala del contenido y permitirá que se reproduzca a 1080.

## Problemas conocidos en la versión 5.3 {#known-issues}

* `Hasher.bat (flashaccess-hasher.jar)` envía mensajes de registro a  `flashaccess-global.log.`Debe asegurarse de que el  `flashaccess-global.log` archivo se encuentra en el mismo directorio que Hasher.bat.

* El resultado de algunas de las `toJSON()`llamadas devuelve `Strings` que no son totalmente compatibles con JSON ni totalmente compatibles de forma independiente (es decir, sin la composición de estructuras JSON).

* El servidor de claves Xbox acepta solicitudes de claves que tienen un valor de versión no igual a 1.

El servidor de claves Xbox solo debe admitir solicitudes de claves que tengan la versión igual a 1, pero actualmente, el servidor acepta solicitudes de claves en las que la versión no sea 1.

* El servidor de claves Xbox no valida correctamente una directiva.

El servidor de claves Xbox no debe aceptar directivas que estén fuera de la fecha de validez, pero actualmente, el servidor las acepta de todas formas.

* El servidor de claves Xbox debe rechazar una solicitud de clave que contenga un metadatos creado con un certificado de empaquetador incorrecto.
* El valor devuelto de algunas estructuras JSON no tienen el formato correcto para las clases relacionadas con la protección de salida basadas en resolución.

Varias clases implementan un método toJSON() que debería devolver una representación compatible con JSON de ese objeto como una cadena, pero actualmente el valor devuelto no es totalmente compatible con JSON.

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en la página [Aprendizaje y asistencia de Adobe Primetime](https://helpx.adobe.com/support/primetime.html).
