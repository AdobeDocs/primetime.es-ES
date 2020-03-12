---
title: Versiones de Primetime Offline Packager 2.x
seo-title: Versiones de Primetime Offline Packager 2.x
description: Novedades de las versiones 2.1 y 2.3.1 de Primetime Offline Packager
seo-description: Novedades de las versiones 2.1 y 2.3.1 de Primetime Offline Packager
uuid: 01926a10-890d-477d-b832-e22847d957e0
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: 933a0711-846a-4bb7-bf51-b300822a93d4
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# Versiones de Primetime Offline Packager {#primetime-offline-packager-x-releases}

Novedades de las versiones 2.1 y 2.3.1 de Primetime Offline Packager

## Novedades de Primetime Offline Packager 2.3.1 (octubre de 2016) {#what-s-new-in-primetime-offline-packager-oct}

La versión habilita el perfil bajo demanda para MPEG-DASH, añade compatibilidad con la `validate` opción de la herramienta PlaylistCreator y tiene pocas correcciones clave para los escenarios de Multi-DRM que se indican a continuación.

| **Número de problema** | **Descripción** |
|---|---|
| PTPUB-985 | HLS AAXS y Sample-AES no funcionan para la clave generada por el empaquetador |
| PTPUB-973 | Se corrigió un error en el algoritmo de codificación para contenido específico de Widevine |
| PTPUB-964 | Cifrado de CENC dañado para determinados tipos de medios en un reproductor determinado: Android TVSDK. |
| PTPUB-954 | El cifrado AES de muestra evita el DRM AAXS de forma predeterminada / Error generado con la entrega de clave remota habilitada. |
| PTPUB-951 | El empaquetador sin conexión no emite una excepción cuando key_file_path no se especifica con Widevine. En cambio, lanza NPE. |

La documentación más reciente de Primetime Packagers está disponible en [https://help.adobe.com/en_US/primetime/api/packagers/index.html](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

### Problema conocido en la versión 2.3.1 {#known-issue-in-version}

Esta versión presenta los siguientes problemas.

| **Número de problema** | **Descripción** |
|---|---|
| PTPUB-1005 | PlaylistCreator no proporciona la dirección URL correcta para el archivo .pssh en el último archivo .mpd de nivel de conjunto generado para el DRM AAXS. |
| PTPUB-1001 | PlaylistCreator debe generar un error cuando se proporciona una ruta vacía mediante el parámetro in_path |
| PTPUB-990 | Para DASH, Offline Packager no escribe en el disco IV generado por el empaquetador cuando se especifican los parámetros `log_vi` &amp; `iv_out_path` . |
| PTPUB-980 | Cuando se utiliza el archivo de configuración para empaquetar, el uso del parámetro `key_url` no elimina las comillas de las entradas proporcionadas. |

## Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager}

### Requisitos mínimos del sistema {#minimum-system-requirements}

Sistemas operativos admitidos

* Linux CentOS 6.3 de 64 bits

Requisitos de hardware

* Procesador Intel® Pentium® 4 de 3,2 GHz (se recomienda doble Intel Xeon® o más rápido)

* Sistemas operativos de 64 bits: 4 GB de RAM (se recomiendan 8 GB)

* Disco duro

(Disk-SAS): Mínimo de 10 GB con 7.500 RPM

(Disco-SSD): Velocidad de lectura y escritura de 400 MBps

(NAS): Vínculo dedicado de 1 GB

Requisitos de software

* Oracle Java SE 1.8 o superior

### Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager-1}

1. Descargue el software Java SE del sitio [de](https://www.oracle.com/technetwork/java/javase/downloads/index.html) Oracle y siga las instrucciones de instalación.
1. Extraiga el archivo de archivo de Adobe Primetime Offline Packager 2.3.1 con el nombre `PrimetimeOfflinePackager-2-3-1-b47-10142016.zip` del disco.

### Configuración de Offline Packager 2.3.1 {#configuring-the-offline-packager}

Las instrucciones de configuración están disponibles en la guía Primetime Offline Packager Getting Started (Introducción a Paquetes sin conexión de Primetime) en [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Novedades de Primetime Offline Packager 2.1 (julio de 2015) {#what-s-new-in-primetime-offline-packager-july}

Compatibilidad con PlayReady BuyDRM (para DASH). Para obtener más información, consulte la documentación de ayuda [disponible aquí](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

También se realizó la siguiente mejora en el empaquetador sin conexión.

PTPUB-780 Se agregó compatibilidad con la etiqueta EXT-X-START

## Novedades de Primetime Offline Packager 2.0 (junio de 2015) {#what-s-new-in-primetime-offline-packager-june}

Se ha agregado la compatibilidad con la salida de borrado DASH. Consulte la documentación del producto [aquí](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html) para obtener más información.

En esta versión también se han solucionado los problemas siguientes.

* PTPUB-783 Offline Packager ahora puede gestionar archivos WebVTT vacíos.
* PTPUB- 781 Artefactos en la salida HLS en Chrome cuando ciertos recursos MP4 transcodificados se empaquetan con un empaquetador sin conexión para producir salida MBR.

## Adobe Primetime Offline Packager 2.1 {#adobe-primetime-offline-packager-2}

### Requisitos mínimos del sistema {#minimum-system-requirements-1}

**Sistemas operativos admitidos**

* Linux CentOS 6.3 de 64 bits

**Requisitos de hardware**

* Procesador Intel® Pentium® 4 de 3,2 GHz (se recomienda doble Intel Xeon® o más rápido)

* Sistemas operativos de 64 bits: 4 GB de RAM (se recomiendan 8 GB)

* Se recomienda una tarjeta Ethernet de 1 Gb (se admiten varias tarjetas de red y 10 Gb)

* Disco duro

   * (Disk-SAS): Mínimo de 10 GB con 7.500 RPM
   * (Disco-SSD): Velocidad de lectura y escritura de 400 MBps
   * (NAS): Vínculo dedicado de 1 GB

**Requisitos de software**

* Oracle Java SE 1.8 o superior

### Instalación de Offline Packager 2.1 {#installing-offline-packager}

1. Descargue el software Java SE del sitio [de](https://www.oracle.com/technetwork/java/javase/downloads/index.html) Oracle y siga las instrucciones de instalación.
1. Extraiga el `Adobe Primetime - Offline Packager 2.1.0 archive file, PrimetimeOfflinePackager-2-1-0-b15-07082015.zip`, en el disco.

### Configuración de Offline Packager 2.1 {#configuring-the-offline-packager-1}

Consulte el documento Primetime Offline Packager Getting Started para obtener los detalles de configuración disponibles aquí [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en la página de información y asistencia [de](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.