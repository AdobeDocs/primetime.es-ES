---
title: Versiones de Primetime Streaming Server
description: Novedades de las versiones 1.3 y 1.4 de Primetime Streaming Server.
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 0%

---


# Versiones de Primetime Streaming Server {#primetime-streaming-server-x-releases}

Novedades de las versiones 1.3 y 1.4 de Primetime Streaming Server.

## Novedades en Primetime Streaming Server 1.4 (versión de diciembre) {#what-s-new-in-primetime-streaming-server-december-release}

**Paquete sin conexión**

* Los flujos HLS de salida ahora contienen metadatos ID3 presentes en MPEG-2 TS
* HLS Audio solo las emisiones ahora pueden tener una imagen estática asociada
* Compatibilidad para proporcionar IV como entrada de usuario para flujos de trabajo de cifrado HLS AES
* Compatibilidad con la salida IV a un archivo cuando IV es generado por el empaquetador sin conexión
* El Creador de listas de reproducción ahora es compatible con la asociación de grupos de audio multilingües y grupos de subtítulos WebVTT multilingües a flujos de medios

**Servidor de origen**

* El cifrado HLS AES está disponible para flujos de trabajo en directo y VOD. Primetime Origin puede Just in Time aplicar cifrado HLS AES a flujos HLS entrantes o archivos MP4.
* También puede aplicar el cifrado AES JIT HLS cuando se utiliza para convertir flujos entrantes de HDS a flujos HLS.
* El origen de Primetime ahora admite la inclusión en la lista de permitidos SWF para flujos PHLS. Anteriormente, solo era compatible con flujos de PHDS

**Primetime Live Packager**

* Compatibilidad para generar flujos HLS AES-128 para flujos RTMP de entrada y MPEG-2 TS

Se han actualizado los certificados PHDS/PHLS. La nueva fecha de caducidad para el mismo será 10/01/2016.

### **Correcciones de errores incluidas en la versión 1.4** {#bug-fixes-included-in-release}

* PTPUB-282- El manifiesto de nivel de conjunto HLS creado por OfflinePackager 1.3.1 no tiene información de códec y resolución.
* PTPUB-353 - PlayListCreator no admite la adición de información de WebVTT en el manifiesto de nivel establecido
* PTPUB-583 - La herramienta PlaylistCreator antepone inesperadamente los URI de grupo.
* El Creador de listas de reproducción PTPUB-605 no enumera el grupo de subtítulos en cada flujo de variantes
* PTPUB-634 -Offline Packager agrega SpliceInsert al manifiesto.
* PTPUB-635 - Varias etiquetas SpliceOut insertadas para una sola señal de anuncio.

### Problema conocido en la versión 1.4 {#known-issue-in-release}

* El modo PTPUB-645 DPISimple se fuerza incluso cuando se especifica el modo DPIScte35 cuando tanto las señales de línea de comandos como las señales de flujo se proporcionan en la configuración del empaquetador sin conexión

## Novedades de Primetime Streaming Server 1.3.1 (versión de mayo) {#what-s-new-in-primetime-streaming-server-may-release}

La versión 1.3.1 hace referencia a la corrección. Las siguientes mejoras lo convierten en una actualización recomendada para los clientes, ya que consiste en mejoras clave de rendimiento para casos de uso de JIT MP4:

1. Corrección de rendimiento para la generación m3u8 de MP4 JIT en origen con DRM, incluida la rotación de claves
1. Se ha añadido la configuración &quot;CopyQueryParamToJITFragmentURIs&quot; para copiar parámetros de consulta de la solicitud de manifiesto de JIT a los URI de fragmento generados para la conversión JIT de MP4. Consulte la documentación del servidor de origen HTTP para obtener ejemplos de uso
1. Permitir archivos MP4 sin extensión para la conversión JIT , a través de la configuración Config/MP4Only añadida a vod.xml

### Correcciones de errores incluidas en la versión 1.3.1 {#bug-fixes-included-in-release-1}

* 3759167 - No todas las señales SCTE35 llegan al manifiesto de salida debido a una anomalía en la marca de tiempo al empaquetar. Aplique el parámetro eps_adapt en el SpliceTime de la señal de tiempo de SpliceInfoSection en el mensaje SCTE35.

### Problemas conocidos en la versión 1.3.1 {#known-issues-in-release}

* 3717039 - Cuando el empaquetador está configurado para producir señales de modo simple DPI, realmente debería estar buscando tipos de señal específicos, como la oportunidad de inserción o colocación de empalme, y convirtiendo sólo esas señales en simples señales de modo. Debe ignorar otros tipos de señales, como el inicio del programa, el inicio de la red, etc.

