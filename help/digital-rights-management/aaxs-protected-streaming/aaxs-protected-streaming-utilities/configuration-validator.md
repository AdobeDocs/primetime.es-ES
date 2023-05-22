---
title: Validador de configuración
description: Validador de configuración
copied-description: true
exl-id: 9b73e107-6ab7-4089-b415-0af8c9f86995
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# Validador de configuración {#configuration-validator}

Adobe recomienda ejecutar la utilidad Validador de configuración antes de iniciar el servidor cada vez que se realicen cambios en el archivo de configuración. Esta utilidad puede detectar la mayoría de los errores de configuración de forma temprana, antes de que causen errores durante el procesamiento de la solicitud.

Para ejecutar el validador, utilice el comando:

```
Validator.bat options  
```

o el comando:

```
java -jar libs/flashaccess-validator.jar options 
```

Para cada uno de los archivos de configuración del servidor de licencias, el validador puede realizar una validación basada en archivos, lo que garantiza que el archivo XML tenga el formato correcto y se ajuste al esquema del archivo de configuración. Para realizar la validación basada en archivos en el archivo de configuración global, ejecute el comando:

```
Validator --file path/flashaccess-global.xml --global
```

Para realizar la validación basada en archivos en el archivo de configuración del inquilino, ejecute el comando:

```
Validator --file path/flashaccess-tenant.xml --tenant
```

El validador también puede realizar una validación basada en la implementación; además de comprobar la conformidad con el esquema, este nivel de validación también comprueba que los valores especificados son válidos (por ejemplo, garantiza que existan archivos a los que se hace referencia). La validación basada en la implementación se puede realizar en dos niveles:

* Inquilino: valida el archivo de configuración y las credenciales de un inquilino específico. Para validar la configuración de &quot;tenant1&quot;, ejecute el comando:

```
Validator --root-path-to-LicenseServer.ConfigRoot -d flashaccessserver/tenant1 -t 
```

* Global: valida el archivo de configuración global y la validación del inquilino para todos los inquilinos. Para realizar una validación global basada en la implementación, ejecute el comando:

```
Validator --root-path-to-LicenseServer.ConfigRoot -g 
```
