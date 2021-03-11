---
title: Registro de dominios del grupo de dispositivos
description: Registro de dominios del grupo de dispositivos
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# Registro del dominio del grupo de dispositivos{#device-group-domain-registration}

Como alternativa al enlace de una licencia a un dispositivo específico, Primetime DRM 3.0 o posterior admite el enlace de licencias a un dominio del dispositivo.

Es posible que varios dispositivos se unan a un dominio y reciban tokens de dominio. Una vez que un dispositivo del dominio adquiere una licencia, la licencia se puede transferir a cualquier otro dispositivo del dominio y esos dispositivos pueden reproducir el contenido sin adquirir una licencia directamente desde el servidor de licencias.

Si desea admitir cualquier licencia enlazada al dominio, la directiva DRM de Primetime debe especificar el servidor de dominio con el que el cliente debe registrarse. La directiva DRM de Primetime también debe especificar los requisitos de autenticación para el servidor de dominio si el acceso anónimo está habilitado o si el servidor requiere un nombre de usuario/contraseña o autenticación personalizada.

Los clientes de Primetime DRM versión 3.0 o posterior admiten el registro de dominios y las licencias enlazadas a dominios. Si un cliente antiguo o un cliente de Adobe Primetime 3.0 en Flash Player solicitan una licencia para contenido que admita el registro de dominios, el servidor de licencias puede emitir una licencia que utilice una directiva DRM de Primetime alternativa para admitir el enlace a un dispositivo específico.
