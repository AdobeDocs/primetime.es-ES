---
description: El Adobe recomienda que, si se realizan cambios en el archivo de configuración, se ejecute el Validador de configuración antes de iniciar el servidor. Esta utilidad puede detectar la mayoría de los errores de configuración de forma temprana, antes de que causen errores durante el procesamiento de la solicitud.
title: Validador de configuración
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Validador de configuración{#configuration-validator}

El Adobe recomienda que, si se realizan cambios en el archivo de configuración, se ejecute el Validador de configuración antes de iniciar el servidor. Esta utilidad puede detectar la mayoría de los errores de configuración de forma temprana, antes de que causen errores durante el procesamiento de la solicitud.

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

Para cada uno de los archivos de configuración del servidor de licencias, el validador puede realizar una validación basada en archivos, lo que garantiza que el archivo XML tenga el formato correcto y se ajuste al esquema del archivo de configuración.

Para realizar la validación basada en archivos en el archivo de configuración global, escriba:

```
Validator --<file path>/flashaccess-global.xml --global
```

Para realizar la validación basada en archivos en el archivo de configuración del inquilino, escriba:

```
Validator --<file path>/flashaccess-tenant.xml --tenant
```

El validador también puede realizar una validación basada en la implementación. Además de comprobar la conformidad con el esquema, este nivel de validación también comprueba que los valores especificados son válidos. Por ejemplo, garantiza que existan archivos a los que se hace referencia.

La validación basada en la implementación se puede realizar en los siguientes niveles:

* `Tenant` — Valida el archivo de configuración y las credenciales de un inquilino específico. Si desea validar la configuración de `<tenant1>`, escriba:

  ```
      Validator --<root-path-to-LicenseServer.ConfigRoot> -d flashaccessserver/tenant1 -t
  ```

* `Global` — valida el archivo de configuración global y la validación del inquilino para todos los inquilinos. Si desea realizar una validación basada en la implementación global, escriba:

  ```
      Validator --<root-path-to-LicenseServer.ConfigRoot> -g
  ```
