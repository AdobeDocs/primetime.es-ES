---
title: Controles de protección de salida
description: Controles de protección de salida
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---

# Controles de protección de salida{#output-protection-controls}

El parámetro de protección de salida controla si la salida a dispositivos de renderización externos está protegida. Puede especificar restricciones para las salidas analógicas y digitales de forma independiente.

Controla si la salida a dispositivos de procesamiento externos debe restringirse. Un dispositivo externo se define como cualquier dispositivo de vídeo o audio que no esté incrustado en el equipo. Las pantallas integradas, como en los equipos portátiles, no se consideran externas en el escenario de los controles de protección de salida.

Los tipos de conexión Over the Air (OTA) están incluidos en la lista de bloques de forma predeterminada, pero se pueden incluir explícitamente en la lista de permitidos si es necesario. Las conexiones OTA admitidas incluyen: Miracast, AirPlay, DLNA y WIDI.

**Protección de salida basada en resolución: (disponible a partir de la versión 5.3). ** Esto proporciona protección de salida en función del recuento de píxeles verticales del contenido, lo que permite especificar una variedad de requisitos de protección en función del recuento de píxeles verticales.

Están disponibles las siguientes opciones/niveles de aplicación:

| Opción | Admitido en dispositivos analógicos | Admitido en dispositivos digitales |
|---|---|---|
| **Requerido** — Protección de copia analógica (ACP) o Sistema de gestión de generación de copias: la protección de salida analógica (CGMS-A) debe habilitarse para reproducir contenido en un dispositivo externo. Los clientes de DRM de Primetime deben habilitar la protección de salida mediante ACP o CGMS-A. En dispositivos compatibles con ambos, los clientes de Primetime DRM 3.0 intentan habilitar ambos. Sin embargo, solo uno debe estar habilitado para reproducir el contenido. | SÍ | SÍ |
| **ACP Necesario** — Se requiere protección de la salida ACP. No se permite la reproducción en CGMS-A. Los clientes de Primetime DRM 2.0 no admiten esta opción. Si se configura, un cliente DRM 2.0 de Primetime se comporta como si se hubiera especificado la opción &quot;Sin reproducción&quot;. | SÍ | - |
| **Usar si está disponible** — Intente activar la protección de salida ACP y CGMS-A si está disponible y permitir la reproducción si no está disponible. Los clientes de Primetime DRM 3.0 intentan habilitar tanto ACP como CGMS-A, si es posible. Los clientes de Primetime DRM 2.0 solo intentan habilitar ACP o CGMS-A. Por ejemplo, el cliente DRM de Primetime intenta habilitar ACP o CGMS-A. Si el intento se realiza correctamente, no se puede activar la otra opción. Si el intento falla, se realiza un segundo intento para habilitar la otra opción. Incluso si ambos intentos fallan, el contenido se reproduce de todos modos. | SÍ | SÍ |
| **Utilizar ACP si está disponible** — Intentar activar la protección de salida ACP si está disponible, pero permitir la reproducción si no está disponible. La protección no está disponible en CGMS-A. Los clientes de Primetime DRM 2.0 no admiten esta opción. Si se configura, un cliente DRM 2.0 de Primetime se comporta como si se hubiera especificado la opción &quot;Sin protección&quot;. | SÍ | - |
| **Usar CGMS-A si está disponible **— Intente activar la protección de salida CGMS-A si está disponible, pero permitir la reproducción si no está disponible. La protección no está disponible en ACP. Los clientes de Primetime DRM 2.0 no admiten esta opción. Si se configura, un cliente DRM 2.0 de Primetime se comporta como si se hubiera especificado la opción &quot;Sin protección&quot;. | SÍ | - |
| **Sin protección** — No se exige protección de salida para las salidas analógicas y digitales. | SÍ | SÍ |
| **Sin reproducción** — No permitir la reproducción en un dispositivo externo para salidas analógicas y digitales. | SÍ | SÍ |

>[!NOTE]
>
>Aunque estas reglas se aplican de forma coherente en todas las plataformas, solo puede activar de forma segura la protección de salida en las plataformas Windows. En otras plataformas, como Macintosh y Linux, no hay funciones de sistema operativo compatibles disponibles para aplicaciones de terceros.

Ejemplo de caso de uso: Algunos contenidos pueden aplicar controles de protección de salida y, por lo tanto, el distribuidor de contenido puede establecer el nivel de protección. Si se especifica &quot;Obligatorio&quot; y se intenta reproducir en un Macintosh, el cliente no reproduce contenido en dispositivos externos. El contenido puede reproducirse en monitores internos.

Si se especifica &quot;Obligatorio&quot; y se intenta la reproducción en Linux, el cliente no reproduce contenido en ningún dispositivo porque no puede diferenciar entre dispositivos internos y externos.

Si especifica &quot;Usar si está disponible&quot;, la protección de salida se activa siempre que sea posible. Por ejemplo, en sistemas Windows compatibles con el Protocolo de protección de salida certificada (COPP), el contenido se pasa con protección de salida a una pantalla externa. Este ejemplo se conoce a veces como *`selectable output control`*.
