---
title: Versiones de Primetime Streaming Server
description: Novedades de las versiones 1.3 y 1.4 de Primetime Streaming Server.
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: 80c4687e-b0ac-48f2-a1c3-8751552da9d1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 0%

---

# Versiones de Primetime Streaming Server {#primetime-streaming-server-x-releases}

Novedades de las versiones 1.3 y 1.4 de Primetime Streaming Server.

## Novedades de Primetime Streaming Server 1.4 (versión de diciembre) {#what-s-new-in-primetime-streaming-server-december-release}

**Empaquetador sin conexión**

* Los flujos HLS de salida ahora contienen metadatos ID3 presentes en MPEG-2 TS
* Ahora, solo los flujos de audio HLS pueden tener una imagen estática asociada
* Compatibilidad para proporcionar entradas IV como entrada de usuario para flujos de trabajo de cifrado AES de HLS
* Compatibilidad para generar IV en un archivo cuando IV es generado por el empaquetador sin conexión
* El creador de listas de reproducción ahora admite la asociación de grupos de audio en varios idiomas y grupos de subtítulos WebVTT en varios idiomas a flujos de medios

**Servidor de origen**

* El cifrado AES de HLS está disponible para flujos de trabajo de Live y VOD. Primetime Origin puede aplicar Just in Time cifrado AES HLS a flujos HLS entrantes o archivos MP4.
* También puede aplicar el cifrado AES JIT HLS cuando se utiliza para convertir los flujos entrantes del HDS a flujos HLS.
* El origen de Primetime ahora admite la inclusión en listas de permitidos de SWF para flujos PHLS. Anteriormente, solo era compatible con flujos PHDS

**Primetime Live Packager**

* Soporte para generar flujos HLS AES-128 para flujos de entrada RTMP y MPEG-2 TS

Se han actualizado los certificados de PHD/PHLS. La nueva fecha de caducidad para el mismo será el 10/01/2016.

### **Correcciones de errores incluidas en la versión 1.4** {#bug-fixes-included-in-release}

* PTPUB-282- El manifiesto de nivel de conjunto HLS creado por OfflinePackager 1.3.1 no tiene información de codificación y resolución.
* PTPUB-353: PlayListCreator no admite la adición de información WebVTT en el manifiesto de nivel establecido
* PTPUB-583: la herramienta PlaylistCreator antepone inesperadamente los URI de grupo a.
* El creador de la lista de reproducción de PTPUB-605 no enumera el grupo SUBTITLE en cada flujo de variante
* PTPUB-634: el empaquetador sin conexión agrega SpliceInsert a manifest.
* PTPUB-635: varias etiquetas SpliceOut insertadas para una sola señal de anuncio.

### Problema conocido en la versión 1.4 {#known-issue-in-release}

* El modo PTPUB- 645 DPISimple se fuerza incluso cuando se especifica el modo DPIScte35 cuando tanto las señales de línea de comandos como las señales en flujo se proporcionan en la configuración del empaquetador sin conexión

## Novedades de Primetime Streaming Server 1.3.1 (versión de MAYO) {#what-s-new-in-primetime-streaming-server-may-release}

La versión 1.3.1 hace referencia a la revisión. Las siguientes mejoras lo convierten en una actualización recomendada para los clientes, ya que consiste en mejoras de rendimiento clave para casos de uso de JIT MP4:

1. Corrección de rendimiento para la generación MP4 JIT m3u8 en Origin con DRM, incluida la rotación de clave
1. Se ha añadido la configuración CopyQueryParamToJITFragmentURIs para copiar parámetros de consulta de la solicitud de manifiesto JIT a los URI de fragmento generados para la conversión JIT MP4. Consulte la documentación del servidor de origen HTTP para ver un ejemplo de uso
1. Permitir la conversión de archivos MP4 sin extensión para JIT mediante la configuración Config/MP4Only añadida a vod.xml

### Correcciones de errores incluidas en la versión 1.3.1 {#bug-fixes-included-in-release-1}

* 3759167: no todas las señales SCTE35 llegan al manifiesto de salida debido a una anomalía en la marca de tiempo al empaquetar. Aplique pts_adjustment en el SpliceTime de la TimeSignal de SpliceInfoSection en el mensaje SCTE35.

### Problemas conocidos de la versión 1.3.1 {#known-issues-in-release}

