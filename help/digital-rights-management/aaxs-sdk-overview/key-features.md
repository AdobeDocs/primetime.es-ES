---
title: Características principales
description: Características principales
copied-description: true
exl-id: e17b7ce8-a408-4731-b63e-9d25feac2cdc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 0%

---

# Características principales {#key-features}

Adobe Access proporciona estas características clave:

* **Compatibilidad con flujo HLS (requiere Adobe Primetime):** Utilice DRM de acceso a Adobe con contenido HLS que se pueda transmitir a cualquier plataforma compatible con Flash o Adobe Primetime (como Desktop, iOS y Android).
* **Compatibilidad con aplicaciones iOS nativas (requiere Adobe Primetime):** Utilice DRM de acceso a Adobe para proteger el vídeo en las aplicaciones de iOS.
* **Compatibilidad con aplicaciones Android nativas (requiere Adobe Primetime):** Utilice DRM de acceso a Adobe para proteger el vídeo en las aplicaciones de Android.
* **Transmisión protegida en Xbox (requiere Adobe Primetime)**.
* **Entrega remota de claves iOS (requiere Adobe Primetime):** Compatibilidad para entregar claves iOS remotas a través de un servidor de claves de varios inquilinos, denominado Servidor de claves de acceso a Adobe.
* **Protección de contenido persistente:** El contenido permanece protegido en toda la cadena de distribución. Una vez empaquetado el contenido, permanece protegido en todo momento, y partes de él solo se descifran en el momento de la reproducción y de acuerdo con las reglas de uso.
* Dado que el contenido está empaquetado con reglas de uso e información de licencias, la protección siempre se desplaza con el contenido. Si los consumidores sin licencia intentan reproducir el contenido, la directiva incrustada en el contenido los redirige para que puedan adquirir una licencia válida para el contenido.
* **Reproducción segura de contenido protegido: **Se utilizan esquemas de cifrado probados para proteger el contenido de la reproducción no autorizada.
* **Reglas de uso flexibles:** Las reglas de uso determinan cómo los consumidores pueden utilizar el contenido protegido. Las reglas de uso admitidas por Adobe Access permiten varios modelos de negocio diferentes, incluidos servicios de pago por visión, alquiler de películas, suscripciones o servicios financiados con publicidad. Las reglas de uso se especifican mediante la directiva que se incrusta en el contenido durante el empaquetado o el servidor de licencias las puede especificar durante la adquisición de la licencia.
* **Protección de salida:** Los controles de protección de la salida pueden utilizarse para aplicar esquemas de protección como HDCP, CGMS-A o Rovi (anteriormente Macrovision) ACP. Esto permite proteger la salida de contenido a través de salidas digitales (por ejemplo, HDMI, DVI y UDI) y analógicas (por ejemplo, S-Video y vídeo en componentes).

   Puede especificar opciones de protección de salida en la directiva que cree para el contenido, lo que permite o deniega el acceso al contenido en función de las capacidades de protección de salida de un dispositivo. Por ejemplo, puede especificar que la protección de salida no sea necesaria para determinado contenido, sino que requiera protección de salida para el contenido de vídeo premium, lo que evita la salida de contenido en sistemas operativos que carecen de esta capacidad.

   Aunque estas reglas se aplican de forma coherente en todas las plataformas, actualmente solo es posible activar de forma segura la protección de salida en las plataformas Windows.

