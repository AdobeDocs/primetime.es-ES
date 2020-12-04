---
seo-title: Tiempo de espera para los tokens de autenticación
title: Tiempo de espera para los tokens de autenticación
uuid: 41b0fbf5-a567-4118-bec1-c05e6e0b6d1f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# Tiempo de espera para autentificadores{#timeout-for-authentication-tokens}

Todos los tokens de autenticación generados por el SDK de Adobe Access tienen un intervalo de tiempo de espera para proteger la seguridad de la aplicación. La caducidad del token de autenticación se especifica mediante el uso del SDK de Adobe Access al administrar una solicitud de autenticación. Una vez que la caducidad ha pasado, el autentificador ya no es válido y el usuario debe volver a autenticarse con el servidor de licencias.

Para obtener más información sobre las solicitudes de autenticación, consulte AuthenticationHandler en la *Referencia de API de acceso a Adobe*.
