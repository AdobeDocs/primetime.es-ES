---
description: Adobe recomienda que, si realiza cambios en el archivo de configuración, ejecute la utilidad Validador de configuración antes de iniciar el servidor. Esta utilidad puede detectar la mayoría de los errores de configuración antes de que se produzcan errores durante el procesamiento de la solicitud.
seo-description: Adobe recomienda que, si realiza cambios en el archivo de configuración, ejecute la utilidad Validador de configuración antes de iniciar el servidor. Esta utilidad puede detectar la mayoría de los errores de configuración antes de que se produzcan errores durante el procesamiento de la solicitud.
seo-title: Validador de configuración
title: Validador de configuración
uuid: 7b44919a-0319-4675-95e2-ad1ad72ec0cb
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Validador de configuración{#configuration-validator}

Adobe recomienda que, si realiza cambios en el archivo de configuración, ejecute la utilidad Validador de configuración antes de iniciar el servidor. Esta utilidad puede detectar la mayoría de los errores de configuración antes de que se produzcan errores durante el procesamiento de la solicitud.

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

Para cada uno de los archivos de configuración del servidor de licencias, el validador puede realizar una validación basada en archivos, lo que garantiza que el archivo XML esté bien formado y se ajuste al esquema del archivo de configuración.

Para realizar una validación basada en archivos en el archivo de configuración global, escriba:

```
Validator --<file path>/flashaccess-global.xml --global
```

Para realizar una validación basada en archivos en el archivo de configuración del inquilino, escriba:

```
Validator --<file path>/flashaccess-tenant.xml --tenant
```

El validador también puede realizar una validación basada en la implementación. Además de comprobar la conformidad con el esquema, este nivel de validación también comprueba que los valores especificados son válidos. Por ejemplo, garantiza la existencia de los archivos a los que se hace referencia.

La validación basada en la implementación se puede realizar en los siguientes niveles:

* `Tenant` — Valida el archivo de configuración y las credenciales de un inquilino específico. Si desea validar la configuración para `<tenant1>`, escriba:

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -d flashaccessserver/tenant1 -t
   ```

* `Global` — Valida el archivo de configuración global y la validación del inquilino para todos los inquilinos. Si desea realizar una validación global basada en la implementación, escriba:

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -g
   ```