* **Compatibilidad con flujo dinámico: **Utilice la función de flujo dinámico del HTTP Dynamic Streaming de Flash Media Server o Adobe para proteger el contenido codificado a varias velocidades de bits. El streaming dinámico utiliza un flujo de vídeo que ajusta dinámicamente la velocidad de bits y la calidad de reproducción en función del ancho de banda disponible, lo que proporciona una experiencia de usuario mejorada. El acceso a Adobe permite utilizar la misma clave y licencia de cifrado de contenido en las distintas codificaciones del mismo recurso.
* **Visualización sin conexión:** El cliente de tiempo de ejecución de Adobe AIR permite a los consumidores descargar y almacenar contenido para su visualización posterior, independientemente de si el equipo permanece conectado a Internet o no.
* **Licencias basadas en identidad:** Vincula permisos a identidades de usuarios, lo que requiere que los consumidores se autentiquen a sí mismos (proporcionando un ID de usuario y una contraseña) para obtener acceso al contenido. Las licencias basadas en identidad requieren que la parte que desarrolla la aplicación cliente implemente la autenticación de usuario como parte del flujo de trabajo de adquisición de licencias.
* **Encadenamiento de licencias:** Permite a los consumidores ampliar la vida útil de todo su contenido mediante la renovación de una sola licencia raíz. Uno de los usos principales de la encadenamiento de licencias es para modelos de negocio basados en suscripciones, donde, al final de un período de suscripción, las licencias a grandes cantidades de archivos de contenido se pueden renovar simplemente renovando la licencia raíz.

   Las licencias raíz y hoja están enlazadas al equipo del consumidor. La licencia hoja contiene el CEK y una referencia a la licencia raíz. La licencia raíz puede ampliar los derechos otorgados en la licencia hoja. Por ejemplo, un consumidor puede tener licencias hoja para 50 fragmentos de contenido que caducarán al final de un periodo de suscripción determinado. Si el consumidor descarga una nueva licencia raíz con una nueva fecha de caducidad, los 50 fragmentos de contenido se pueden reproducir hasta que caduque la licencia actualizada.

   Adobe Access 2.0 introdujo el encadenamiento de licencias en el que las licencias hoja y raíz están enlazadas a un equipo específico. Adobe Access 3.0 presenta una forma mejorada de encadenamiento de licencias, en la que una hoja está enlazada a una licencia raíz y sólo la licencia raíz está enlazada a un equipo o dominio específico. Leer *Encadenamiento de licencias mejorado* in *Uso del SDK de acceso a Adobe para proteger el contenido*.

* **Rotación de clave:** Durante el empaquetado habitual, el contenido se cifra utilizando la clave de cifrado de contenido (CEK) y el cliente obtiene una licencia que lo contiene para consumirlo. Cuando la rotación de claves está habilitada, la clave utilizada para cifrar el contenido se puede cambiar de modo que la clave solo se utilice para cifrar una parte del contenido. Leer *Rotación de clave* in *Uso del SDK de acceso a Adobe para proteger el contenido*.

* **Licencias fuera de banda:** Con Adobe Access, es posible implementar un flujo de trabajo en el que los clientes obtienen licencias generadas previamente fuera de banda, lo que elimina la necesidad de implementar un servidor de licencias.
* **Compatibilidad con dominios:** Como alternativa al enlace de una licencia a un dispositivo específico, Acceso a Adobe admite el enlace de licencias a un dominio. Varios dispositivos pueden unirse a un dominio y recibir un token de dominio que permite mover licencias entre dispositivos del dominio. Leer *Registro de dominios* in *Uso del SDK de acceso a Adobe para proteger el contenido*.

* **Cifrado parcial:** Especifica si se deben cifrar todos los fotogramas o sólo un subconjunto de ellos. Existen tres niveles de cifrado: bajo, medio y alto. La reducción del nivel de cifrado puede disminuir la sobrecarga de CPU en los equipos de gama baja.
* **Empaquetado de contenido desconectado:** El empaquetado de contenido no requiere una conexión de red con el servidor de licencias. Esto permite operaciones back-end seguras al limitar la exposición de contenido comprimido que aún no se ha protegido.
* **Controlar la reversión del reloj: **Adobe Access proporciona un cálculo seguro y preciso del tiempo para detectar la reversión del reloj en el equipo cliente. Esto aplica derechos relacionados con el acceso al contenido durante una cantidad de tiempo específica y evita que los consumidores subviertan los derechos de acceso al alterar la hora en su equipo.
* **Individualización**: permite enlazar contenido a un equipo concreto.
* **Lista de permitidos de la aplicación:** Permite al tiempo de ejecución del cliente garantizar que el contenido protegido solo se reproduce dentro de un SWF autorizado o una aplicación de AIR.
* **Revocación de clientes comprometidos: **Se puede revocar el software cliente comprometido. Si se determina que el Flash Player o el tiempo de ejecución de Adobe AIR se han visto comprometidos, se puede rechazar el servicio a esos clientes hasta que actualicen a una versión más reciente y segura del software cliente.
* **Varias políticas para el mismo archivo de vídeo: **Un solo fragmento de contenido de vídeo puede tener varias políticas incrustadas durante el empaquetado. Al emitir una licencia, el servidor de licencias puede decidir cuál de las políticas utilizar, lo que permite a un distribuidor de contenido utilizar el mismo archivo protegido para diferentes modelos de negocio (como alquiler y venta electrónica).
