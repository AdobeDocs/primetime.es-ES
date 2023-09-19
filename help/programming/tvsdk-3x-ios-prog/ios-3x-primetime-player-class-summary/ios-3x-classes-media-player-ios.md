---
description: Puede utilizar la API Objective-C del reproductor Primetime para personalizar el comportamiento del reproductor.
title: Clases de reproductor multimedia
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# Clases de reproductor multimedia {#media-player-classes}

Puede utilizar la API Objective-C del reproductor Primetime para personalizar el comportamiento del reproductor.

Estas clases describen el reproductor de contenidos y sus recursos.

| Clase | Descripción |
|---|---|
| PTABRControlParameters | Encapsula todos los parámetros de control de velocidad de bits adaptable. Los parámetros admitidos son:<ul><li>minBitRate</li><li>maxBitRate</li><li>initialBitRate</li></ul> |
| PTDefaultMediaPlayerClientFactory | Implementación predeterminada de PTMediaPlayerClientFactory en TVSDK. Proporciona las instancias PTOportunityResolver, PTContentResolver y PTAdPolicySelector disponibles. |
| PTMediaPlayer | Define el componente raíz del marco de trabajo del Reproductor de Primetime. Las aplicaciones crean una instancia de esta clase para reproducir un contenido. Este componente envía notificaciones para que la aplicación conozca el estado del reproductor en cualquier momento. |
| PTMediaPlayerClientFactory | Protocolo que describe los métodos que un generador de cliente de reproductor de medios personalizado debe implementar para proporcionar las instancias de PTOportunityResolver, PTContentResolver y PTAdPolicySelector disponibles. |
| PTMediaPlayerItem | Representa un medio de audio y vídeo específico. |
| PTMediaPlayerView | Administra el componente de vista del marco de trabajo del reproductor de Primetime. |
| PTMediaProfile | Representa el perfil de un solo flujo en la lista de reproducción de variante. |
| PTMediaSelectionOption | Representa un recurso de medios audiovisuales para adaptarse a diferentes preferencias de idioma, requisitos de accesibilidad o configuraciones de aplicación personalizadas. Tipos de opciones válidos:<ul><li>Subtítulos (PTMediaSelectionOptionTypeSubtitle)</li><li>Audio alternativo (PTMediaSelectionOptionTypeAudio)</li><li>Subtítulos opcionales (PTMediaSelectionOptionTypeCC)</li><li>Indefinido (PTMediaSelectionOptionTypeUndefined)</li></ul> |
| PTOportunityResolver, clase, PTOportunityResolver, protocolo | Clase utilizada para procesar señales en manifiesto que se utilizarán como ubicaciones para el proceso de Adobe Primetime y decisiones. |
| PTOportunityResolverDelegate | Protocolo que describe los métodos que debe utilizar el solucionador de oportunidades personalizado ( PTOportunityResolver ) para comunicar al delegado el estado de la resolución de la oportunidad. |
| PTSDK | Describe la versión de TVSDK y sus funcionalidades. |
| PTSDKConfig | Expone la configuración global de TVSDK y permite que una aplicación se suscriba a etiquetas HLS personalizadas. |
| PTextStyleRule | Define constantes que representan claves de atributo de estilo de texto que forman el diccionario de reglas. |
