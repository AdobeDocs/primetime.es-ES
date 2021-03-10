---
title: Controles de protección de salida
description: Controles de protección de salida
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---


# Controles de protección de salida{#output-protection-controls}

El parámetro de protección de salida controla si la salida a dispositivos de renderización externos está protegida. Puede especificar restricciones para las salidas analógicas y digitales de forma independiente.

Controla si se debe restringir la salida a dispositivos de renderización externos. Un dispositivo externo se define como cualquier dispositivo de vídeo o audio que no esté incrustado en el equipo. Las pantallas integradas, como en los ordenadores portátiles, no se consideran externas en el escenario de controles de protección de salida.

Los tipos de conexión a través del aire (OTA) están enumerados de forma predeterminada, pero se pueden incluir explícitamente si es necesario. Las conexiones OTA admitidas incluyen: Miracast, AirPlay, DLNA y WIDI.

**Protección de salida basada en resolución: (Disponible a partir de la versión 5.3). ** Proporciona protección de salida basada en el recuento vertical de píxeles del contenido, lo que permite especificar una variedad de requisitos de protección en función de los recuentos verticales de píxeles.

Están disponibles las siguientes opciones y niveles de aplicación:

| Opción | Admitido en dispositivos analógicos | Compatible con dispositivos digitales |
|---|---|---|
| **Obligatorio** : la protección de salida de la copia analógica (ACP) o del sistema de gestión de la generación de copias (CGMS-A) debe estar activada para poder reproducir contenido en un dispositivo externo. Los clientes de Primetime DRM deben habilitar la protección de salida utilizando ACP o CGMS-A. En dispositivos que admiten ambos, los clientes de Primetime DRM 3.0 intentan habilitar ambos. Sin embargo, solo se debe activar una para reproducir el contenido. | SÍ | SÍ |
| **ACP Requerido** : se requiere protección de salida ACP. No se permite la reproducción en CGMS-A. Los clientes de Primetime DRM 2.0 no admiten esta opción. Si se configura, un cliente de Primetime DRM 2.0 se comporta como si se hubiera especificado la opción &quot;Sin reproducción&quot;. | SÍ | - |
| **Usar si está disponible** : intente habilitar la protección de salida ACP y CGMS-A si está disponible y permita la reproducción si no está disponible. Los clientes de Primetime DRM 3.0 intentan habilitar tanto ACP como CGMS-A, si es posible. Los clientes de Primetime DRM 2.0 solo intentan activar ACP o CGMS-A. Por ejemplo, el cliente Primetime DRM intenta habilitar tanto ACP como CGMS-A. Si el intento se realiza correctamente, la otra opción no se puede activar. Si el intento falla, se realiza un segundo intento para habilitar la otra opción. Incluso si ambos intentos fallan, el contenido se reproduce de todas formas. | SÍ | SÍ |
| **Utilice ACP si está disponible** : intente habilitar la protección de salida ACP si está disponible, pero permita la reproducción si no está disponible. La protección no está disponible en CGMS-A. Los clientes de Primetime DRM 2.0 no admiten esta opción. Si se configura, un cliente de Primetime DRM 2.0 se comporta como si se hubiera especificado la opción &quot;Sin protección&quot;. | SÍ | - |
| **Utilice CGMS-A si está disponible **: Intente habilitar la protección de salida de CGMS-A si está disponible, pero permita la reproducción si no está disponible. La protección no está disponible en los países ACP. Los clientes de Primetime DRM 2.0 no admiten esta opción. Si se configura, un cliente de Primetime DRM 2.0 se comporta como si se hubiera especificado la opción &quot;Sin protección&quot;. | SÍ | - |
| **Sin protección** : no se aplica ninguna habilitación de protección de salida para las salidas analógicas y digitales. | SÍ | SÍ |
| **Sin reproducción** : no permita la reproducción en un dispositivo externo para salidas analógicas y digitales. | SÍ | SÍ |

>[!NOTE]
>
>Aunque estas reglas se aplican de manera consistente en todas las plataformas, solo puede activar de forma segura la protección de salida en las plataformas Windows. En otras plataformas, como Macintosh y Linux, no hay funciones de sistema operativo compatibles disponibles para aplicaciones de terceros.

Ejemplo de caso de uso: Algunos contenidos pueden exigir controles de protección de salida y, por lo tanto, el distribuidor de contenido puede establecer el nivel de protección. Si se especifica &quot;Obligatorio&quot; y se intenta reproducir en un Macintosh, el cliente no reproduce contenido en dispositivos externos. El contenido se puede reproducir en monitores internos.

Si se especifica &quot;Obligatorio&quot; y se intenta reproducir en Linux, el cliente no reproduce contenido en ningún dispositivo porque no puede diferenciar entre dispositivos internos y externos.

Si especifica &quot;Usar si está disponible&quot;, la protección de salida se activa siempre que sea posible. Por ejemplo, en sistemas Windows que admiten el protocolo de protección de salida certificado (COPP), el contenido se pasa con protección de salida a una pantalla externa. Este ejemplo a veces se conoce como *`selectable output control`*.
