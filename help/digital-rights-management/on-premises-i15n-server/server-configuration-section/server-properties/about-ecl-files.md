---
seo-title: Acerca de los archivos ECI
title: Acerca de los archivos ECI
uuid: 124d8ab1-933b-4a1b-992a-919f3d799460
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4

---


# Acerca de los archivos ECI{#about-eci-files}

Además de las CRL, también es necesario actualizar periódicamente los archivos de interfaz común integrada (ECI). Siempre que Adobe añada compatibilidad con una nueva plataforma de cliente Primetime DRM (por ejemplo: iOS, Android, Windows Flash Player, etc.), se crea un nuevo registro ECI. Para poder admitir la individualización de este cliente, debe estar presente un registro ECI correspondiente en el servidor de individualización.

Dado que el lanzamiento de nuevos clientes de DRM Primetime no es muy frecuente, Adobe lanzará los datos de ECI actualizados según sea necesario. De forma periódica, Adobe recopilará archivos ECI y los alojará en la siguiente ubicación para su distribución:

```
http://cdmdownload.adobe.com/indiv/onprem/eci/Latest.txt
```

El [!DNL Latest.txt] archivo contendrá la dirección URL del archivo de distribución CRL más reciente.

Adobe creará el archivo zip ECI de la manera que se describe a continuación:

Estructura de carpetas:

```
ECI\*
```

El contenido de la carpeta se comprimirá de forma recursiva:

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

Debe comprobar periódicamente la ubicación anterior para buscar archivos ECI actualizados.

Realice el siguiente proceso de instalación después de la descarga:

1. Observe el compendio SHA-256 y vuelva a calcularlo con OpenSSL o una herramienta equivalente.
1. Compárela con la especificada en el nombre del archivo.
1. Cambie el nombre del archivo a [!DNL ECI.zip].
1. Descomprima el [!DNL ECI] directorio.
1. Reemplace el directorio ECI antiguo por el nuevo.
1. Reinicie el servidor de individualización.

