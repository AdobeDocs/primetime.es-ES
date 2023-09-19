---
title: Notas de la versión de autenticación de Adobe Primetime 2.64.1
description: Notas de la versión de autenticación de Adobe Primetime 2.64.1
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Notas de la versión de autenticación de Adobe Primetime 2.64.1 {#authn-264-rn}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.

En esta página se describen las nuevas funciones, los cambios y los problemas conocidos de esta versión:

## Lado del servidor y clientes web {#server-side-web-clients-2641}

* [Número de compilación](#build-number-2641)
* [Información general de versión](#release-overview-2641)

### Número de compilación {#build-number-2641}

Autenticación de Adobe Primetime: adobe-pass-end **2.64.1**
Fecha de versión: **31/01/2023 - 02/02/2023**

### Información general de versión {#release-overview-2641}

Esta versión añade lo siguiente:

* La capacidad de bloquear respuestas de autenticación no solicitadas de MVPD donde el parámetro &quot;in_response_to&quot; no aparece en la afirmación de SAML.
* Se ha mejorado la validación sobre el parámetro redirect_url para cumplir con los requisitos de seguridad.
* Registro mejorado de la información del dispositivo para solicitudes de autenticación de segunda pantalla, con información proporcionada desde el dispositivo inicial.
