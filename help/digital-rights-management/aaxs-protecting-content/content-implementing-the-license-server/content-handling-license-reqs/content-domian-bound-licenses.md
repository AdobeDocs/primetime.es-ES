---
seo-title: Emisión de licencias enlazadas al dominio
title: Emisión de licencias enlazadas al dominio
uuid: 175d3b7d-d1df-44ee-85ad-a0db4a1bdb9d
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Emisión de licencias enlazadas al dominio{#issuing-domain-bound-licenses}

Para emitir una licencia mediante una directiva que requiera el registro de dominio, la solicitud del cliente debe incluir un token de dominio válido emitido por el servidor de dominio especificado en la directiva. Cuando el cliente solicita una licencia, incluirá automáticamente sus tokens de dominio para cualquier servidor de dominio especificado en los metadatos de contenido, si se ha registrado en esos servidores de dominio. Si la directiva seleccionada requiere el registro de dominio, el SDK seleccionará automáticamente un token de dominio de la solicitud para enlazar la licencia a o devolver un error si no se encontró ningún token de dominio adecuado.

Un token de dominio se considera válido si no ha caducado y si ha sido emitido por una CA de dominio autorizada. El servidor de licencias debe especificar las autoridades de dominio desde las que aceptará tokens de dominio configurando `HandlerConfiguration.setDomainCAs()`. Si no hay ninguna CA de dominio configurada, el servidor de licencias no podrá emitir licencias enlazadas a dominios.

Si los metadatos incluyen varias directivas, la lógica empresarial del servidor de licencias podría seleccionar una directiva en función de si el cliente presentó un token de dominio. Se utiliza `LicenseRequestMessage.getDomainTokens()` para determinar los dominios con los que se ha registrado el cliente.
