---
seo-title: Emisión de licencias enlazadas a dominios
title: Emisión de licencias enlazadas a dominios
uuid: 706650b7-6044-4c01-9f5a-90779127c9e1
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Emisión de licencias enlazadas a dominios{#issuing-domain-bound-licenses}

Para emitir una licencia mediante una directiva DRM que requiera el registro de dominio, la solicitud del cliente debe incluir un token de dominio válido emitido por el servidor de dominio especificado en la directiva. Cuando el cliente solicita una licencia, incluye automáticamente sus tokens de dominio para cualquier servidor de dominio especificado en los metadatos de contenido, siempre que se haya registrado en esos servidores de dominio. Si la directiva DRM seleccionada requiere el registro de dominio, el SDK selecciona automáticamente un token de dominio de la solicitud para enlazar la licencia a o devuelve un error si no se ha encontrado ningún token de dominio adecuado.

Un token de dominio se considera válido si no ha caducado y si ha sido emitido por una CA de dominio autorizada. El servidor de licencias debe especificar las autoridades de dominio desde las que acepta los tokens de dominio configurando `HandlerConfiguration.setDomainCAs()`. Si no hay ninguna CA de dominio configurada, el servidor de licencias no podrá emitir licencias enlazadas a dominios.

Si los metadatos incluyen varias directivas DRM, la lógica empresarial del servidor de licencias podría seleccionar una directiva DRM basada en si el cliente presentó un token de dominio. Puede utilizar `LicenseRequestMessage.getDomainTokens()` para determinar los dominios con los que se ha registrado el cliente.
