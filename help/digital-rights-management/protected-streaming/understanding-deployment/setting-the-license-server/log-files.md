---
description: Los archivos de registro generados por la aplicación Adobe Primetime DRM Server for Protected Streaming se encuentran en el directorio especificado por LicenseServer.LogRoot.
seo-description: Los archivos de registro generados por la aplicación Adobe Primetime DRM Server for Protected Streaming se encuentran en el directorio especificado por LicenseServer.LogRoot.
seo-title: Archivos de registro
title: Archivos de registro
uuid: 4498fe60-65af-4f99-8f9b-e85013d0c9e9
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---


# Archivos de registro{#log-files}

Los archivos de registro generados por la aplicación Adobe Primetime DRM Server for Protected Streaming se encuentran en el directorio especificado por LicenseServer.LogRoot.

>[!NOTE]
>
>Si los archivos de registro actuales se eliminan o mueven mientras se ejecuta el servidor, es posible que no se vuelva a crear el archivo de registro. Por lo tanto, se puede eliminar parte de la información de registro.

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

El archivo de registro global, [!DNL flashaccess-global.log], se encuentra en *LicenseServer.LogRoot*. El registro puede incluir mensajes de registro que el SDK de Java de Adobe Primetime DRM o los mensajes de registro pueden haber generado durante el tiempo en que se inicializó el servidor.

## Archivo de registro de partición {#section_5660137CD6AA40519E72A4315534846B}

El archivo de registro de partición, [!DNL flashaccess-partition.log], se encuentra en el [!DNL <LicenseServer.LogRoot>/flashaccesserver] directorio. Incluye los mensajes de registro que se han generado durante el procesamiento de una solicitud de licencia.

## Archivo de registro del inquilino {#section_F0257CC0831647F18A746B4F02E3E910}

El archivo de registro de inquilinos de cada inquilino, [!DNL flashaccess-tenant.log], se encuentra en [!DNL &lt;LicenseServer.LogRoot>/flashaccesserver/inants/<tenantname>]. El registro de inquilinos incluye información de auditoría que describe cada licencia que se genera para este inquilino.
