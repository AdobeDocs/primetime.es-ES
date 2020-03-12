---
description: 'Adobe Access Server for Protected Streaming requiere dos tipos de archivos de configuración: un archivo de configuración global (flashaccess-global.xml) y un archivo de configuración de inquilino para cada inquilino (flashaccess-inquilino.xml).'
seo-description: 'Adobe Access Server for Protected Streaming requiere dos tipos de archivos de configuración: un archivo de configuración global (flashaccess-global.xml) y un archivo de configuración de inquilino para cada inquilino (flashaccess-inquilino.xml).'
seo-title: Estructura del directorio de configuración
title: Estructura del directorio de configuración
uuid: c6cfc734-6b7c-4502-9bdb-c7aaca156e0e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Archivos de configuración del servidor de licencias y estructura del directorio de configuración {#configuration-directory-structure}

Adobe Access Server for Protected Streaming requiere dos tipos de archivos de configuración: un archivo de configuración global (flashaccess-global.xml) y un archivo de configuración de inquilino para cada inquilino (flashaccess-inquilino.xml).

Después de editar los archivos de configuración, Adobe recomienda utilizar las utilidades proporcionadas con Adobe Access Server para el flujo protegido para comprobar que los archivos están bien formados. Para obtener más información, consulte &quot;Validador[de configuración](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

Para evitar que las contraseñas estén disponibles en texto sin formato en los archivos de configuración, todas las contraseñas especificadas en los archivos de configuración global e inquilino deben estar cifradas. Para obtener más información sobre la codificación de contraseñas, consulte &quot;[Password Scrambler](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/password-scrambler.md)&quot;.

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