* 3718598 - Cuando el servidor de origen está configurado para servir contenido protegido con acceso HSM habilitado, el cliente backend LunaSA realiza una comunicación frecuente con el módulo HSM

## Novedades de Primetime Streaming Server 1.3 (versión de ABRIL) {#what-s-new-in-primetime-streaming-server-april-release}

La versión Primetime 1.3 incorpora varias funciones nuevas en cuanto al contenido de transmisión, una mejor facilidad de uso y seguridad.

**Primetime Streaming Server como una forma unificada de Live Packager y Origin Server**

Primetime Live Packager y Primetime Origin se agrupan para funcionar como un solo componente. Este componente se puede utilizar como un Packager o como un Origin o utilizar las capacidades combinadas para empaquetar y alojar un Stream en directo.

Esto proporciona una interfaz de archivos unificada a estos servidores, lo que facilita su ejecución en un solo equipo. Sigue proporcionando la flexibilidad para configurarse como un Packager u Origin separado.

**Compatibilidad con Beta MPEG-DASH**

Primetime Streaming Server es compatible con el empaquetado MPEG-DASH para flujos de trabajo en directo y VOD. El componente Live packager convierte la ingesta de transmisiones RTMP o MPEG-2-TS al formato DASH. El componente Origen acepta un flujo DASH.

Para los flujos de trabajo de VOD, el componente Packager sin conexión convierte los activos de MP4 y TS al formato MPEG-DASH ISOBFF.

**Conversión de Live a VOD**

Ya está disponible un nuevo componente Servidor de grabación que admite la captura de un flujo en directo y el archivado para la reproducción de VOD. Admite la creación de reproducciones de eventos completas, así como clips/resaltados para parte del evento. Se puede configurar para grabar únicamente emisiones de audio, eliminar anuncios o barras en contenido activo. El servidor de grabación funciona con Primetime Streaming Server, así como con orígenes de terceros.

**Conversión de RTMP a HLS en Primetime Live Packager**

El componente Primetime Live Packager admite la creación de flujos HLS a partir de flujos RTMP. También permite añadir Primetime DRM y flujos protegidos a los flujos HLS de salida.

**Autenticación para emisiones RTMP entrantes para el empaquetador Primetime Live**

Un usermgmt.jar ahora se envía con Primetime Live Packager para configurar el acceso con credenciales de confianza al enviar un flujo RTMP a Primetime Live Packager

Ahora los codificadores pueden configurarse para utilizar un nombre de usuario y contraseña al enviar transmisiones a Live Packager.

**Lista de reproducciónHerramienta de creación para crear manifiestos de nivel superior para HDS y HLS**

Ahora hay disponible una utilidad gratuita PlaylistCreator.jar con Primetime Offline Packager para crear fácilmente archivos de manifiesto de nivel superior para los activos HDS y HLS.

**Función de seguridad adicional para incorporar un módulo de seguridad de hardware**

Primetime Offline Packager ahora admite el acceso al certificado Credencial de Packager y a claves comunes desde un módulo de seguridad de hardware.

Un módulo de seguridad de hardware proporciona protección adicional a estos activos confidenciales.

**Rendimiento mejorado para el paquete de VOD**

Se han incorporado varias mejoras de rendimiento para mejorar el tiempo de empaquetado de los recursos intermedios en Primetime Offline Packager

**Rendimiento mejorado para el paquete JIT MP4**

Se han incorporado varias mejoras de rendimiento a las capacidades de empaquetado JIT de Primetime Origin para gestionar las solicitudes de los usuarios para una gran biblioteca de activos de VOD.

## Adobe Primetime Streaming Server 1.4 {#adobe-primetime-streaming-server}

### Requisitos mínimos del sistema {#minimum-system-requirements}

**Requisitos de red**

* La red debe estar habilitada para Multicast para enviar el flujo MPEG-TS desde un codificador a Live Packager. Live Packager también acepta un flujo RTMP de un codificador que no requiere una red de multidifusión.

**Sistemas operativos compatibles**

* Linux CentOS 6.3 de 64 bits

**Requisitos de hardware**

