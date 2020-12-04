---
seo-title: Características principales
title: Características principales
uuid: bee91fd7-a335-4881-abad-8972f28630d5
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 0%

---


# Características principales{#key-features}

Adobe Primetime DRM proporciona estas funciones clave:

* **Compatibilidad con flujo continuo HLS (requiere Adobe Primetime):** utilice DRM de Primetime con contenido HLS que se pueda transmitir a cualquier plataforma admitida por Flash o Adobe Primetime (como Escritorio, iOS y Android).
* **Compatibilidad nativa con aplicaciones iOS (requiere Adobe Primetime):** utilice Primetime DRM para proteger vídeo en sus aplicaciones iOS.
* **Compatibilidad nativa con aplicaciones de Android (requiere Adobe Primetime):** utilice Primetime DRM para proteger vídeo en sus aplicaciones de Android.
* **Flujo protegido en Xbox (requiere Adobe Primetime)**.
* **Envío de clave remota de iOS (requiere Adobe Primetime):** compatibilidad con la entrega de claves remotas de iOS a través de un servidor de claves de varios usuarios, denominado Primetime DRM Key Server.
* **Protección de contenido persistente:** El contenido permanece protegido en toda la cadena de distribución. Una vez empaquetado el contenido, permanece protegido en todo momento y partes del mismo solo se descifran en el momento de la reproducción y de acuerdo con las reglas de uso.
* Dado que el contenido está empaquetado con reglas de uso e información de licencias, la protección siempre viaja con el contenido. Si los consumidores sin licencia intentan reproducir el contenido, la política incrustada en el contenido los redirige para que puedan adquirir una licencia válida para el contenido.
* **Reproducción segura de contenido protegido:los esquemas de encriptación** comprobados se utilizan para proteger el contenido de la reproducción no autorizada.
* **Reglas de uso flexibles:las reglas** de uso determinan cómo pueden utilizar el contenido protegido los consumidores. Las reglas de uso admitidas por Primetime DRM permiten varios modelos comerciales diferentes, incluidos el pago por vista, el alquiler de películas, suscripciones o servicios financiados con publicidad. Las reglas de uso están especificadas por la directiva que incruste en el contenido durante el empaquetado o bien pueden especificarlas el servidor de licencias durante la adquisición de la licencia.
* **Protección de salida:los controles de protección de** salida pueden utilizarse para interactuar con sistemas de protección como HDCP, CGMS-A o Rovi (anteriormente Macrovision) ACP. Esto puede ayudar a proteger la salida de contenido mediante salidas digitales (por ejemplo, HDMI, DVI y UDI) y analógicas (por ejemplo, S-Video y Vídeo en componentes).

   Puede especificar opciones de protección de salida en la directiva que cree para el contenido, permitiendo o denegando el acceso al contenido en función de las capacidades de protección de salida de un dispositivo. Por ejemplo, puede especificar que la protección de salida no es necesaria para cierto contenido, pero requiere protección de salida para el contenido de vídeo premium, lo que evita la salida de contenido en sistemas operativos que carecen de esta capacidad.

   Aunque estas reglas se aplican de manera consistente en todas las plataformas, actualmente solo es posible activar de forma segura la protección de salida en las plataformas Windows.

