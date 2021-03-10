---
title: Funciones principales
description: Funciones principales
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 0%

---


# Funciones principales {#key-features}

Adobe Access proporciona estas características clave:

* **Compatibilidad con transmisión por secuencias HLS (requiere Adobe Primetime):** Utilice DRM de acceso al Adobe con contenido HLS que se pueda transmitir a cualquier plataforma compatible con Flash o Adobe Primetime (como escritorio, iOS y Android).
* **Compatibilidad nativa con aplicaciones iOS (requiere Adobe Primetime):** use DRM de acceso a Adobe para proteger vídeo en sus aplicaciones iOS.
* **Compatibilidad nativa con aplicaciones de Android (requiere Adobe Primetime):** use DRM de acceso a Adobe para proteger vídeo en sus aplicaciones de Android.
* **Transmisión protegida en Xbox (requiere Adobe Primetime)**.
* **Entrega remota de claves de iOS (requiere Adobe Primetime):** compatibilidad con la entrega de claves de iOS remotas a través de un servidor de claves de varios inquilinos, denominado Servidor de claves de acceso a Adobe.
* **Protección de contenido persistente:** el contenido permanece protegido a lo largo de la cadena de distribución. Una vez empaquetado el contenido, permanece protegido en todo momento, y las partes de él solo se descifran en el momento de la reproducción y de acuerdo con las reglas de uso.
* Dado que el contenido está empaquetado con reglas de uso e información de licencias, la protección siempre viaja con el contenido. Si los consumidores sin licencia intentan reproducir el contenido, la política incrustada en el contenido los redirige para que puedan adquirir una licencia válida para el contenido.
* **Reproducción segura de contenido protegido: **Los esquemas de encriptación comprobados se utilizan para proteger el contenido de la reproducción no autorizada.
* **Reglas de uso flexibles:** las reglas de uso determinan cómo los consumidores pueden utilizar el contenido protegido. Las reglas de uso compatibles con el acceso a Adobe permiten varios modelos de negocio diferentes, incluidos el pago por visualización, el alquiler de películas, las suscripciones o los servicios financiados por publicidad. Las reglas de uso están especificadas por la directiva que incruste en el contenido durante el empaquetado o pueden especificarlas el servidor de licencias durante la adquisición de la licencia.
* **Protección de la salida:**  Los controles de protección de la salida pueden utilizarse para interactuar con sistemas de protección como HDCP, CGMS-A o Rovi (anteriormente Macrovision) ACP. Esto puede ayudar a proteger la salida de contenido sobre las salidas digitales (por ejemplo, HDMI, DVI y UDI) y analógicas (por ejemplo, S-Video y Component Video).

   Puede especificar opciones de protección de salida en la política que cree para el contenido, permitiendo o denegando el acceso al contenido en función de las capacidades de protección de salida de un dispositivo. Por ejemplo, puede especificar que no se requiera protección de salida para cierto contenido, pero que se requiera protección de salida para contenido de vídeo premium, lo que impide que el contenido se muestre en sistemas operativos que no tengan esta capacidad.

   Aunque estas reglas se aplican de manera consistente en todas las plataformas, actualmente solo es posible activar de forma segura la protección de salida en las plataformas Windows.

