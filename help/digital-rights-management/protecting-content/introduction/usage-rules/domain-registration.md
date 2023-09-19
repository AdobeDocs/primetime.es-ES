---
title: Registro de dominio de grupo de dispositivos
description: Registro de dominio de grupo de dispositivos
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Registro de dominio de grupo de dispositivos{#device-group-domain-registration}

Como alternativa al enlace de una licencia a un dispositivo específico, Primetime DRM 3.0 o posterior admite el enlace de licencias a un dominio de dispositivo.

Varios dispositivos pueden unirse a un dominio y recibir tokens de dominio. Una vez que un dispositivo del dominio adquiere una licencia, esta se puede transferir a cualquier otro dispositivo del dominio y esos dispositivos pueden reproducir el contenido sin adquirir una licencia directamente del servidor de licencias.

Si desea admitir licencias enlazadas a dominio, la directiva DRM de Primetime debe especificar el servidor de dominio con el que el cliente debe registrarse. La directiva DRM de Primetime también debe especificar los requisitos de autenticación para el servidor de dominio, ya sea si el acceso anónimo está habilitado o si el servidor requiere un nombre de usuario/contraseña o autenticación personalizada.

Los clientes de Primetime DRM versión 3.0 o posterior admiten el registro de dominios y las licencias enlazadas a dominios. Si un cliente antiguo o un cliente de Adobe Primetime 3.0 en Flash Player solicita una licencia para el contenido que admite el registro de dominios, el servidor de licencias puede emitir una licencia que utilice una directiva DRM de Primetime alternativa para admitir el enlace a un dispositivo específico.
