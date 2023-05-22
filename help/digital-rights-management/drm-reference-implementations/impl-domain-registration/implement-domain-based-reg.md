---
title: Implementar el registro de dominios basado en identidad
description: Implementar el registro de dominios basado en identidad
copied-description: true
exl-id: e2f826a8-eea5-4d5f-ac4d-401d7a6c5373
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
