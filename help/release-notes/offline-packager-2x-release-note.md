---
title: Versiones de Primetime Offline Packager 2.x
description: Novedades de las versiones 2.1 y 2.3.1 de Primetime Offline Packager
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---

# Versiones de Primetime Offline Packager {#primetime-offline-packager-x-releases}

Novedades de las versiones 2.1 y 2.3.1 de Primetime Offline Packager

## Novedades de Primetime Offline Packager 2.3.1 (octubre de 2016)  {#what-s-new-in-primetime-offline-packager-oct}

La versión permite On-demand Profile para MPEG-DASH, añade compatibilidad con el `validate` para la herramienta PlaylistCreator y tiene algunas correcciones clave para los escenarios de Multi-DRM que se enumeran a continuación.

| **Número de problema** | **Descripción** |
|---|---|
| PTPUB-985 | AXS de HLS y Sample-AES no funcionan para claves generadas por el empaquetador |
| PTPUB-973 | Se ha corregido un error en el algoritmo de cifrado para algunos contenidos específicos de Widevine |
| PTPUB-964 | El cifrado CENC está dañado para ciertos tipos de medios en ciertos reproductores: Android TVSDK. |
| PTPUB-954 | El cifrado AES de muestra omite AXS DRM de forma predeterminada/Se produjo un error con la entrega de claves remotas habilitada. |
| PTPUB-951 | El empaquetador sin conexión no genera excepciones cuando key_file_path no se especifica con Widevine. En su lugar lanza NPE. |

La documentación más reciente de los paquetes de Primetime está disponible en [https://help.adobe.com/en_US/primetime/api/packagers/index.html](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

### Problema conocido en la versión 2.3.1 {#known-issue-in-version}

En esta versión existen los siguientes problemas.

| **Número de problema** | **Descripción** |
|---|---|
| PTPUB-1005 | PlaylistCreator no proporciona la dirección URL correcta para el archivo .pssh en el archivo .mpd de nivel de conjunto final generado para la DRM de AXS. |
| PTPUB-1001 | PlaylistCreator debería generar un error cuando se proporciona una ruta vacía a través del parámetro in_path |
| PTPUB-990 | Para DASH, el empaquetador sin conexión no escribe el empaquetador IV generado en el disco cuando los parámetros `log_vi` &amp; `iv_out_path` se han especificado. |
| PTPUB-980 | Cuando se utiliza el archivo de configuración para el empaquetado, se utiliza el parámetro `key_url` no quita las comillas de las entradas proporcionadas. |

## Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager}

### Requisitos mínimos del sistema {#minimum-system-requirements}

Sistemas operativos compatibles

* Linux CentOS 6.3 de 64 bits

Requisitos de hardware

* Procesador Intel® Pentium® 4 a 3,2 GHz (se recomienda dual Intel Xeon® o más rápido)

* Sistemas operativos de 64 bits: 4 GB de RAM (se recomienda 8 GB)

* Disco duro

(Disco SAS): Mínimo de 10 GB a 7.500 rpm

(Disco SSD): Velocidad de lectura/escritura de 400 MBps

(NAS): Vínculo dedicado de 1 GB

Requisitos de software

* Oracle Java SE 1.8 o superior

### Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager-1}

1. Descargue el software Java SE desde el [sitio de oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) y siga las instrucciones de instalación.
1. Extraiga el archivo de Adobe Primetime Offline Packager 2.3.1 llamado `PrimetimeOfflinePackager-2-3-1-b47-10142016.zip` al disco.

### Configuración del empaquetador sin conexión 2.3.1 {#configuring-the-offline-packager}

Las instrucciones de configuración están disponibles en la guía de Introducción al empaquetador sin conexión de Primetime en [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Novedades de Primetime Offline Packager 2.1 (julio de 2015) {#what-s-new-in-primetime-offline-packager-july}

Soporte para PlayReady BuyDRM (para DASH). Para obtener más información, consulte la documentación de ayuda de [disponible aquí](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

También se realizó la siguiente mejora en el empaquetador sin conexión.

PTPUB-780 Se ha agregado compatibilidad con la etiqueta EXT-X-START

## Novedades de Primetime Offline Packager 2.0 (junio de 2015) {#what-s-new-in-primetime-offline-packager-june}

Se ha añadido la compatibilidad con la salida Clear DASH. Consulte la documentación del producto [aquí](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html) para obtener más información.

Los siguientes problemas también se solucionaron en esta versión.

* El empaquetador sin conexión PTPUB-783 ahora puede administrar archivos WebVTT vacíos.
* PTPUB- 781 Artefactos en la salida HLS en Chrome cuando ciertos recursos MP4 transcodificados están empaquetados con el empaquetador sin conexión para producir la salida MBR.

## Adobe Primetime Offline Packager 2.1 {#adobe-primetime-offline-packager-2}

### Requisitos mínimos del sistema {#minimum-system-requirements-1}

**Sistemas operativos compatibles**

* Linux CentOS 6.3 de 64 bits

**Requisitos de hardware**

* Procesador Intel® Pentium® 4 a 3,2 GHz (se recomienda dual Intel Xeon® o más rápido)

* Sistemas operativos de 64 bits: 4 GB de RAM (se recomienda 8 GB)

* Tarjeta 1 Gb Ethernet recomendada (también admite varias tarjetas de red y 10 Gb)

* Disco duro

   * (Disco SAS): Mínimo de 10 GB a 7.500 rpm
   * (Disco SSD): Velocidad de lectura/escritura de 400 MBps
   * (NAS): Vínculo dedicado de 1 GB

**Requisitos de software**

* Oracle Java SE 1.8 o superior

### Instalación de Offline Packager 2.1 {#installing-offline-packager}

1. Descargue el software Java SE desde el [sitio de oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) y siga las instrucciones de instalación.
1. Extraiga el `Adobe Primetime - Offline Packager 2.1.0 archive file, PrimetimeOfflinePackager-2-1-0-b15-07082015.zip`, en el disco.

### Configuración del empaquetador sin conexión 2.1 {#configuring-the-offline-packager-1}

Consulte el documento Introducción al empaquetador sin conexión de Primetime para obtener los detalles de configuración disponibles aquí [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en [Formación y asistencia de Adobe Primetime](https://helpx.adobe.com/support/primetime.html) página.
