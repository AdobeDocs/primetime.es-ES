---
seo-title: Registro de dominio de grupo de dispositivos
title: Registro de dominio de grupo de dispositivos
uuid: 221bf6c3-0568-443d-b761-64715a57ada6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# Registro del dominio del grupo de dispositivos{#device-group-domain-registration}

Como alternativa a enlazar una licencia a un dispositivo específico, Primetime DRM 3.0 o posterior admite el enlace de licencias a un dominio de dispositivo.

Varios dispositivos pueden unirse a un dominio y recibir tokens de dominio. Una vez que un dispositivo del dominio adquiere una licencia, la licencia puede transferirse a cualquier otro dispositivo del dominio y esos dispositivos pueden reproducir el contenido sin adquirir una licencia directamente del servidor de licencias.

Si desea admitir licencias enlazadas a dominios, la directiva DRM de Primetime debe especificar el servidor de dominio en el que el cliente debe registrarse. La directiva DRM de Primetime también debe especificar los requisitos de autenticación para el servidor de dominio si el acceso anónimo está habilitado o si el servidor requiere un nombre de usuario/contraseña o autenticación personalizada.

Los clientes Primetime DRM versión 3.0 o posterior admiten el registro de dominios y las licencias enlazadas a dominios. Si un cliente anterior o un cliente de Adobe Primetime 3.0 en Flash Player solicita una licencia para contenido que admita el registro de dominio, el servidor de licencias puede emitir una licencia que utilice una directiva DRM de Primetime alternativa para admitir el enlace a un dispositivo específico.
