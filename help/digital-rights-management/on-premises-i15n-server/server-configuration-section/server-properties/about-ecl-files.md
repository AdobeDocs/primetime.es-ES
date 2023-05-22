---
title: Acerca de los archivos ECI
description: Acerca de los archivos ECI
copied-description: true
exl-id: ac452897-3c64-4481-a3b7-4b69ef6edb61
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Acerca de los archivos ECI{#about-eci-files}

Además de las listas CRL, también debe actualizar periódicamente los archivos de la Interfaz común incrustada (ECI). Cada vez que Adobe agrega compatibilidad con una nueva plataforma de cliente DRM de Primetime (por ejemplo: iOS, Android, Windows FlashPlayer, etc.), se crea un nuevo registro de ECI. Para admitir la individualización de este cliente, debe estar presente un registro ECI correspondiente en el servidor de individualización.

Dado que el lanzamiento de nuevos clientes de DRM de Primetime no es muy frecuente, el Adobe lanzará datos de ECI actualizados según sea necesario. Periódicamente, el Adobe recopilará archivos ECI y los alojará en la siguiente ubicación para su distribución:

```
http://cdmdownload.adobe.com/indiv/onprem/eci/Latest.txt
```

El [!DNL Latest.txt] contendrá la dirección URL del archivo de distribución de CRL más reciente.

Adobe creará el archivo zip de ECI de la manera que se describe a continuación:

Estructura de carpetas:

```
ECI\*
```

El contenido de la carpeta se comprimirá de forma recursiva:

```
zip -R ECI ECI.zip
```

Se calculará un compendio SHA-256 de OpenSSL del archivo zip:

```
openssl dgst -sha256 -hex ECI.zip
```

Se cambiará el nombre del archivo zip para que contenga la fecha del archivo y el compendio SHA-256:

```
Rename ECI.zip to <DATE_SHA-256>.zip
```

Por ejemplo:

```
20150310_aea45bf06241f04fba2b310ff9a8066c6aba73c8d22387b60509481e9cefc43e.zip
```

Debe comprobar periódicamente la ubicación anterior para ver si hay archivos ECI actualizados.

Realice el siguiente proceso para la instalación después de la descarga:

1. Observe el compendio SHA-256 y vuelva a calcularlo con OpenSSL o una herramienta equivalente.
1. Compárela con la especificada en el nombre del archivo.
1. Cambie el nombre del archivo a [!DNL ECI.zip].
1. Descomprima el [!DNL ECI] directorio.
1. Reemplace el directorio ECI antiguo por el nuevo.
1. Reinicie el servidor de individualización.