* **Compatibilidad con flujo continuo dinámico:** utilice la función de flujo continuo dinámico de Flash Media Server o HTTP Dynamic Streaming de Adobe para proteger el contenido codificado a varias velocidades de bits. El flujo dinámico utiliza un flujo de vídeo que ajusta dinámicamente la velocidad de bits y la calidad de reproducción en función del ancho de banda disponible, lo que proporciona una experiencia de usuario mejorada. Primetime DRM permite utilizar la misma clave de cifrado de contenido y la misma licencia en las diferentes codificaciones del mismo recurso.
* **Visualización sin conexión:** El cliente de tiempo de ejecución de Adobe AIR permite a los consumidores descargar y almacenar contenido para su visualización posterior, independientemente de si el equipo permanece conectado a Internet o no.
* **Licencias basadas en la identidad:** vincula permisos a identidades de usuario, lo que requiere que los consumidores se autentiquen (proporcionando un ID de usuario y una contraseña) para obtener acceso al contenido. La licencia basada en la identidad requiere que la parte que desarrolla la aplicación cliente implemente la autenticación de usuarios como parte del flujo de trabajo de adquisición de licencias.
* **encadenado de licencias:** permite a los consumidores ampliar la vida de todo su contenido renovando una única licencia de raíz. Uno de los usos principales de la encadenación de licencias es para modelos empresariales basados en suscripciones, donde, al final de un período de suscripción, las licencias para una gran cantidad de archivos de contenido se pueden renovar simplemente renovando la licencia raíz.

   Las licencias de raíz y hoja están enlazadas al equipo del consumidor. La licencia de hoja contiene el CEK y una referencia a la licencia de raíz. La licencia raíz puede ampliar los derechos otorgados en la licencia de hoja. Por ejemplo, un consumidor puede tener licencias de hoja para 50 fragmentos de contenido que caducan al final de un período de suscripción determinado. Si el consumidor descarga una nueva licencia raíz con una nueva fecha de caducidad, se pueden reproducir las 50 partes de contenido hasta que caduque la licencia actualizada.

   Primetime DRM 2.0 introdujo la formación de licencias en la que tanto las licencias de hoja como las de raíz están enlazadas a una máquina específica. Primetime DRM 3.0 introduce una forma mejorada de encadenamiento de licencias, en la que una hoja está enlazada a una licencia raíz y solo la licencia raíz está enlazada a un equipo o dominio específico. Lea *Encadenado de licencia mejorado* en *Uso del SDK de DRM de Adobe Primetime para la protección de contenido*.

* **Rotación de clave:** durante el empaquetado típico, el contenido se cifra mediante la clave de cifrado de contenido (CEK) y el cliente obtiene una licencia que contiene el CEK para consumir el contenido. Cuando se habilita la rotación de claves, la clave utilizada para cifrar el contenido se puede cambiar para que la clave se utilice solamente para cifrar una parte del contenido. Lea *Rotación de clave* en *Uso del SDK de DRM de Adobe Primetime para proteger contenido*.

* **Licencias fuera de banda:** Con Primetime DRM, es posible implementar un flujo de trabajo en el que los clientes obtienen licencias pregeneradas fuera de banda, eliminando la necesidad de implementar un servidor de licencias.
* **Compatibilidad con dominios:** como alternativa a enlazar una licencia a un dispositivo específico, Primetime DRM admite el enlace de licencias a un dominio. Es posible que varios dispositivos se unan a un dominio y reciban un token de dominio que permite mover licencias entre dispositivos del dominio. Lea *Registro de dominio* en *Uso del SDK de DRM de Adobe Primetime para la protección de contenido*.

* **Cifrado parcial:** especifica si todos los marcos, o solo un subconjunto de marcos, deben cifrarse. Existen tres niveles de cifrado: baja, media y alta. La reducción del nivel de encriptación puede reducir el overhead de la CPU en los equipos de gama baja.
* **Empaquetado de contenido desconectado:el empaquetado** de contenido no requiere una conexión de red al servidor de licencias. Esto permite operaciones seguras de back-end al limitar la exposición de contenido comprimido que aún no se ha protegido.
* **Control de la reversión del reloj: **Primetime DRM proporciona el cálculo seguro y preciso del tiempo para detectar la reversión del reloj en el equipo cliente. Esto impone derechos relacionados con el acceso al contenido durante una cantidad de tiempo específica y evita que los consumidores subviertan los derechos de acceso al alterar la hora en su equipo.
* **Individualización**: Permite enlazar contenido a un equipo en particular.
* **Lista de permitidos de la aplicación:** permite al tiempo de ejecución del cliente garantizar que el contenido protegido solo se reproduce en una aplicación SWF o AIR autorizada.
* **Revocación de clientes comprometidos: el software cliente** comprometido puede ser revocado. Si se determina que el tiempo de ejecución de Flash Player o Adobe AIR se ha visto comprometido, el servicio se puede rechazar a esos clientes hasta que se actualicen a una versión más nueva y segura del software cliente.
* **Varias directivas para el mismo archivo de vídeo:** un solo fragmento de contenido de vídeo puede tener varias directivas incrustadas durante el empaquetado. Al expedir una licencia, el servidor de licencias puede decidir qué políticas utilizar, lo que permite que un distribuidor de contenido utilice el mismo archivo protegido para distintos modelos comerciales (como alquiler y venta electrónica).