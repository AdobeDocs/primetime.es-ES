---
title: Implementar el registro de dominio anónimo
description: Implementar el registro de dominio anónimo
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---

# Implementar el registro de dominio anónimo{#implement-anonymous-domain-registration}

1. Cree una directiva DRM que especifique que se requiere el registro del dominio.
1. Especifique la URL del servidor de dominio como:

   ```
   https://[host:port]/flashaccess/domainserver/domainname/
   ```

1. Hacer la autenticación anónima obligatoria.

   En su [!DNL .properties] archivo, establecer:

   ```
   policy.domain.anonymous=true 
   ```
