---
seo-title: Validador de configuración
title: Validador de configuración
uuid: 60ebd35c-290a-4f08-9bd0-178903857149
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# Validador de configuración {#configuration-validator}

Adobe recomienda que se ejecute la utilidad Configuration Validator antes de iniciar el servidor cuando se realicen cambios en el archivo de configuración. Esta utilidad puede detectar la mayoría de los errores de configuración antes de que se produzcan errores durante el procesamiento de la solicitud.

Para ejecutar el validador, utilice el comando:

```
Validator.bat options  
```

o el comando:

```
java -jar libs/flashaccess-validator.jar options 
```

Para cada uno de los archivos de configuración del servidor de licencias, el validador puede realizar una validación basada en archivos, lo que garantiza que el archivo XML esté bien formado y se ajuste al esquema del archivo de configuración. Para realizar una validación basada en archivos en el archivo de configuración global, ejecute el comando:

```
Validator --file path/flashaccess-global.xml --global
```

Para realizar una validación basada en archivos en el archivo de configuración del inquilino, ejecute el comando:

```
Validator --file path/flashaccess-tenant.xml --tenant
```

El validador también puede realizar una validación basada en la implementación; además de comprobar la conformidad con el esquema, este nivel de validación comprueba también que los valores especificados son válidos (por ejemplo, garantiza la existencia de los archivos a los que se hace referencia). La validación basada en la implementación se puede realizar en dos niveles:

* Inquilino — Valida el archivo de configuración y las credenciales de un inquilino específico. Para validar la configuración de &quot;inquilino1&quot;, ejecute el comando:

```
Validator --root-path-to-LicenseServer.ConfigRoot -d flashaccessserver/tenant1 -t 
```

* Global — Valida el archivo de configuración global y la validación del inquilino para todos los inquilinos. Para realizar una validación global basada en la implementación, ejecute el comando:

```
Validator --root-path-to-LicenseServer.ConfigRoot -g 
```

