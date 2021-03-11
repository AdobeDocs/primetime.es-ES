---
title: Emisión de licencias enlazadas al dominio
description: Emisión de licencias enlazadas al dominio
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Emisión de licencias enlazadas al dominio{#issuing-domain-bound-licenses}

Para emitir una licencia utilizando una directiva que requiera registro de dominio, la solicitud del cliente debe incluir un token de dominio válido emitido por el servidor de dominio especificado en la directiva. Cuando el cliente solicite una licencia, incluirá automáticamente sus tokens de dominio para cualquier servidor de dominio especificado en los metadatos de contenido, si se ha registrado con esos servidores de dominio. Si la política seleccionada requiere el registro de dominio, el SDK seleccionará automáticamente un token de dominio de la solicitud para enlazar la licencia a o devolverá un error si no se encontró ningún token de dominio apropiado.

Un token de dominio se considera válido si no ha caducado y si ha sido emitido por una CA de dominio autorizada. El servidor de licencias debe especificar las autoridades de dominio desde las que aceptará tokens de dominio configurando `HandlerConfiguration.setDomainCAs()`. Si no hay ninguna CA de dominio configurada, el servidor de licencias no podrá emitir licencias enlazadas a dominio.

Si los metadatos incluyen varias directivas, la lógica empresarial del servidor de licencias podría seleccionar una directiva en función de si el cliente presentó un token de dominio. Utilice `LicenseRequestMessage.getDomainTokens()` para determinar los dominios con los que se ha registrado el cliente.