* Procesador Intel® Pentium® 4 a 3,2 GHz (se recomienda el procesador Intel Xeon® dual o más rápido)
* Sistemas operativos de 64 bits: 4 GB de RAM (se recomiendan 8 GB)
* Tarjeta Ethernet de 1 Gb recomendada (también se admiten varias tarjetas de red y 10 Gb)
* Disco:

   * (Disk-SAS) : Mínimo de 10 GB con 7.500 RPM
   * (Disco-SSD) : 400 MBps de lectura/escritura
   * (NAS) : Vínculo dedicado de 1 GB

**Requisitos de software**

* Oracle Java JRE 1.7 (recomendado: Sun/Oracle (JVM). El JDK es necesario para el acceso de JConsole a las API de JMX

### Instalación y configuración de Primetime Streaming Server {#install-and-configure-primetime-streaming-server}

**Instalación del servidor de flujo continuo**

1. Descargue el software Java SE y JDK del [sitio de Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) y siga las instrucciones de instalación.
2. Extraiga el archivo de Adobe Primetime-Streaming Server 1.4, `Primetime- StreamingServer-1-4-0-b206-12042014.zip` en su disco.

**Inicio del servidor de transmisión de Primetime**

Para iniciar el servidor de transmisión, ejecute el siguiente comando desde la línea de comandos en el directorio raíz del servidor de transmisión:\
`$./pss_start.sh`

**Configurar el servidor de transmisión de Primetime como Live Packager o HTTP Origin Server**

Para configurar el servidor de transmisión como Live Packager o el servidor de origen, actualice el archivo de configuración pss.xml colocado en el directorio conf en el directorio raíz del servidor de transmisión:

```
<Config> 
<!-- Set this false to disable the Origin Component. --> 
<OriginEnabled&gt;true&lt;/OriginEnabled>  
<!-- Set this false to disable the Packager Component. -->  
<PackagerEnabled&gt;true&lt;/PackagerEnabled>
</Config>
```

**Detener el servidor de transmisión de Primetime**

Para detener el servidor de transmisión, ejecute el siguiente comando en el directorio raíz del servidor de transmisión:\
`$./pss_stop.sh`

**Reinicio del servidor de transmisión de Primetime**

Para reiniciar el servidor de transmisión, detenga e inicie el servidor de transmisión.

<!-- 

Comment Type: draft

**Configuring Primetime Streaming Server**

Refer the Primetime Streaming Server Getting Started document for the configuration details available at [https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf](https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf).

-->

**Desinstalación del servidor de transmisión de Primetime**

Para desinstalar el servidor de transmisión, detenga el servidor de transmisión y elimine el directorio pss del servidor de transmisión en el directorio Primetime

## Uso de Live Packager y Origin Server 1.4 {#working-with-live-packager-and-origin-server}

Esta sección se aplica cuando no se utiliza Primetime Streaming Server y en su lugar se está implementando Primetime Live Packager AND/OR Primetime Origin Server

### Requisitos mínimos del sistema {#minimum-system-requirements-1}

**Requisitos de red**

* La red debe estar habilitada para Multicast para enviar el flujo MPEG-TS desde un codificador a Live Packager. Live Packager también acepta un flujo RTMP de un codificador que no requiere una red de multidifusión.

**Sistemas operativos compatibles**

* Linux CentOS 6.3 de 64 bits

**Requisitos de hardware**

* Procesador Intel® Pentium® 4 a 3,2 GHz (se recomienda el procesador Intel Xeon® dual o más rápido)
* Sistemas operativos de 64 bits: 4 GB de RAM (se recomiendan 8 GB)
* Tarjeta Ethernet de 1 Gb recomendada (también se admiten varias tarjetas de red y 10 Gb)
* Disco:

   * (Disk-SAS) : Mínimo de 10 GB con 7.500 RPM
   * (Disco-SSD) : 400 MBps de lectura/escritura
   * (NAS) : Vínculo dedicado de 1 GB

**Requisitos de software**

* Oracle Java JRE 1.7 (recomendado: Sun/Oracle (JVM). El JDK es necesario para el acceso de JConsole a las API de JMX

Los requisitos mínimos del sistema anteriores son verdaderos tanto para el servidor de origen como para Live Packager.

### Instale y configure Live Packager {#install-and-configure-the-live-packager}

**Instalación de Live Packager**

1. Descargue el software Java SE y JDK del [sitio de Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) y siga las instrucciones de instalación.
1. Extraiga el archivo `Primetime-LivePackager-1-4-0-b206-12042014.zip` del archivo de Adobe Primetime - Live Packager 1.4 a su disco.

**Instalación del servidor de origen HTTP**

1. Descargue el software JRE y JDK de Java desde el [sitio de Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) y siga las instrucciones de instalación.
1. Extraiga el archivo de Adobe Primetime - HTTP Origin Server 1.4, `Primetime-HttpOrigin-1-4-0-b206-12042014.zip`, en su disco.

**Para iniciar Live** PackagerPara iniciar el empaquetador, ejecute el siguiente comando desde el directorio raíz del empaquetador:\
`$packager_start.sh`

**Para iniciar el servidor de origen HTTP**

Para iniciar el servidor de origen HTTP, ejecute el siguiente comando desde la línea de comandos en el directorio raíz del servidor de origen:\
`$./origin_start.sh`

**Detener Live Packager**

Para detener el empaquetador, ejecute el siguiente comando desde el directorio raíz del empaquetador:\
`$packager_stop.sh`

**Detener el servidor de origen HTTP**

Para detener el servidor de origen HTTP, ejecute el siguiente comando en el directorio raíz del servidor de origen:\
`$./origin_stop.sh`

**Reinicie Live Packager**

Para reiniciar el empaquetador, detenga e inicie el empaquetador.

**Nota**: Cuando se inicia el empaquetador, intenta inicializar la información de arranque desde el destino del fragmento en el directorio temporal. Si la información de arranque se encuentra en el destino del fragmento, significa que el empaquetador se ha reiniciado. En caso de reinicio, el empaquetador espera hasta el siguiente límite de fragmento y, a continuación, inicia el empaquetado. El empaquetador inserta una entrada de hueco en el bootstrap para indicar que faltan fragmentos.

**Reinicio del servidor de origen HTTP**

Para reiniciar el servidor de origen HTTP, detenga e inicie el servidor de origen HTTP.

**Configuración de Live Packager**

El archivo de distribución contiene una configuración de muestra que se puede utilizar para probar el empaquetador.

Después de extraer el archivo Adobe Primetime - Live Packager 1.4, cambie los directorios al directorio del empaquetador y ejecute el script packager_start.sh. La configuración de ejemplo escucha en la dirección de multidifusión 239.235.0.3:14000 y ejecuta el servidor de origen local en el puerto 8080. La salida está configurada para escribirse en `packager/webroot/_default_/_default_/ directory`.

<!-- 

Comment Type: draft

For more details about the configuration refer [the Primetime Live Packager document](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

-->

**Configuración del servidor de origen HTTP**

Consulte el documento Introducción al servidor de origen HTTP de Primetime para obtener los detalles de configuración disponibles aquí.

**Desinstalación de Live Packager**

Para desinstalar el empaquetador, detenga el empaquetador y elimine el directorio del empaquetador del directorio Primetime.

**Desinstalación del servidor de origen HTTP**

Para desinstalar el servidor de origen HTTP, detenga el servidor de origen HTTP y elimine el directorio httporigin del servidor de origen HTTP en el directorio Primetime.

## Adobe Primetime Offline Packager 1.4 {#adobe-primetime-offline-packager}

### Requisitos mínimos del sistema {#minimum-system-requirements-2}

**Sistemas operativos compatibles**

* Linux CentOS 6.3 de 64 bits

**Requisitos de hardware**

* Procesador Intel® Pentium® 4 a 3,2 GHz (se recomienda el procesador Intel Xeon® dual o más rápido)
* Sistemas operativos de 64 bits: 4 GB de RAM (se recomiendan 8 GB)
* Tarjeta Ethernet de 1 Gb recomendada (también se admiten varias tarjetas de red y 10 Gb)
* Disco:

   * (Disk-SAS) : Mínimo de 10 GB con 7.500 RPM
   * (Disco-SSD) : 400 MBps de lectura/escritura
   * (NAS) : Vínculo dedicado de 1 GB

**Requisitos de software**

* Oracle Java JRE 1.7 o posterior.

### Instalación y configuración de Offline Packager {#install-and-configure-offline-packager}

Para instalar Offline Packager, siga estos pasos:

1. Descargue el software Java SE del [sitio de Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) y siga las instrucciones de instalación.
1. Extraiga el archivo de Adobe Primetime - Offline Packager 1.4, `Primetime- OfflinePackager-1-4-0-b206-12042014.zip`, en su disco.

Consulte el documento Introducción a Paquetes sin conexión de Primetime para obtener los detalles de configuración disponibles [aquí](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

## Recursos útiles {#helpful-resources}

* Consulte la documentación de ayuda completa en la página [Aprendizaje y asistencia de Adobe Primetime](https://helpx.adobe.com/support/primetime.html).