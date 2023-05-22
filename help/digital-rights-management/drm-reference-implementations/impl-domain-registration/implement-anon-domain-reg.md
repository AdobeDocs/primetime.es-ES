---
title: Implementar el registro de dominio anónimo
description: Implementar el registro de dominio anónimo
copied-description: true
exl-id: 304cfe6f-0917-42ef-a49a-e6c4bc9c10d0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
