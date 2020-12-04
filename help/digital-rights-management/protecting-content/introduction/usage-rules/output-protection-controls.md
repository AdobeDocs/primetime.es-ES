---
seo-title: Controles de protección de salida
title: Controles de protección de salida
uuid: a0518392-cd33-4ef0-834c-f90145a9b421
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---


# Controles de protección de salida{#output-protection-controls}

El parámetro de protección de salida controla si la salida a dispositivos de procesamiento externos está protegida. Puede especificar restricciones para salidas analógicas y digitales de forma independiente.

Controla si se debe restringir la salida a dispositivos de procesamiento externos. Un dispositivo externo se define como cualquier dispositivo de audio o vídeo que no esté incrustado en el equipo. Las pantallas integradas, como en los equipos portátiles, no se consideran externas en el escenario de controles de protección de salida.

Todos los tipos de conexión a través del aire (OTA) están enumerados de forma predeterminada, pero se pueden permitir de forma explícita si es necesario. Las conexiones OTA admitidas incluyen: Miracast, AirPlay, DLNA y WIDI.

**Protección de salida basada en resolución: (Disponible a partir de la versión 5.3.) ** Esto proporciona protección de salida basada en el recuento vertical de píxeles del contenido, lo que permite especificar una serie de requisitos de protección en función de los recuentos verticales de píxeles.

Existen las siguientes opciones y niveles de cumplimiento:

| Opción | Compatible con dispositivos analógicos | Compatible con dispositivos digitales |
|---|---|---|
| **Requerido** — La protección de salida Analog Copy Protection (ACP) o Copy Generation Management System - Analog (CGMS-A) debe estar activada para poder reproducir contenido en un dispositivo externo. Los clientes de Primetime DRM deben habilitar la protección de salida mediante ACP o CGMS-A. En dispositivos que admiten ambos, los clientes Primetime DRM 3.0 intentan habilitar ambos. Sin embargo, solo se debe habilitar uno para reproducir el contenido. | SÍ | SÍ |
| **ACP requerido** — Se requiere protección de salida ACP. No se permite la reproducción en CGMS-A. Los clientes de Primetime DRM 2.0 no admiten esta opción. Si se configura, un cliente Primetime DRM 2.0 se comporta como si se hubiera especificado la opción &quot;Sin reproducción&quot;. | SÍ | - |
| **Usar si está disponible** — Intente habilitar la protección de salida ACP y CGMS-A si está disponible y permitir la reproducción si no está disponible. Los clientes de Primetime DRM 3.0 intentan habilitar tanto ACP como CGMS-A, si es posible. Los clientes de Primetime DRM 2.0 solo intentan activar tanto ACP como CGMS-A. Por ejemplo, el cliente Primetime DRM intenta habilitar tanto ACP como CGMS-A. Si el intento se realiza correctamente, la otra opción no se puede activar. Si el intento falla, se realiza un segundo intento para habilitar la otra opción. Incluso si ambos intentos fallan, el contenido se reproduce de todos modos. | SÍ | SÍ |
| **Usar ACP si está disponible** — Intente habilitar la protección de salida ACP si está disponible, pero permita la reproducción si no está disponible. La protección no está disponible en CGMS-A. Los clientes de Primetime DRM 2.0 no admiten esta opción. Si se configura, un cliente Primetime DRM 2.0 se comporta como si se hubiera especificado la opción &quot;Sin protección&quot;. | SÍ | - |
| **Utilizar CGMS-A si está disponible **— Intente activar la protección de salida CGMS-A si está disponible, pero permita la reproducción si no está disponible. La protección no está disponible en los países ACP. Los clientes de Primetime DRM 2.0 no admiten esta opción. Si se configura, un cliente Primetime DRM 2.0 se comporta como si se hubiera especificado la opción &quot;Sin protección&quot;. | SÍ | - |
| **Sin protección** — No se aplica ninguna habilitación de protección de salida para salidas analógicas y digitales. | SÍ | SÍ |
| **Sin reproducción** — No permita la reproducción en un dispositivo externo para salidas analógicas y digitales. | SÍ | SÍ |

>[!NOTE]
>
>Aunque estas reglas se aplican de manera consistente en todas las plataformas, solo puede activar de forma segura la protección de salida en las plataformas Windows. En otras plataformas, como Macintosh y Linux, no hay funciones de sistema operativo compatibles disponibles para aplicaciones de terceros.

Ejemplo de caso de uso: Algunos contenidos pueden exigir controles de protección de salida y, por lo tanto, el distribuidor de contenido puede establecer el nivel de protección. Si se especifica &quot;Requerido&quot; y se intenta reproducir en un Macintosh, el cliente no reproduce contenido en dispositivos externos. El contenido se puede reproducir en monitores internos.

Si se especifica &quot;Requerido&quot; y se intenta reproducir en Linux, el cliente no reproduce contenido en ningún dispositivo porque no puede diferenciar entre dispositivos internos y externos.

Si especifica &quot;Usar si está disponible&quot;, la protección de salida se activa siempre que sea posible. Por ejemplo, en sistemas Windows que admiten el protocolo de protección de salida certificado (COPP), el contenido se pasa con protección de salida a una pantalla externa. Este ejemplo se conoce a veces como *`selectable output control`*.
