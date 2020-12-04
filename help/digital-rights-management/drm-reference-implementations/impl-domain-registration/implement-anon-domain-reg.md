---
seo-title: Implementar el registro de dominios anónimos
title: Implementar el registro de dominios anónimos
uuid: 330d32fd-8c23-40f9-949b-635e5a9acc86
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f
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

1. Hacer obligatoria la autenticación anónima.

   En el archivo [!DNL .properties], establezca:

   ```
   policy.domain.anonymous=true 
   ```