* 3717039: cuando el empaquetador está configurado para producir señales de modo simple de ppp, realmente debe buscar tipos de señales específicas, como inserción de empalme o oportunidad de colocación, y convertir solo esas señales a señales de modo simple. Debe ignorar otros tipos de señales, como el inicio del programa, el inicio de la red, etc.

* 3718598: cuando Origin Server está configurado para servir contenido protegido con acceso HSM habilitado, el cliente LunaSA back-end realiza una comunicación frecuente con el módulo HSM

## Novedades de Primetime Streaming Server 1.3 (versión de ABRIL) {#what-s-new-in-primetime-streaming-server-april-release}

La versión Primetime 1.3 incorpora varias funciones nuevas en torno al contenido de streaming, una mejor facilidad de uso y seguridad.

**Servidor de streaming de Primetime como una forma unificada de Live Packager y Origin Server**

Primetime Live Packager y Primetime Origin se unen para funcionar como un solo componente. Este componente puede utilizarse como empaquetador o como origen, o puede utilizar las capacidades combinadas para empaquetar y alojar una emisión en directo.

Esto proporciona una interfaz de archivo unificada a estos servidores, lo que facilita su ejecución en un solo equipo. Sigue proporcionando la flexibilidad para configurarse como un empaquetador u origen independiente.

**Compatibilidad con MPEG-DASH beta**

Primetime Streaming Server admite el empaquetado MPEG-DASH para flujos de trabajo en directo y VOD. El componente Live Packager convierte los flujos de ingesta RTMP o MPEG-2-TS al formato DASH. El componente Origen acepta una secuencia DASH.

Para flujos de trabajo de VOD, el componente Empaquetador sin conexión convierte los recursos MP4 y TS al formato MPEG-DASH ISOBFF.

**Conversión de Live to VOD**

Ya está disponible un nuevo componente Servidor de grabación que permite capturar una emisión en directo y archivar para la reproducción de VOD. Admite la creación de Reproducciones completas de eventos, así como clips/resaltados para parte del evento. Se puede configurar para grabar flujos de solo audio, eliminar anuncios o pizarras en contenido en directo. El servidor de grabación funciona con el servidor de flujo continuo de Primetime, así como con orígenes de terceros.

**Conversión de RTMP a HLS en el empaquetador en vivo de Primetime**

El componente Primetime Live Packager admite la creación de flujos HLS a partir de flujos RTMP. También permite añadir DRM de Primetime y Flujo protegido a las secuencias HLS de salida.

**Autenticación para flujos RTMP entrantes en el empaquetador de Primetime Live**

Ahora, usermgmt.jar se envía con Primetime Live Packager para configurar el acceso con credenciales de confianza al enviar un flujo RTMP a Primetime Live Packager

Ahora los codificadores pueden configurarse para usar un nombre de usuario/contraseña al enviar flujos a Live Packager.

**Herramienta de creación de listas de reproducción para crear manifiestos de nivel superior para HDS y HLS**

Ahora hay disponible una ingeniosa utilidad PlaylistCreator.jar con Primetime Offline Packager para crear fácilmente archivos de manifiesto de nivel superior para recursos HDS y HLS.

**Función de seguridad adicional para incorporar un módulo de seguridad de hardware**

El empaquetador sin conexión de Primetime ahora admite el acceso al certificado de credencial del empaquetador y a las claves comunes desde un módulo de seguridad de hardware.

Un módulo de seguridad de hardware proporciona protección adicional a estos activos confidenciales.

**Rendimiento mejorado para el empaquetado de VOD**

Se han incorporado varias mejoras de rendimiento para mejorar el tiempo de empaquetado de los recursos intermedios en el empaquetador sin conexión de Primetime

**Rendimiento mejorado para el empaquetado JIT MP4**

Se han incorporado varias mejoras de rendimiento a las funciones de empaquetado JIT de Primetime Origin para gestionar las solicitudes de los usuarios para grandes bibliotecas de recursos de VOD.

## Adobe Primetime Streaming Server 1.4 {#adobe-primetime-streaming-server}

### Requisitos mínimos del sistema {#minimum-system-requirements}

**Requisitos de red**

* La red debe estar habilitada para multidifusión para enviar secuencias MPEG-TS desde un codificador a Live Packager. Live Packager también acepta un flujo RTMP desde un codificador que no requiere una red de multidifusión.

**Sistemas operativos compatibles**

* Linux CentOS 6.3 de 64 bits

**Requisitos de hardware**

