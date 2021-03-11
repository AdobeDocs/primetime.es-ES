---
description: Puede utilizar la API Objective-C de Primetime Player para personalizar el comportamiento del reproductor.
title: Clases del reproductor multimedia
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# Clases del reproductor de contenidos {#media-player-classes}

Puede utilizar la API Objective-C de Primetime Player para personalizar el comportamiento del reproductor.

Estas clases describen el reproductor de contenidos y sus recursos.

| Clase | Descripción |
|---|---|
| PTABRControlParameters | Encapsula todos los parámetros de control de velocidad de bits adaptables. Los parámetros admitidos son:<ul><li>minBitRate</li><li>maxBitRate</li><li>initialBitRate</li></ul> |
| PTDefaultMediaPlayerClientFactory | Implementación predeterminada de PTMediaPlayerClientFactory en TVSDK. Proporciona las instancias availablePTOpportunityResolver, PTContentResolver y PTAdPolicySelector . |
| PTMediaPlayer | Define el componente raíz para el marco del Reproductor de Primetime. Las aplicaciones crean una instancia de esta clase para reproducir un contenido multimedia. Este componente envía notificaciones para informar a la aplicación del estado del reproductor en cualquier momento. |
| PTMediaPlayerClientFactory | Protocolo que describe los métodos que debe implementar una fábrica de cliente de reproductor de medios personalizada para proporcionar las instancias PTOpportunityResolver , PTContentResolver y PTAdPolicySelector disponibles. |
| PTMediaPlayerItem | Representa un medio de audio y vídeo específico. |
| PTMediaPlayerView | Gestiona el componente de vista de la estructura del Reproductor de Primetime. |
| PTMediaProfile | Representa el perfil de un único flujo en la lista de reproducción de variantes. |
| PTMediaSelectionOption | Representa un recurso de medios audiovisuales para dar cabida a diferentes preferencias de idioma, requisitos de accesibilidad o configuraciones de aplicación personalizadas. Tipos de opciones válidas:<ul><li>Subtítulos (PTMediaSelectionOptionTypeSubtitle)</li><li>Audio alternativo (PTMediaSelectionOptionTypeAudio)</li><li>Subtítulos (PTMediaSelectionOptionTypeCC)</li><li>Sin definir (PTMediaSelectionOptionTypeUndefined)</li></ul> |
| PTOpportunityResolver, clase,protocolo PTOpportunityResolver | Clase utilizada para procesar señales in-manifest que se utilizarán como ubicaciones para el proceso de toma de decisiones de anuncios de Adobe Primetime. |
| PTOpportunityResolverDelegate | Protocolo que describe los métodos que debe utilizar la resolución de oportunidad personalizada ( PTOpportunityResolver ) para comunicar al delegado el estado de la resolución de la oportunidad. |
| PTSDK | Describe la versión de TVSDK y sus capacidades. |
| PTSDKConfig | Expone la configuración global de TVSDK y permite que una aplicación se suscriba a etiquetas HLS personalizadas. |
| PTTextStyleRule | Define constantes que representan claves de atributo de estilo de texto que forman el diccionario de reglas. |
