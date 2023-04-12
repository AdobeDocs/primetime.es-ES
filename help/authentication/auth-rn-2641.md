---
title: Notas de la versión 2.64.1 de la autenticación de Adobe Primetime
description: Notas de la versión 2.64.1 de la autenticación de Adobe Primetime
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# Notas de la versión 2.64.1 de la autenticación de Adobe Primetime {#authn-264-rn}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

Esta página describe nuevas funciones, cambios y problemas conocidos con esta versión:

## Clientes web y del lado del servidor {#server-side-web-clients-2641}

* [Número de compilación](#build-number-2641)
* [Información general de la versión](#release-overview-2641)

### Número de compilación {#build-number-2641}

Autenticación de Adobe Primetime: adobe-pass-**2,64,1**
Fecha de versión: **31/1/2023 - 02/02/2023**

### Información general de la versión {#release-overview-2641}

Esta versión agrega lo siguiente:

* La capacidad de bloquear respuestas de autenticación no solicitada de MVPD donde falta el parámetro &quot;in_response_to&quot; en la afirmación SAML.
* Se ha mejorado la validación del parámetro redirect_url para cumplir los requisitos de seguridad.
* Registro mejorado de la información del dispositivo para solicitudes de autenticación de segunda pantalla, mediante el uso de la información proporcionada desde el dispositivo inicial.
