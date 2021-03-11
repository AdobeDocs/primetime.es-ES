---
description: 'Adobe Access Server para la transmisión protegida requiere dos tipos de archivos de configuración: un archivo de configuración global (flashaccess-global.xml) y un archivo de configuración de inquilino para cada inquilino (flashaccess-tenant.xml).'
title: Estructura del directorio de configuración
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Archivos de configuración del servidor de licencias y estructura del directorio de configuración {#configuration-directory-structure}

Adobe Access Server para la transmisión protegida requiere dos tipos de archivos de configuración: un archivo de configuración global (flashaccess-global.xml) y un archivo de configuración de inquilino para cada inquilino (flashaccess-tenant.xml).

Después de editar los archivos de configuración, Adobe recomienda utilizar las utilidades proporcionadas con Adobe Access Server para la transmisión protegida para comprobar que los archivos están bien formados. Para obtener más información, consulte &quot;[Validador de configuración](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

Para evitar que las contraseñas estén disponibles en texto claro en los archivos de configuración, todas las contraseñas especificadas en los archivos de configuración global e inquilino deben cifrarse. Para obtener más información sobre el cifrado de contraseñas, consulte &quot;[Contraseña Scrambler](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/password-scrambler.md)&quot;.

Los directorios de configuración tienen la siguiente estructura:

```
<i class="+ topic ph hi-d="" i "="">
  LicenseServer.ConfigRoot/  
  flashaccess-global.xml  
  pkcs11.cfg (optional)  
  flashaccessserver/  
   libs/ (optional)  
   tenants/  
     
 <i class="+ topic ph hi-d="" i "="">
   tenantname/  
      flashaccess-tenant.xml  
       
  <i class="+ topic ph hi-d="" i "="">
    credential.pfx (optional)  
        
   <i class="+ topic ph hi-d="" i "="">
     packagercert.cer (optional) 
   </i class="+ topic> 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

