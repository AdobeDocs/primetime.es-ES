---
seo-title: Registro de dominio de grupo de dispositivos
title: Registro de dominio de grupo de dispositivos
uuid: fd559175-2c3c-4d71-bfa1-8de9907d2b7c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# Registro del dominio del grupo de dispositivos{#device-group-domain-registration}

Como alternativa a enlazar una licencia a un dispositivo específico, Adobe Access 3.0 y versiones posteriores admiten el enlace de licencias a un dominio de dispositivo. Varios dispositivos pueden unirse a un dominio y recibir tokens de dominio. Una vez que un dispositivo del dominio adquiere una licencia, la licencia puede transferirse a cualquier otro dispositivo del dominio y esos dispositivos pueden reproducir el contenido sin adquirir una licencia directamente del servidor de licencias.

Para admitir las licencias enlazadas a dominios, la directiva debe especificar el servidor de dominio en el que debe registrarse el cliente. La directiva también especificará los requisitos de autenticación para el servidor de dominio (si se permite el acceso anónimo o si el servidor requiere un nombre de usuario/contraseña o autenticación personalizada).

Los clientes de Adobe Access versión 3.0 y posteriores admiten el registro de dominios y las licencias enlazadas a dominios. Si un cliente anterior o un cliente de Adobe Access 3.0 en Flash Player solicita una licencia para contenido que admita el registro de dominio, el servidor de licencias puede emitir una licencia mediante una política alternativa que admita el enlace a un dispositivo específico.
