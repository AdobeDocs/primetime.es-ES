---
seo-title: Implementar el registro de dominio basado en la identidad
title: Implementar el registro de dominio basado en la identidad
uuid: 4a71b2e0-d1a2-4d63-9cbd-980a292774ab
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f

---


# Implementar el registro de dominio basado en la identidad{#implement-identity-based-domain-registration}

1. Cree una directiva DRM con registro de dominio obligatorio.
1. Especifique el host y el puerto del servidor para la dirección URL del servidor de dominio.

   En el [!DNL .properties] archivo, configure:

   ```
   policy.domain.url=https://[server:port] 
   ```

1. Hacer obligatoria la autenticación con un nombre de usuario y una contraseña.

   En el [!DNL .properties] archivo, configure:

   ```
   policy.domain.anonymous=false 
   ```
