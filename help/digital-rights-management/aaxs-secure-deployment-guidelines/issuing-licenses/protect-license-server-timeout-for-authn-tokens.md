---
title: Tiempo de espera para los tokens de autenticación
description: Tiempo de espera para los tokens de autenticación
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# Tiempo de espera para los tokens de autenticación{#timeout-for-authentication-tokens}

Todos los tokens de autenticación generados por el SDK de acceso a Adobe tienen un intervalo de tiempo de espera para proteger la seguridad de la aplicación. La caducidad del token de autenticación se especifica usar el SDK de acceso al Adobe al gestionar una solicitud de autenticación. Una vez que ha pasado la caducidad, el token de autenticación ya no es válido y el usuario debe volver a autenticarse con el servidor de licencias.

Para obtener más información sobre las solicitudes de autenticación, consulte AuthenticationHandler en la *Referencia de API de acceso al Adobe*.
