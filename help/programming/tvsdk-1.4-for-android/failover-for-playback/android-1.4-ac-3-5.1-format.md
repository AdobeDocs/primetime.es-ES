---
description: La transmisión por Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o la reproducción de flujo de un visor significa que la reproducción remota puede no tener la calidad de medios reproducidos localmente.
seo-description: La transmisión por Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o la reproducción de flujo de un visor significa que la reproducción remota puede no tener la calidad de medios reproducidos localmente.
seo-title: Formato AC-3 5.1
title: Formato AC-3 5.1
uuid: d5e77bb5-ed51-4f9f-b34f-e9082f5ee4de
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Formato AC-3 5.1{#ac-format}

La transmisión por Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o la reproducción de flujo de un visor significa que la reproducción remota puede no tener la calidad de medios reproducidos localmente.

Primetime no puede protegerse de errores como una interrupción de ISP o una desconexión de cable. Sin embargo, el flujo de Primetime proporciona protección de conmutación por error para proteger la reproducción de determinados fallos de servidor remoto o fallos operativos, lo que ofrece una mejor experiencia a los visores. TVSDK implementa la protección de conmutación por error para minimizar las interrupciones de reproducción y lograr una reproducción sin problemas a pesar de los problemas de transmisión. El reproductor de vídeo cambia automáticamente a un conjunto de medios de copia de seguridad cuando no están disponibles representaciones o fragmentos completos.

El formato de códec de audio 3 (AC-3, también conocido como Dolby Digital®) 5.1, permite a los proveedores de contenido comprimir el tamaño de los archivos de audio multicanal sin perjudicar la calidad de sonido. AC-3 es un formato 5.1, lo que significa que proporciona cinco canales de ancho de banda completo para una experiencia de usuario más rica.

Para obtener más información, consulte [Dolby Digital 5.1](https://www.dolby.com/us/en/technologies/dolby-digital.html).

>[!IMPORTANT]
>
>La versión 1.4 de TVSDK admite el formato AC-3 5.1 únicamente en Amazon FireTV.

TVSDK admite las siguientes funciones AC-3 5.1:

* Audio envolvente AC-3
* Flujos mixtos/sin mezclar para el tipo de audio envolvente
* Posibilidad de consultar el dispositivo para ver si el códec de audio envolvente está disponible en el dispositivo.

   Los resultados determinan qué tipo de códec de audio preferido se selecciona. Se descarta el manifiesto con el tipo de códec de audio que el dispositivo no va a usar. Por ejemplo, si se ha seleccionado el formato AC-3, no se tendrán en cuenta los perfiles con el formato de codificación de audio avanzada (AAC).
* Modo de paso

   En el modo de paso, en lugar de descodificar los medios del formato AC-3 5.1 a un formato de modulación de código de impulso multicanal (PCM), el TVSDK se modifica o no se modifica (según el dispositivo) del medio Dolby desde el Decoder. Este medio se envía al dispositivo de audio (altavoz o receptor) para que el dispositivo de audio pueda descodificar y reproducir el flujo envolvente Dolby.

TVSDK admite las funciones AC-3 5.1 solo en el dispositivo Amazon Fire TV de primera generación.

No se admiten las siguientes funciones de AC-3 5.1:

* Audio AAC multicanal
* ABR en diferentes códecs (AAC - AC3)

## Selección de medios admitidos {#section_E1DFA1F472EA4BDE846C71A3343E275A}

Este es el flujo de trabajo típico que se produce cuando TVSDK encuentra un manifiesto con medios AC-3 y AAC:

1. TVSDK consulta qué códec puede admitir el dispositivo.
1. Se selecciona el códec con mayor calidad.

   El orden de calidad es AC-3 > AAC.
1. TVSDK ignora los perfiles con otros tipos de códec de audio.

>[!TIP]
>
>La aplicación no puede obtener información sobre perfiles ignorados.

## Determinación del modo de salida {#section_64145D9824594C36AADBF0482C528767}

Durante el procesamiento de medios AC-3, si un dispositivo Android está conectado al sistema de altavoces, la decisión de reproducir contenido en modo envolvente o estéreo depende de cómo se configure el dispositivo.

|  | Sonido envolvente | Altavoz estéreo |
|---|---|---|
| Configuración de dispositivo Dolby activado (o automático) | Configuración de dispositivo Dolby activado (o automático) | Modo estéreo |
| Configuración del dispositivo Dolby desactivado | Modo estéreo | Modo estéreo |

