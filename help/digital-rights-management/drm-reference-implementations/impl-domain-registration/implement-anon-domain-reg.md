---
title: Implementación del registro de dominios anónimos
description: Implementación del registro de dominios anónimos
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---


# Implementar el registro de dominio anónimo{#implement-anonymous-domain-registration}

1. Cree una directiva DRM que especifique que se requiere el registro de dominio.
1. Especifique la URL del servidor de dominio como:

   ```
   https://[host:port]/flashaccess/domainserver/domainname/
   ```

1. Haga obligatoria la autenticación anónima.

   En el archivo [!DNL .properties], establezca:

   ```
   policy.domain.anonymous=true 
   ```
