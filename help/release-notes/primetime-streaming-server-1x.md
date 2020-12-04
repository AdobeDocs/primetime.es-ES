---
title: Versiones de Primetime Streaming Server
seo-title: Versiones de Primetime Streaming Server 1.x
description: Novedades de las versiones 1.3 y 1.4 de Primetime Streaming Server.
seo-description: Novedades de las versiones 1.3 y 1.4 de Primetime Streaming Server.
uuid: be05db6b-713f-4406-940d-9f3a805f967b
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: baec714e-9d41-4e8b-b134-13a736885cbd
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '1929'
ht-degree: 0%

---


# Versiones de Primetime Streaming Server {#primetime-streaming-server-x-releases}

Novedades de las versiones 1.3 y 1.4 de Primetime Streaming Server.

## Nuevo en Primetime Streaming Server 1.4 (versión de diciembre) {#what-s-new-in-primetime-streaming-server-december-release}

**Packager sin conexión**

* Los flujos HLS de salida ahora contienen metadatos ID3 presentes en MPEG-2 TS
* Los flujos solo de audio HLS ahora pueden tener una imagen estática asociada
* Compatibilidad para proporcionar IV como entrada de usuario para flujos de trabajo de cifrado HLS AES
* Compatibilidad con la salida IV a un archivo cuando el empaquetador sin conexión genera IV
* Playlist Creator ahora admite la asociación de grupos de audio en varios idiomas y grupos de subtítulos WebVTT en varios idiomas a flujos de medios

**Origen Server**

* El cifrado HLS AES está disponible para flujos de trabajo en directo y VOD. Primetime Origen puede aplicar codificación AES de HLS a flujos HLS entrantes o archivos MP4.
* También puede aplicar cifrado AES JIT HLS cuando se utiliza para convertir flujos entrantes de HDS a flujos HLS.
* El Origen Primetime ahora admite la inclusión de listas permitidas por SWF para flujos PHLS. Anteriormente, solo se admitía para flujos PHDS

**Primetime Live Packager**

* Compatibilidad para generar flujos HLS AES-128 para flujos RTMP de entrada y MPEG-2 TS

Se han actualizado los certificados PHDS/PHLS. La nueva fecha de caducidad será el 10/01/2016.

### **Corrección de errores incluida en la versión 1.4** {#bug-fixes-included-in-release}

* PTPUB-282- El manifiesto de nivel de conjunto HLS creado por OfflinePackager 1.3.1 no tiene información de códec y resolución.
* PTPUB-353 - PlayListCreator no admite la adición de información de WebVTT en el manifiesto de nivel establecido
* PTPUB-583 - La herramienta PlaylistCreator antepone inesperadamente los URI de grupo con.
* PTPUB-605 Playlist Creator no incluye el grupo de subtítulos en cada flujo de variante
* PTPUB-634 -Offline Packager agrega SpliceInsert al manifiesto.
* PTPUB-635- Se insertaron varias etiquetas SpliceOut para una sola señal de publicidad.

### Problema conocido en la versión 1.4 {#known-issue-in-release}

* PTPUB- 645 El modo DPISimple se fuerza incluso cuando se especifica el modo DPIScte35 cuando tanto las señales de línea de comandos como las señales en flujo se proporcionan en la configuración del empaquetador sin conexión

## Novedades de Primetime Streaming Server 1.3.1 (versión de MAYO) {#what-s-new-in-primetime-streaming-server-may-release}

La versión 1.3.1 hace referencia a la revisión. Las siguientes mejoras lo convierten en una actualización recomendada para los clientes, ya que consiste en mejoras de rendimiento clave para casos de uso de JIT MP4:

1. Corrección de rendimiento para la generación m3u8 de MP4 JIT en Origen con DRM, incluida la rotación de claves
1. Se ha añadido una configuración &quot;CopyQueryParamToJITFragmentURIs&quot; para copiar parámetros de consulta de una solicitud de manifiesto JIT a URI de fragmento generados para la conversión de JIT MP4. Consulte la documentación de HTTP Origen Server para obtener ejemplos de uso
1. Permitir archivos MP4 sin extensión para la conversión JIT, mediante la configuración Config/MP4Only agregada a vod.xml

### Correcciones de errores incluidas en la versión 1.3.1 {#bug-fixes-included-in-release-1}

* 3759167 - No todas las señales de SCTE35 llegan al manifiesto de salida debido a una anomalía de marca de tiempo durante el empaquetado. Aplique pt_Adjustment en SpliceTime en el mensaje TimeSignal de SpliceInfoSection de SCTE35.

