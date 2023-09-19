---
title: Emisión de licencias enlazadas al dominio
description: Emisión de licencias enlazadas al dominio
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# Emisión de licencias enlazadas al dominio{#issuing-domain-bound-licenses}

Para emitir una licencia utilizando una directiva DRM que requiera el registro de dominios, la solicitud del cliente debe incluir un token de dominio válido emitido por el servidor de dominios especificado en la directiva. Cuando el cliente solicita una licencia, incluye automáticamente sus tokens de dominio para cualquier servidor de dominio que se especifique en los metadatos de contenido siempre que se haya registrado con esos servidores de dominio. Si la directiva DRM seleccionada requiere el registro del dominio, el SDK selecciona automáticamente un token de dominio de la solicitud para enlazar la licencia a o devuelve un error si no se ha encontrado ningún token de dominio adecuado.

Un token de dominio se considera válido si no ha caducado y si lo ha emitido una CA de dominio autorizada. El servidor de licencias debe especificar las autoridades de dominio desde las que acepta tokens de dominio configurando `HandlerConfiguration.setDomainCAs()`. Si no se configura ninguna CA de dominio, el servidor de licencias no podrá emitir licencias enlazadas a dominios.

Si los metadatos incluyen varias políticas de DRM, la lógica empresarial del servidor de licencias podría seleccionar una política de DRM basada en si el cliente presentó un token de dominio. Puede utilizar `LicenseRequestMessage.getDomainTokens()` para determinar los dominios con los que se ha registrado el cliente.