* Procesador Intel® Pentium® 4 a 3,2 GHz (se recomienda dual Intel Xeon® o más rápido)
* Sistemas operativos de 64 bits: 4 GB de RAM (se recomienda 8 GB)
* Tarjeta 1 Gb Ethernet recomendada (también admite varias tarjetas de red y 10 Gb)
* Disco:

   * (Disk-SAS) : Mínimo de 10 GB con 7.500 rpm
   * (Disco SSD) : 400 MB/s de lectura y escritura
   * (NAS) : Vínculo dedicado de 1 GB

**Requisitos de software**

* Oracle Java JRE 1.7 (recomendado: Sun/Oracle Hotspot JVM). El JDK es necesario para que JConsole acceda a las API de JMX

### Instalación y configuración de Primetime Streaming Server {#install-and-configure-primetime-streaming-server}

**Instalar servidor de flujo continuo**

1. Descargue el software Java SE y JDK desde el [sitio de oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) y siga las instrucciones de instalación.
2. Extraiga el archivo de Adobe Primetime-Streaming Server 1.4, `Primetime- StreamingServer-1-4-0-b206-12042014.zip` al disco.

**Inicio del servidor de flujo de Primetime**

Para iniciar el servidor de flujo continuo, ejecute el siguiente comando desde la línea de comandos del directorio raíz del servidor de flujo continuo:\
`$./pss_start.sh`

**Configuración del servidor de streaming de Primetime como Live Packager o HTTP Origin Server**

Para configurar el servidor de streaming como Live Packager o Origin Server, actualice el archivo de configuración pss.xml ubicado en el directorio conf en el directorio raíz del servidor de streaming:

```
<Config> 
<!-- Set this false to disable the Origin Component. --> 
<OriginEnabled&gt;true&lt;/OriginEnabled>  
<!-- Set this false to disable the Packager Component. -->  
<PackagerEnabled&gt;true&lt;/PackagerEnabled>
</Config>
```

**Detener el servidor de flujo de Primetime**

Para detener el servidor de flujo continuo, ejecute el siguiente comando en el directorio raíz del servidor de flujo continuo:\
`$./pss_stop.sh`

**Reinicie Primetime Streaming Server**

Para reiniciar el servidor de flujo continuo, detenga e inicie el servidor de flujo continuo.

<!-- 

Comment Type: draft

**Configuring Primetime Streaming Server**

Refer the Primetime Streaming Server Getting Started document for the configuration details available at [https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf](https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf).

-->

**Desinstalación del servidor de flujo de Primetime**

Para desinstalar el servidor de flujo continuo, detenga el servidor de flujo continuo y elimine el directorio pss del servidor de flujo continuo en el directorio Primetime

## Uso de Live Packager y Origin Server 1.4 {#working-with-live-packager-and-origin-server}

Esta sección se aplica cuando no se utiliza Primetime Streaming Server y, en su lugar, se está implementando Primetime Live packager AND/OR Primetime Origin Server

### Requisitos mínimos del sistema {#minimum-system-requirements-1}

**Requisitos de red**

* La red debe estar habilitada para multidifusión para enviar secuencias MPEG-TS desde un codificador a Live Packager. Live Packager también acepta un flujo RTMP desde un codificador que no requiere una red de multidifusión.

**Sistemas operativos compatibles**

* Linux CentOS 6.3 de 64 bits

**Requisitos de hardware**

* Procesador Intel® Pentium® 4 a 3,2 GHz (se recomienda dual Intel Xeon® o más rápido)
* Sistemas operativos de 64 bits: 4 GB de RAM (se recomienda 8 GB)
* Tarjeta 1 Gb Ethernet recomendada (también admite varias tarjetas de red y 10 Gb)
* Disco:

   * (Disk-SAS) : Mínimo de 10 GB con 7.500 rpm
   * (Disco SSD) : 400 MB/s de lectura y escritura
   * (NAS) : Vínculo dedicado de 1 GB

**Requisitos de software**

* Oracle Java JRE 1.7 (recomendado: Sun/Oracle Hotspot JVM). El JDK es necesario para que JConsole acceda a las API de JMX

Los requisitos mínimos del sistema anteriores son verdaderos para Origin Server así como para Live Packager.

### Instalación y configuración de Live Packager {#install-and-configure-the-live-packager}

**Instalación del Live Packager**

1. Descargue el software Java SE y JDK desde el [sitio de oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) y siga las instrucciones de instalación.
1. Extraer el archivo de Adobe Primetime - Live Packager 1.4 `Primetime-LivePackager-1-4-0-b206-12042014.zip` al disco.

**Instalación del servidor de origen HTTP**

