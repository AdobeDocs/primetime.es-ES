---
description: 'Adobe Access Server para flujo protegido requiere dos tipos de archivos de configuración: un archivo de configuración global (flashaccess-global.xml) y un archivo de configuración de inquilino para cada inquilino (flashaccess-tenant.xml).'
title: Estructura del directorio de configuración
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# Archivos de configuración del servidor de licencias y estructura del directorio de configuración {#configuration-directory-structure}

Adobe Access Server para flujo protegido requiere dos tipos de archivos de configuración: un archivo de configuración global (flashaccess-global.xml) y un archivo de configuración de inquilino para cada inquilino (flashaccess-tenant.xml).

Después de editar los archivos de configuración, Adobe recomienda utilizar las utilidades proporcionadas con Adobe Access Server para flujo protegido para comprobar que los archivos tengan el formato correcto. Para obtener más información, consulte &quot;[Validador de configuración](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

Para evitar que las contraseñas estén disponibles en texto no cifrado en los archivos de configuración, todas las contraseñas especificadas en los archivos de configuración global e inquilino deben estar cifradas. Para obtener más información sobre el cifrado de contraseñas, consulte &quot;[Descodificador de contraseñas](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/password-scrambler.md)&quot;.

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
