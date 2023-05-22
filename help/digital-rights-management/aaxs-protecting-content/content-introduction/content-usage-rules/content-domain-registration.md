---
title: Registro de dominio de grupo de dispositivos
description: Registro de dominio de grupo de dispositivos
copied-description: true
exl-id: 1f3e9d26-c185-4d12-accf-aa74a313f890
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# Registro de dominio de grupo de dispositivos{#device-group-domain-registration}

Como alternativa al enlace de una licencia a un dispositivo específico, Adobe Access 3.0 y versiones posteriores admite el enlace de licencias a un dominio de dispositivo. Varios dispositivos pueden unirse a un dominio y recibir tokens de dominio. Una vez que un dispositivo del dominio adquiere una licencia, esta se puede transferir a cualquier otro dispositivo del dominio y esos dispositivos pueden reproducir el contenido sin adquirir una licencia directamente del servidor de licencias.

Para admitir las licencias enlazadas al dominio, la directiva debe especificar el servidor de dominio con el que el cliente debe registrarse. La directiva también especificará los requisitos de autenticación para el servidor de dominio (si se permite el acceso anónimo o si el servidor requiere un nombre de usuario/contraseña o autenticación personalizada).

Los clientes de Adobe Access versión 3.0 y posteriores admiten el registro de dominios y las licencias enlazadas a dominios. Si un cliente antiguo o un cliente de Adobe Access 3.0 en Flash Player solicita una licencia para el contenido que admite el registro de dominios, el servidor de licencias puede emitir una licencia mediante una directiva alternativa que admita el enlace a un dispositivo específico.
