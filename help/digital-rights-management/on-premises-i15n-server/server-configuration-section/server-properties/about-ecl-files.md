---
title: Acerca de los archivos ECI
description: Acerca de los archivos ECI
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# Acerca de los archivos ECI{#about-eci-files}

Además de las listas CRL, también debe actualizar periódicamente los archivos de la interfaz común integrada (ECI). Siempre que el Adobe añada compatibilidad con una nueva plataforma de cliente de Primetime DRM (por ejemplo: iOS, Android, Windows FlashPlayer, etc.), se crea un nuevo registro ECI. Para poder admitir la individualización de este cliente, es necesario que haya un registro ECI correspondiente en el servidor de individualización.

Dado que el lanzamiento de nuevos clientes de DRM de Primetime no es muy frecuente, el Adobe publicará los datos de ECI actualizados según sea necesario. Periódicamente, los Adobes recopilarán archivos ECI y los alojarán en la siguiente ubicación para su distribución:

```
http://cdmdownload.adobe.com/indiv/onprem/eci/Latest.txt
```

El archivo [!DNL Latest.txt] contendrá la dirección URL del archivo de distribución CRL más reciente.

Adobe creará el archivo zip ECI de la manera descrita a continuación:

Estructura de carpetas:

```
ECI\*
```

El contenido de la carpeta se comprimirá varias veces:

```
zip -R ECI ECI.zip
```

Se calculará un compendio OpenSSL SHA-256 del archivo zip:

```
openssl dgst -sha256 -hex ECI.zip
```

Se cambiará el nombre del archivo zip para que contenga la fecha del archivo, así como el compendio SHA-256:

```
Rename ECI.zip to <DATE_SHA-256>.zip
```

Por ejemplo:

```
20150310_aea45bf06241f04fba2b310ff9a8066c6aba73c8d22387b60509481e9cefc43e.zip
```

Debe comprobar periódicamente la ubicación anterior para consultar los archivos ECI actualizados.

Realice el siguiente proceso de instalación después de la descarga:

1. Observe el compendio SHA-256 y vuelva a calcularlo usando OpenSSL o una herramienta equivalente.
1. Compare todo con el especificado en el nombre del archivo.
1. Cambie el nombre del archivo a [!DNL ECI.zip].
1. Descomprima el directorio [!DNL ECI].
1. Sustituya el antiguo directorio ECI por el nuevo.
1. Reinicie el servidor de Individualización.

