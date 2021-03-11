---
description: Los archivos de registro generados por la aplicación Adobe Primetime DRM Server para la transmisión protegida se encuentran en el directorio especificado por LicenseServer.LogRoot.
title: Archivos de registro
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# Archivos de registro{#log-files}

Los archivos de registro generados por la aplicación Adobe Primetime DRM Server para la transmisión protegida se encuentran en el directorio especificado por LicenseServer.LogRoot.

>[!NOTE]
>
>Si los archivos de registro actuales se eliminan o mueven mientras el servidor se ejecuta, es posible que el archivo de registro no se vuelva a crear. Por lo tanto, se puede eliminar parte de la información de registro.

## Estructura del directorio de registro {#section_F490A483D60145ADBC21038914C39203}

Los directorios de registro están estructurados para facilitar su uso. El directorio de registro tiene la siguiente estructura:

```
<i class="+ topic ph hi-d="" i "="">
 LicenseServer.LogRoot/ 
 flashaccess-global.log 
     flashaccessserver/ 
         flashaccess-partition.log 
         tenants/ 
             
 <i class="+ topic ph hi-d="" i "="">
  tenantname/ 
                  flashaccess-tenant.log
 </i class="+ topic>
</i class="+ topic>
```

## Archivo de registro global {#section_1CFA90748142439C9F3BE380969539DA}

El archivo de registro global, `flashaccess-global.log`, se encuentra en *LicenseServer.LogRoot*. El registro puede incluir mensajes de registro que el SDK de Java de Adobe Primetime DRM o los mensajes de registro pueden haber generado durante el tiempo en que se ha inicializado el servidor.

## Archivo de registro de partición {#section_5660137CD6AA40519E72A4315534846B}

El archivo de registro de partición, `flashaccess-partition.log`, se encuentra en el directorio `<LicenseServer.LogRoot>/flashaccesserver`. Incluye mensajes de registro que se han generado durante el procesamiento de una solicitud de licencia.

## Archivo de registro del inquilino {#section_F0257CC0831647F18A746B4F02E3E910}

El archivo de registro de inquilino de cada inquilino, `flashaccess-tenant.log`, se encuentra en `<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`. El registro de inquilino incluye información de auditoría que describe cada licencia generada para este inquilino.
