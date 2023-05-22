---
description: El streaming a través de Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o de la reproducción de una transmisión en tiempo real de un usuario significa que la reproducción remota podría no tener la calidad del contenido reproducido localmente.
title: Formato AC-3 5.1
exl-id: dcc43c1b-b9ce-44a1-a4c9-50ccfc5d572d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# Formato AC-3 5.1{#ac-format}

El streaming a través de Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o de la reproducción de una transmisión en tiempo real de un usuario significa que la reproducción remota podría no tener la calidad del contenido reproducido localmente.

Primetime no puede protegerse de errores como una interrupción del ISP o una desconexión del cable. Sin embargo, el streaming de Primetime proporciona protección contra failover para proteger la reproducción de ciertos fallos del servidor remoto o fallos de funcionamiento, lo que mejora la experiencia del usuario. TVSDK implementa la protección contra fallos para minimizar las interrupciones en la reproducción y conseguir una reproducción perfecta a pesar de los problemas de transmisión. El reproductor de vídeo cambia automáticamente a un conjunto de medios de copia de seguridad cuando no están disponibles representaciones o fragmentos completos.

El formato Audio Codec 3 (AC-3, también conocido como Dolby Digital®) 5.1, permite a los proveedores de contenido comprimir el tamaño de archivos de audio multicanal sin afectar la calidad del sonido. AC-3 es un formato 5.1, lo que significa que proporciona cinco canales de ancho de banda completo para una mejor experiencia de usuario.

Para obtener más información, consulte [Dolby Digital 5.1](https://www.dolby.com/us/en/technologies/dolby-digital.html).

>[!IMPORTANT]
>
>La versión 1.4 de TVSDK admite el formato AC-3 5.1 solo en Amazon FireTV.

TVSDK admite las siguientes funciones de AC-3 5.1:

* Audio envolvente AC-3
* Flujos mixtos/no mixtos para el tipo de audio envolvente
* Posibilidad de consultar el dispositivo para ver si el códec de audio envolvente está disponible en el dispositivo.

   Los resultados determinan qué tipo de códec de audio preferido se selecciona. Se descarta el manifiesto del tipo de códec de audio que el dispositivo no va a utilizar. Por ejemplo, si se ha seleccionado el formato AC-3, no se tienen en cuenta los perfiles con el formato Advanced Audio Coding (AAC).
* Modo de paso a través

   En el modo de paso a través, en lugar de descodificar los medios del formato AC-3 5.1 a un formato de modulación de código de pulso multicanal (PCM), el TVSDK se modifica o no modifica (según el dispositivo) los medios Dolby del Decodificador. Este medio se envía al dispositivo de audio (altavoz o receptor) para que el dispositivo de audio pueda descodificar y reproducir el flujo Dolby surround.

TVSDK admite las funciones AC-3 5.1 solo en el dispositivo Amazon Fire TV de primera generación.

No se admiten las siguientes funciones de AC-3 5.1:

* Audio AAC multicanal
* ABR en diferentes códecs (AAC - AC3)

## Selección de medios admitidos {#section_E1DFA1F472EA4BDE846C71A3343E275A}

Este es el flujo de trabajo típico que se produce cuando TVSDK encuentra un manifiesto con medios AC-3 y AAC:

1. TVSDK consulta qué códec admite el dispositivo.
1. Se selecciona el códec con la calidad más alta.

   El orden de calidad es AC-3 > AAC.
1. TVSDK ignora los perfiles con otros tipos de códec de audio.

>[!TIP]
>
>La aplicación no puede obtener información sobre perfiles ignorados.

## Determinación del modo de salida {#section_64145D9824594C36AADBF0482C528767}

Al procesar medios AC-3, si un dispositivo Android está conectado al sistema de altavoces, la decisión de reproducir contenido en modo surround o estéreo depende de cómo esté configurado el dispositivo.

|  | Sonido envolvente | Altavoz estéreo |
|---|---|---|
| Configuración del dispositivo Dolby activado (o automático) | Configuración del dispositivo Dolby activado (o automático) | Modo estéreo |
| Configuración del dispositivo Dolby desactivado | Modo estéreo | Modo estéreo |
