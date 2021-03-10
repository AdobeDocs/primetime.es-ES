---
title: Implementación del registro de dominio basado en identidad
description: Implementación del registro de dominio basado en identidad
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# Implementar el registro de dominio basado en identidad{#implement-identity-based-domain-registration}

1. Cree una directiva DRM con registro de dominio obligatorio.
1. Especifique el host y el puerto del servidor para la URL del servidor de dominio.

   En el archivo [!DNL .properties], establezca:

   ```
   policy.domain.url=https://[server:port] 
   ```

1. Haga obligatoria la autenticación con un nombre de usuario y una contraseña.

   En el archivo [!DNL .properties], establezca:

   ```
   policy.domain.anonymous=false 
   ```