### Problemas conocidos en la versión 1.3.1 {#known-issues-in-release}

* 3717039 - Cuando el empaquetador está configurado para producir señales de modo simple DPI, realmente debería estar buscando tipos de señal específicos, como oportunidades de inserción o colocación de empalme, y convirtiendo sólo esos datos en señales de modo simple. Debe ignorar otros tipos de señales como el inicio de programa, el inicio de red, etc.

* 3718598 - Cuando Origen Server está configurado para ofrecer contenido protegido con acceso HSM habilitado, el cliente LunaSA back-end realiza una comunicación frecuente con el módulo HSM

## Novedades de Primetime Streaming Server 1.3 (versión de ABRIL) {#what-s-new-in-primetime-streaming-server-april-release}

La versión 1.3 de Primetime incorpora varias funciones nuevas en cuanto al contenido de flujo continuo, una mayor facilidad de uso y seguridad.

**Primetime Streaming Server como una forma unificada de Live Packager y Origen Server**

Primetime Live Packager y Primetime Origen se reúnen para trabajar como un solo componente. Este componente se puede usar como Packager o como Origen, o bien como funciones combinadas para empaquetar y alojar un flujo en directo.

Esto proporciona una interfaz de archivos unificada a estos servidores, lo que facilita su ejecución en un solo equipo. Sigue proporcionando la flexibilidad necesaria para configurarse como un Packager o Origen independiente.

**Compatibilidad con Beta MPEG-DASH**

Primetime Streaming Server admite el empaquetado MPEG-DASH para flujos de trabajo en directo y VOD. El componente Live Packager convierte los flujos RTMP o MPEG-2-TS de ingesta al formato DASH. El componente Origen acepta un flujo DASH.

Para flujos de trabajo VOD, el componente Offline Packager convierte los recursos MP4 y TS al formato MPEG-DASH ISOBFF.

**Conversión de lanzamiento a VOD**

Ahora hay disponible un nuevo componente Servidor de grabación que admite la captura de un flujo en directo y el archivado para la reproducción de VOD. Es compatible con la creación de reproducciones de Evento completo, así como con clips/resaltados para parte del evento. Se puede configurar para grabar flujos de solo audio, eliminar publicidades o barras inclinadas en el contenido en directo. El servidor de grabaciones funciona con Primetime Streaming Server y con Orígenes de terceros.

**Conversión de RTMP a HLS en Primetime Live Packager**

El componente Primetime Live Packager admite la creación de flujos HLS a partir de flujos RTMP. También permite agregar DRM de Primetime y Flujo protegido a los flujos HLS de salida.

**Autenticación para flujos RTMP entrantes en el empaquetador Primetime Live**

Ahora se entrega un usermgmt.jar con Primetime Live Packager para configurar el acceso con credenciales de confianza al enviar un flujo RTMP a Primetime Live Packager

Ahora los codificadores pueden configurarse para utilizar un nombre de usuario/contraseña al enviar flujos a Live Packager.

**PlaylistCreator Tool para crear manifiestos de nivel superior para HDS y HLS**

Ahora hay una utilidad ingeniosa PlaylistCreator.jar disponible con Primetime Offline Packager para crear fácilmente archivos de manifiesto de nivel superior para recursos de HDS y HLS.

**Función de seguridad adicional para incorporar un módulo de seguridad de hardware**

Primetime Offline Packager ahora admite el acceso al certificado de credenciales de Packager y a claves comunes desde un módulo de seguridad de hardware.

Un módulo de seguridad de hardware proporciona protección adicional a estos activos confidenciales.

**Rendimiento mejorado para el empaquetado de VOD**

Se han incorporado varias mejoras de rendimiento para mejorar el tiempo de empaquetado de los recursos intermedios en Primetime Offline Packager

**Rendimiento mejorado para el paquete JIT MP4**

Se han incorporado varias mejoras de rendimiento a las funciones de empaquetado JIT de Primetime Origen para gestionar las solicitudes de los usuarios de una gran biblioteca de recursos VOD.

## Adobe Primetime Streaming Server 1.4 {#adobe-primetime-streaming-server}

### Requisitos mínimos del sistema {#minimum-system-requirements}

**Requisitos de red**

* La red debe estar habilitada para multidifusión para enviar flujo MPEG-TS desde un codificador a Live Packager. Live Packager también acepta un flujo RTMP de un codificador que no requiere una red de multidifusión.

**Sistemas operativos admitidos**

* Linux CentOS 6.3 de 64 bits

