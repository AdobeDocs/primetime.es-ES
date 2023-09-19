---
title: Implementar el registro de dominios basado en identidad
description: Implementar el registro de dominios basado en identidad
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---

# Implementar el registro de dominios basado en identidad{#implement-identity-based-domain-registration}

1. Cree una directiva DRM con registro de dominio obligatorio.
1. Especifique el host y el puerto del servidor para la URL del servidor de dominio.

   En su [!DNL .properties] archivo, establecer:

   ```
   policy.domain.url=https://[server:port] 
   ```

1. Haga obligatoria la autenticación con un nombre de usuario y una contraseña.

   En su [!DNL .properties] archivo, establecer:

   ```
   policy.domain.anonymous=false 
   ```
