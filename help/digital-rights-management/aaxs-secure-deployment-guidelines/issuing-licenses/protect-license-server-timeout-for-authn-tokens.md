---
title: Tiempo de espera para tokens de autenticación
description: Tiempo de espera para tokens de autenticación
copied-description: true
exl-id: ee9c5b2c-6a79-499c-bd60-718e33bc3a9b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Tiempo de espera para tokens de autenticación{#timeout-for-authentication-tokens}

Todos los tokens de autenticación generados por el SDK de acceso a Adobe tienen un intervalo de tiempo de espera para proteger la seguridad de la aplicación. La caducidad del token de autenticación se especifica al usar el SDK de acceso de Adobe al administrar una solicitud de autenticación. Una vez superada la caducidad, el token de autenticación deja de ser válido y el usuario debe volver a autenticarse con el servidor de licencias.

Para obtener más información sobre las solicitudes de autenticación, consulte AuthenticationHandler en la *Referencia de API de acceso de Adobe*.