**Requisitos de hardware**

* Procesador Intel® Pentium® 4 de 3,2 GHz (se recomienda doble Intel Xeon® o más rápido)
* Sistemas operativos de 64 bits: 4 GB de RAM (se recomiendan 8 GB)
* Se recomienda una tarjeta Ethernet de 1 Gb (se admiten varias tarjetas de red y 10 Gb)
* Disco:

   * (Disk-SAS): Mínimo de 10 GB con 7.500 RPM
   * (Disco-SSD): 400 MBps de lectura y escritura
   * (NAS): Vínculo dedicado de 1 GB

**Requisitos de software**

* Oracle Java JRE 1.7 (recomendado: Sun/Oracle Hotspot JVM). El JDK es necesario para el acceso de JConsole a las API de JMX

### Instalar y configurar Primetime Streaming Server {#install-and-configure-primetime-streaming-server}

**Instalación del servidor de flujo continuo**

1. Descargue el software Java SE y JDK del [sitio de Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) y siga las instrucciones de instalación.
2. Extraiga el archivo de Adobe Primetime-Streaming Server 1.4, `Primetime- StreamingServer-1-4-0-b206-12042014.zip` en el disco.

**Inicio del servidor de flujo continuo Primetime**

Para inicio del servidor de flujo, ejecute el siguiente comando desde la línea de comandos del directorio raíz del servidor de flujo:\
`$./pss_start.sh`

**Configurar Primetime Streaming Server como Live Packager o HTTP Origen Server**

Para configurar el servidor de flujo como Live Packager o Origen Server, actualice el archivo de configuración pss.xml ubicado en el directorio conf del directorio raíz del servidor de flujo:

```
<Config> 
<!-- Set this false to disable the Origin Component. --> 
<OriginEnabled&gt;true&lt;/OriginEnabled>  
<!-- Set this false to disable the Packager Component. -->  
<PackagerEnabled&gt;true&lt;/PackagerEnabled>
</Config>
```

**Detener Primetime Streaming Server**

Para detener el servidor de flujo, ejecute el siguiente comando en el directorio raíz del servidor de flujo:\
`$./pss_stop.sh`

**Reinicie Primetime Streaming Server**

Para reiniciar el servidor de flujo, detenga y inicio el servidor de flujo.

<!-- 

Comment Type: draft

**Configuring Primetime Streaming Server**

Refer the Primetime Streaming Server Getting Started document for the configuration details available at [https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf](https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf).

-->

**Desinstalación de Primetime Streaming Server**

Para desinstalar el servidor de flujo, detenga el servidor de flujo y quite el directorio pss del servidor de flujo en el directorio Primetime

## Uso de Live Packager y Origen Server 1.4 {#working-with-live-packager-and-origin-server}

Esta sección se aplica cuando no se utiliza Primetime Streaming Server y en su lugar se implementa Primetime Live Packager Y/O Primetime Origen Server

### Requisitos mínimos del sistema {#minimum-system-requirements-1}

**Requisitos de red**

* La red debe estar habilitada para multidifusión para enviar flujo MPEG-TS desde un codificador a Live Packager. Live Packager también acepta un flujo RTMP de un codificador que no requiere una red de multidifusión.

**Sistemas operativos admitidos**

* Linux CentOS 6.3 de 64 bits

**Requisitos de hardware**

* Procesador Intel® Pentium® 4 de 3,2 GHz (se recomienda doble Intel Xeon® o más rápido)
* Sistemas operativos de 64 bits: 4 GB de RAM (se recomiendan 8 GB)
* Se recomienda una tarjeta Ethernet de 1 Gb (se admiten varias tarjetas de red y 10 Gb)
* Disco:

   * (Disk-SAS): Mínimo de 10 GB con 7.500 RPM
   * (Disco-SSD): 400 MBps de lectura y escritura
   * (NAS): Vínculo dedicado de 1 GB

**Requisitos de software**

* Oracle Java JRE 1.7 (recomendado: Sun/Oracle Hotspot JVM). El JDK es necesario para el acceso de JConsole a las API de JMX

Los requisitos mínimos del sistema anteriores son verdaderos tanto para Origen Server como para Live Packager.

### Instalar y configurar Live Packager {#install-and-configure-the-live-packager}

**Instalación de Live Packager**

1. Descargue el software Java SE y JDK del [sitio de Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) y siga las instrucciones de instalación.
1. Extraiga el archivo de Adobe Primetime - Live Packager 1.4 `Primetime-LivePackager-1-4-0-b206-12042014.zip` en su disco.

