---
title: Versiones de Primetime Offline Packager 2.x
description: Novedades de las versiones 2.1 y 2.3.1 de Primetime Offline Packager
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---


# Versiones de Primetime Offline Packager {#primetime-offline-packager-x-releases}

Novedades de las versiones 2.1 y 2.3.1 de Primetime Offline Packager

## Novedades de Primetime Offline Packager 2.3.1 (octubre de 2016) {#what-s-new-in-primetime-offline-packager-oct}

La versión habilita el Perfil bajo demanda para MPEG-DASH, agrega compatibilidad con la opción `validate` de la herramienta PlaylistCreator y tiene pocas correcciones clave para los escenarios Multi-DRM que se enumeran a continuación.

| **Número de problema** | **Descripción** |
|---|---|
| PTPUB-985 | HLS AAXS y Sample-AES no funcionan para la clave generada por el empaquetador |
| PTPUB-973 | Se ha corregido un error en el algoritmo de cifrado para algunos contenidos de Widevine específicos |
| PTPUB-964 | Se ha interrumpido el cifrado CENC para determinados tipos de medios en ciertos reproductores: Android TVSDK. |
| PTPUB-954 | El cifrado AES de muestra evita AAXS DRM de forma predeterminada/Error generado con la entrega de claves remotas habilitada. |
| PTPUB-951 | El empaquetador sin conexión no genera una excepción cuando key_file_path no se especifica con Widevine. En su lugar, lanza NPE. |

La documentación más reciente de Primetime Packagers está disponible en [https://help.adobe.com/en_US/primetime/api/packagers/index.html](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

### Problema conocido en la versión 2.3.1 {#known-issue-in-version}

Los siguientes problemas existen en esta versión.

| **Número de problema** | **Descripción** |
|---|---|
| PTPUB-1005 | PlaylistCreator no proporciona la dirección URL correcta para el archivo .pssh en el último archivo .mpd de nivel de conjunto generado para el DRM AAXS. |
| PTPUB-1001 | PlaylistCreator debe generar un error cuando se proporciona una ruta vacía mediante el parámetro in_path |
| PTPUB-990 | Para DASH, Offline Packager no escribe el empaquetador generado IV en el disco cuando se especifican los parámetros `log_vi` y `iv_out_path`. |
| PTPUB-980 | Cuando se utiliza el archivo de configuración para empaquetar, el uso del parámetro `key_url` no elimina las comillas de las entradas proporcionadas. |

## Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager}

### Requisitos mínimos del sistema {#minimum-system-requirements}

Sistemas operativos compatibles

* Linux CentOS 6.3 de 64 bits

Requisitos de hardware

* Procesador Intel® Pentium® 4 a 3,2 GHz (se recomienda el procesador Intel Xeon® dual o más rápido)

* Sistemas operativos de 64 bits: 4 GB de RAM (se recomiendan 8 GB)

* Disco duro

(Disk-SAS): Mínimo de 10 GB con 7.500 RPM

(Disco-SSD): Velocidad de lectura/escritura de 400 MBps

(NAS): Vínculo dedicado de 1 GB

Requisitos de software

* Oracle Java SE 1.8 o superior

### Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager-1}

1. Descargue el software Java SE del [sitio de Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) y siga las instrucciones de instalación.
1. Extraiga el archivo de Adobe Primetime Offline Packager 2.3.1 llamado `PrimetimeOfflinePackager-2-3-1-b47-10142016.zip` al disco.

### Configuración de Offline Packager 2.3.1 {#configuring-the-offline-packager}

Las instrucciones de configuración están disponibles en la guía de introducción a Paquetes sin conexión de Primetime en [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Novedades de Primetime Offline Packager 2.1 (julio de 2015) {#what-s-new-in-primetime-offline-packager-july}

Compatibilidad con PlayReady BuyDRM (para DASH). Para obtener más información, consulte la documentación de ayuda [disponible aquí](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

También se realizó la siguiente mejora en el empaquetador sin conexión.

PTPUB-780 Se ha agregado compatibilidad con la etiqueta EXT-X-START

## Novedades de Primetime Offline Packager 2.0 (junio de 2015) {#what-s-new-in-primetime-offline-packager-june}

Se ha añadido la compatibilidad con la salida Clear DASH. Consulte la documentación del producto [aquí](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html) para obtener más información.

En esta versión también se corrigieron los siguientes problemas.

* PTPUB-783 Offline Packager ahora puede gestionar archivos WebVTT vacíos.
* PTPUB-781 Artefactos en la salida HLS en Chrome cuando ciertos activos MP4 transcodificados están empaquetados con un empaquetador sin conexión para producir resultados MBR.

## Adobe Primetime Offline Packager 2.1 {#adobe-primetime-offline-packager-2}

### Requisitos mínimos del sistema {#minimum-system-requirements-1}

**Sistemas operativos compatibles**

* Linux CentOS 6.3 de 64 bits

**Requisitos de hardware**

* Procesador Intel® Pentium® 4 a 3,2 GHz (se recomienda el procesador Intel Xeon® dual o más rápido)

* Sistemas operativos de 64 bits: 4 GB de RAM (se recomiendan 8 GB)

* Tarjeta Ethernet de 1 Gb recomendada (también se admiten varias tarjetas de red y 10 Gb)

* Disco duro

   * (Disk-SAS): Mínimo de 10 GB con 7.500 RPM
   * (Disco-SSD): Velocidad de lectura/escritura de 400 MBps
   * (NAS): Vínculo dedicado de 1 GB

**Requisitos de software**

* Oracle Java SE 1.8 o superior

### Instalación de Offline Packager 2.1 {#installing-offline-packager}

1. Descargue el software Java SE del [sitio de Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) y siga las instrucciones de instalación.
1. Extraiga el `Adobe Primetime - Offline Packager 2.1.0 archive file, PrimetimeOfflinePackager-2-1-0-b15-07082015.zip` en su disco.

### Configuración de Offline Packager 2.1 {#configuring-the-offline-packager-1}

Consulte el documento Introducción a Paquetes sin conexión de Primetime para obtener más información sobre la configuración disponible aquí [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en la página [Aprendizaje y asistencia de Adobe Primetime](https://helpx.adobe.com/support/primetime.html).