---
title: Registro de dominios del grupo de dispositivos
description: Registro de dominios del grupo de dispositivos
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# Registro del dominio del grupo de dispositivos{#device-group-domain-registration}

Como alternativa al enlace de una licencia a un dispositivo específico, Adobe Access 3.0 y versiones posteriores admiten el enlace de licencias a un dominio del dispositivo. Es posible que varios dispositivos se unan a un dominio y reciban tokens de dominio. Una vez que un dispositivo del dominio adquiere una licencia, la licencia se puede transferir a cualquier otro dispositivo del dominio y esos dispositivos pueden reproducir el contenido sin adquirir una licencia directamente desde el servidor de licencias.

Para admitir las licencias enlazadas al dominio, la directiva debe especificar el servidor de dominio en el que el cliente debe registrarse. La directiva también especificará los requisitos de autenticación para el servidor de dominio (si se permite el acceso anónimo o si el servidor requiere un nombre de usuario/contraseña o autenticación personalizada).

Los clientes de Adobe Access versión 3.0 y posteriores admiten el registro de dominios y las licencias enlazadas a dominios. Si un cliente antiguo o un cliente de Adobe Access 3.0 en Flash Player solicita una licencia para el contenido que admita el registro de dominios, el servidor de licencias puede emitir una licencia utilizando una directiva alternativa que admita el enlace a un dispositivo específico.
