---
description: Adobe recomienda que, si realiza cambios en el archivo de configuración, ejecute la utilidad Validador de configuración antes de iniciar el servidor. Esta utilidad puede detectar la mayoría de los errores de configuración antes de que causen errores durante el procesamiento de la solicitud.
title: Validador de configuración
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Validador de configuración{#configuration-validator}

Adobe recomienda que, si realiza cambios en el archivo de configuración, ejecute la utilidad Validador de configuración antes de iniciar el servidor. Esta utilidad puede detectar la mayoría de los errores de configuración antes de que causen errores durante el procesamiento de la solicitud.

Para ejecutar el validador, escriba:

```
Validator.bat  
<i class="+ topic ph hi-d="" i "="">
  options  
</i class="+ topic>
```

o

```
java -jar libs/flashaccess-validator.jar  
<i class="+ topic ph hi-d="" i "="">
  options 
</i class="+ topic>
```

Para cada uno de los archivos de configuración del servidor de licencias, el Validador puede realizar una validación basada en archivos, lo que garantiza que el archivo XML esté bien formado y se ajuste al esquema del archivo de configuración.

Para realizar una validación basada en archivos en el archivo de configuración global, escriba:

```
Validator --<file path>/flashaccess-global.xml --global
```

Para realizar una validación basada en archivos en el archivo de configuración del inquilino, escriba:

```
Validator --<file path>/flashaccess-tenant.xml --tenant
```

El validador también puede realizar una validación basada en la implementación. Además de comprobar la conformidad con el esquema, este nivel de validación también verifica que los valores especificados sean válidos. Por ejemplo, garantiza que existan archivos a los que se hace referencia.

La validación basada en la implementación se puede realizar en los siguientes niveles:

* `Tenant` — Valida el archivo de configuración y las credenciales de un inquilino específico. Si desea validar la configuración para `<tenant1>`, escriba:

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -d flashaccessserver/tenant1 -t
   ```

* `Global` — Valida el archivo de configuración global y la validación de inquilinos para todos los inquilinos. Si desea realizar una validación global basada en la implementación, escriba:

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -g
   ```

