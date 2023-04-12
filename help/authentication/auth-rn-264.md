---
title: Notas de la versión de la autenticación de Adobe Primetime 2.64
description: Notas de la versión de la autenticación de Adobe Primetime 2.64
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# Notas de la versión de la autenticación de Adobe Primetime 2.64 {#authn-264-rn}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

Esta página describe nuevas funciones, cambios y problemas conocidos con esta versión:

## Clientes web y del lado del servidor {#ss-web-clients}

* [Número de compilación](#build-no-264)
* [Nuevas funciones](#new-featres-264)
* [Correcciones de errores](#bug-fixes-264)


### Número de compilación {#build-no-264}

Autenticación de Adobe Primetime: adobe-pass-**2,64**

Fecha de versión: **8/11/2022 - 11/10/2022**

### Nuevas funciones {#new-featres-264}

* Actualizaciones de infraestructura, destinadas a reducir los tiempos de respuesta del servidor, mejorando el rendimiento general del sistema.
* Mejoras en el nuevo mecanismo de identificación de plataformas.
* Posibilidad de bloquear respuestas de autenticación no solicitadas de MVPD donde falta el parámetro &quot;in_response_to&quot; en la aserción SAML.

### Correcciones de errores {#bug-fixes-264}

* Se ha corregido un formato incorrecto de algunos tokens de TempPass heredados.
* Se han corregido problemas menores en el flujo de autenticación de la segunda pantalla.