**Instalación de HTTP Origen Server**

1. Descargue el software Java JRE y JDK del [sitio de Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) y siga las instrucciones de instalación.
1. Extraiga el archivo de almacenamiento Adobe Primetime - HTTP Origen Server 1.4, `Primetime-HttpOrigin-1-4-0-b206-12042014.zip`, en el disco.

**Para inicio de Live** PackagerPara inicio del empaquetador, ejecute el siguiente comando desde el directorio raíz del empaquetador:\
`$packager_start.sh`

**Inicio del servidor de Origen HTTP**

Para inicio del servidor de Origen HTTP, ejecute el siguiente comando desde la línea de comandos del directorio raíz del servidor de Origen:\
`$./origin_start.sh`

**Detener Live Packager**

Para detener el empaquetador, ejecute el siguiente comando desde el directorio raíz del empaquetador:\
`$packager_stop.sh`

**Detener el servidor de Origen HTTP**

Para detener el servidor Origen HTTP, ejecute el siguiente comando en el directorio raíz del servidor Origen:\
`$./origin_stop.sh`

**Reinicie Live Packager**

Para reiniciar el empaquetador, detenga y inicio el empaquetador.

**Nota**: Cuando el empaquetador inicio, intenta inicializar la información de arranque desde el destinatario de fragmento en el directorio temp. Si la información de arranque se encuentra en el destinatario del fragmento, significa que el empaquetador se ha reiniciado. En caso de reinicio, el empaquetador espera hasta el siguiente límite de fragmento y, a continuación, realiza el empaquetado de inicios. El empaquetador inserta una entrada de hueco en el bootstrap para indicar que faltan fragmentos.

**Reinicie el servidor de Origen HTTP**

Para reiniciar el servidor Origen HTTP, detenga y inicio el servidor Origen HTTP.

**Configuración de Live Packager**

El archivo de distribución contiene una configuración de muestra que puede utilizarse para probar el empaquetador.

Después de extraer el archivo Adobe Primetime - Live Packager 1.4, cambie los directorios al directorio del empaquetador y ejecute la secuencia de comandos packager_inicio.sh. La configuración de ejemplo escucha la dirección de multidifusión 239.235.0.3:14000 y ejecuta el servidor de origen local en el puerto 8080. El resultado está configurado para escribirse en `packager/webroot/_default_/_default_/ directory`.

<!-- 

Comment Type: draft

For more details about the configuration refer [the Primetime Live Packager document](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

-->

**Configuración del servidor Origen HTTP**

Consulte el documento Primetime HTTP Origen Server Getting Started para obtener los detalles de configuración disponibles aquí.

**Desinstalación de Live Packager**

Para desinstalar el empaquetador, detenga el empaquetador y elimine el directorio del empaquetador del directorio Primetime.

**Desinstalación de HTTP Origen Server**

Para desinstalar HTTP Origen Server, detenga HTTP Origen Server y elimine el directorio httporigin del HTTP Origen Server en el directorio Primetime.

## Adobe Primetime Offline Packager 1.4 {#adobe-primetime-offline-packager}

### Requisitos mínimos del sistema {#minimum-system-requirements-2}

**Sistemas operativos admitidos**

* Linux CentOS 6.3 de 64 bits

**Requisitos de hardware**

* Procesador Intel® Pentium® 4 de 3,2 GHz (se recomienda doble Intel Xeon® o más rápido)
* Sistemas operativos de 64 bits: 4 GB de RAM (se recomiendan 8 GB)
* Se recomienda una tarjeta Ethernet de 1 Gb (se admiten varias tarjetas de red y 10 Gb)
* Disco:

   * (Disk-SAS): Mínimo de 10 GB con 7.500 RPM
   * (Disco-SSD): 400 MBps de lectura y escritura
   * (NAS): Vínculo dedicado de 1 GB

**Requisitos de software**

* Oracle Java JRE 1.7 o posterior.

### Instalar y configurar Offline Packager {#install-and-configure-offline-packager}

Para instalar Offline Packager, siga estos pasos:

1. Descargue el software Java SE del [sitio de Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) y siga las instrucciones de instalación.
1. Extraiga el archivo de Adobe Primetime - Offline Packager 1.4, `Primetime- OfflinePackager-1-4-0-b206-12042014.zip`, en su disco.

Consulte el documento Primetime Offline Packager Getting Started para obtener los detalles de configuración disponibles [aquí](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en la página [Información y soporte de Adobe Primetime](https://helpx.adobe.com/support/primetime.html).