* **Compatibilidad con flujo dinámico: **Utilice la función de flujo dinámico del HTTP Dynamic Streaming de Flash Media Server o Adobe para proteger el contenido codificado a varias velocidades de bits. La transmisión dinámica utiliza un flujo de vídeo que ajusta dinámicamente la velocidad de bits y la calidad de reproducción en función del ancho de banda disponible, lo que proporciona una experiencia de usuario mejorada. Acceso a Adobe permite utilizar la misma clave de cifrado de contenido y licencia en las diferentes codificaciones del mismo recurso.
* **Visualización sin conexión:** el cliente de tiempo de ejecución de Adobe AIR permite a los consumidores descargar y almacenar contenido para su visualización posterior, independientemente de si el equipo permanece conectado a Internet o no.
* **Licencias basadas en identidad:**  vincula permisos a identidades de usuario, lo que requiere que los consumidores se autentiquen (proporcione un ID de usuario y una contraseña) para obtener acceso al contenido. La licencia basada en identidad requiere que la parte que desarrolla la aplicación cliente implemente la autenticación de usuario como parte del flujo de trabajo de adquisición de licencia.
* **encadenamiento de licencias:** permite a los consumidores ampliar la vida de todo su contenido renovando una única licencia raíz. Uno de los usos principales de la encadenación de licencias es para modelos empresariales basados en suscripciones, donde, al final de un periodo de suscripción, las licencias para un gran número de archivos de contenido se pueden renovar simplemente renovando la licencia raíz.

   Tanto las licencias de raíz como las de hoja están vinculadas al equipo del consumidor. La licencia de hoja contiene el CEK y una referencia a la licencia raíz. La licencia raíz puede ampliar los derechos otorgados en la licencia de hoja. Por ejemplo, un consumidor puede tener licencias de hoja para 50 fragmentos de contenido que caducan al final de un periodo de suscripción determinado. Si el consumidor descarga una nueva licencia raíz con una nueva fecha de caducidad, los 50 fragmentos de contenido se pueden reproducir hasta que caduque la licencia actualizada.

   Adobe Access 2.0 ha introducido la formación de licencias en la que tanto las licencias de hoja como las de raíz están vinculadas a un equipo específico. Adobe Access 3.0 presenta una forma mejorada de encadenamiento de licencias, en la que una hoja está enlazada a una licencia raíz, y solo la licencia raíz está enlazada a un equipo o dominio específico. Lea *Encadenado de licencias mejorado* en *Uso del SDK de acceso a Adobe para la protección de contenido*.

* **Rotación de clave:** durante el empaquetado típico, el contenido se cifra mediante la clave de cifrado de contenido (CEK) y el cliente obtiene una licencia que contiene el CEK para consumir el contenido. Cuando se habilita la rotación de claves, la clave utilizada para cifrar el contenido se puede cambiar para que la clave solo se utilice para cifrar una parte del contenido. Lea *Rotación de clave* en *Uso del SDK de acceso a Adobe para proteger contenido*.

* **Licencias fuera de banda:** con Acceso a Adobe, es posible implementar un flujo de trabajo en el que los clientes obtengan licencias pregeneradas fuera de banda, lo que elimina la necesidad de implementar un servidor de licencias.
* **Compatibilidad con dominios:** como alternativa a enlazar una licencia a un dispositivo específico, Adobe Access admite el enlace de licencias a un dominio. Es posible que varios dispositivos se unan a un dominio y reciban un token de dominio que permita que las licencias se movieran entre dispositivos del dominio. Lea *Registro de dominio* en *Uso del SDK de acceso a Adobe para proteger contenido*.

* **Cifrado parcial:** especifica si se deben cifrar todos los fotogramas, o solo un subconjunto de fotogramas. Hay tres niveles de encriptación: baja, media y alta. La reducción del nivel de encriptación puede disminuir la sobrecarga de CPU en las máquinas de gama baja.
* **Paquete de contenido desconectado:**  el paquete de contenido no requiere una conexión de red al servidor de licencias. Esto permite operaciones de back-end seguras al limitar la exposición de contenido comprimido que aún no se ha protegido.
* **Control de la reversión del reloj: **Adobe Access proporciona un cálculo seguro y preciso del tiempo para detectar la reversión del reloj en el equipo cliente. Esto impone derechos relacionados con el acceso al contenido durante una cantidad de tiempo específica y evita que los consumidores subviertan los derechos de acceso al modificar el tiempo en su equipo.
* **Individualización**: Permite enlazar contenido a un equipo en particular.
* **Lista de permitidos de la aplicación:** permite al tiempo de ejecución del cliente garantizar que el contenido protegido solo se reproduzca dentro de una aplicación SWF o AIR autorizada.
* **Revocación de clientes comprometidos: **Se puede revocar el software cliente comprometido. Si se determina que el tiempo de ejecución del Flash Player o Adobe AIR se ha visto comprometido, se puede denegar el servicio a esos clientes hasta que se actualicen a una versión más reciente y segura del software cliente.
* **Varias directivas para el mismo archivo de vídeo: **Un solo fragmento de contenido de vídeo puede tener varias políticas incrustadas durante el empaquetado. Al expedir una licencia, el servidor de licencias puede decidir cuál de las políticas utilizar, lo que permite a un distribuidor de contenido utilizar el mismo archivo protegido para diferentes modelos de negocio (como alquiler y venta electrónica).

