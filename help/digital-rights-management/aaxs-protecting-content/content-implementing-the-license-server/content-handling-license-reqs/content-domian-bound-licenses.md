---
title: Emisión de licencias enlazadas al dominio
description: Emisión de licencias enlazadas al dominio
copied-description: true
exl-id: b9823ae4-d88f-4580-a2ce-275ed3e32f51
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Emisión de licencias enlazadas al dominio{#issuing-domain-bound-licenses}

Para emitir una licencia mediante una directiva que requiera el registro de dominios, la solicitud del cliente debe incluir un token de dominio válido emitido por el servidor de dominios especificado en la directiva. Cuando el cliente solicita una licencia, incluirá automáticamente sus tokens de dominio para cualquier servidor de dominio especificado en los metadatos de contenido, si se ha registrado en esos servidores de dominio. Si la directiva seleccionada requiere el registro del dominio, el SDK seleccionará automáticamente un token de dominio de la solicitud a la que enlazar la licencia o devolverá un error si no se encuentra ningún token de dominio adecuado.

Un token de dominio se considera válido si no ha caducado y si lo ha emitido una CA de dominio autorizada. El servidor de licencias debe especificar las autoridades de dominio desde las que aceptará tokens de dominio configurando `HandlerConfiguration.setDomainCAs()`. Si no se configura ninguna CA de dominio, el servidor de licencias no podrá emitir licencias enlazadas a dominios.

Si los metadatos incluyen varias directivas, la lógica empresarial del servidor de licencias podría seleccionar una directiva en función de si el cliente presentó un token de dominio. Uso `LicenseRequestMessage.getDomainTokens()` para determinar los dominios con los que se ha registrado el cliente.