1. Descargue el software Java JRE y JDK desde el [sitio de oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) y siga las instrucciones de instalación.
1. Extraiga el archivo de Adobe Primetime - HTTP Origin Server 1.4, `Primetime-HttpOrigin-1-4-0-b206-12042014.zip`, en el disco.

**Para iniciar el Live Packager** Para iniciar el empaquetador, ejecute el siguiente comando desde el directorio raíz del empaquetador:\
`$packager_start.sh`

**Para iniciar el servidor de origen HTTP**

Para iniciar el servidor de origen HTTP, ejecute el siguiente comando desde la línea de comandos del directorio raíz del servidor de origen:\
`$./origin_start.sh`

**Detener el empaquetador en directo**

Para detener el empaquetador, ejecute el siguiente comando desde el directorio raíz del empaquetador:\
`$packager_stop.sh`

**Detenga el servidor de origen HTTP**

Para detener el servidor de origen HTTP, ejecute el siguiente comando en el directorio raíz del servidor de origen:\
`$./origin_stop.sh`

**Reinicie Live Packager**

Para reiniciar el empaquetador, detenga e inicie el empaquetador.

**Nota**: Cuando se inicia el empaquetador, intenta inicializar la información de bootstrap desde el destino del fragmento en el directorio temporal. Si la información de bootstrap se encuentra en el destino del fragmento, implica que el empaquetador se ha reiniciado. En caso de reinicio, el empaquetador espera hasta el siguiente límite de fragmento y, a continuación, inicia el empaquetado. El empaquetador inserta una entrada de espacio en el bootstrap para indicar que faltan fragmentos.

**Reinicie el servidor de origen HTTP**

Para reiniciar el servidor de origen HTTP, detenga e inicie el servidor de origen HTTP.

**Configuración del Live Packager**

El archivo de distribución contiene una configuración de ejemplo que se puede utilizar para probar el empaquetador.

Después de extraer el archivo Adobe Primetime - Live Packager 1.4, cambie los directorios al directorio packager y ejecute el script packager_start.sh. La configuración de ejemplo escucha en la dirección de multidifusión 239.235.0.3:14000 y ejecuta el servidor de origen local en el puerto 8080. La salida está configurada para escribirse en el `packager/webroot/_default_/_default_/ directory`.

<!-- 

Comment Type: draft

For more details about the configuration refer [the Primetime Live Packager document](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

-->

**Configuración del servidor de origen HTTP**

Consulte el documento Introducción al servidor de origen HTTP de Primetime para obtener los detalles de configuración disponibles aquí.

**Desinstalación del Live Packager**

Para desinstalar el empaquetador, detenga el empaquetador y quite el directorio del empaquetador del directorio Primetime.

**Desinstalación del servidor de origen HTTP**

Para desinstalar el servidor de origen HTTP, detenga el servidor de origen HTTP y elimine el directorio httporgin del servidor de origen HTTP en el directorio Primetime.

## Adobe Primetime Offline Packager 1.4 {#adobe-primetime-offline-packager}

### Requisitos mínimos del sistema {#minimum-system-requirements-2}

**Sistemas operativos compatibles**

* Linux CentOS 6.3 de 64 bits

**Requisitos de hardware**

* Procesador Intel® Pentium® 4 a 3,2 GHz (se recomienda dual Intel Xeon® o más rápido)
* Sistemas operativos de 64 bits: 4 GB de RAM (se recomienda 8 GB)
* Tarjeta 1 Gb Ethernet recomendada (también admite varias tarjetas de red y 10 Gb)
* Disco:

   * (Disk-SAS) : Mínimo de 10 GB con 7.500 rpm
   * (Disco SSD) : 400 MB/s de lectura y escritura
   * (NAS) : Vínculo dedicado de 1 GB

**Requisitos de software**

* Oracle Java JRE 1.7 o posterior.

### Instalar y configurar el empaquetador sin conexión {#install-and-configure-offline-packager}

Para instalar el empaquetador sin conexión, siga estos pasos:

1. Descargue el software Java SE desde el [sitio de oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) y siga las instrucciones de instalación.
1. Extraiga el archivo Adobe Primetime - Offline Packager 1.4, `Primetime- OfflinePackager-1-4-0-b206-12042014.zip`, en el disco.

Consulte el documento Introducción al empaquetador sin conexión de Primetime para obtener los detalles de configuración disponibles [aquí](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en [Formación y asistencia de Adobe Primetime](https://helpx.adobe.com/support/primetime.html) página.
