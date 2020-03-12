---
description: Puede utilizar la API Objective-C de Primetime Player para personalizar el comportamiento del reproductor.
seo-description: Puede utilizar la API Objective-C de Primetime Player para personalizar el comportamiento del reproductor.
seo-title: Clases de reproductor multimedia
title: Clases de reproductor multimedia
uuid: 705c71b6-4e5e-46b5-a59d-13df977b04f2
translation-type: tm+mt
source-git-commit: b13f2d3f083a6ca333a4edba1c8d7261f7d448ad

---


# Clases de reproductor multimedia {#media-player-classes}

Puede utilizar la API Objective-C de Primetime Player para personalizar el comportamiento del reproductor.

Estas clases describen el reproductor de medios y sus recursos.

| Clase | Descripción |
|---|---|
| Parámetros de PTABRControl | Encapsula todos los parámetros de control de velocidad de bits adaptable. Los parámetros admitidos son:<ul><li>minBitRate</li><li>maxBitRate</li><li>initialBitRate</li></ul> |
| PTDefaultMediaPlayerClientFactory | Implementación predeterminada de PTMediaPlayerClientFactory en el TVSDK. Proporciona las instancias availablePTOpportunityResolver, PTContentResolver y PTAdPolicySelector. |
| PTMediaPlayer | Define el componente raíz para la estructura de Primetime Player. Las aplicaciones crean una instancia de esta clase para reproducir un medio. Este componente envía notificaciones para que la aplicación sepa el estado del reproductor en cualquier momento. |
| PTMediaPlayerClientFactory | Protocolo que describe los métodos que debe implementar una fábrica de cliente de reproductor de medios personalizada para proporcionar las instancias PTOpportunityResolver, PTContentResolver y PTAdPolicySelector disponibles. |
| PTMediaPlayerItem | Representa un medio de audio y vídeo específico. |
| PTMediaPlayerView | Gestiona el componente de vista del marco de trabajo de Primetime Player. |
| PTMediaProfile | Representa el perfil de un único flujo en la lista de reproducción de variante. |
| PTMediaSelectionOption | Representa un recurso de medios audiovisuales para dar cabida a diferentes preferencias de idioma, requisitos de accesibilidad o configuraciones de aplicación personalizadas. Tipos de opciones válidos:<ul><li>Subtítulos (PTMediaSelectionOptionTypeSubtitle)</li><li>Audio alternativo (PTMediaSelectionOptionTypeAudio)</li><li>Subtítulos cerrados (PTMediaSelectionOptionTypeCC)</li><li>No definido (PTMediaSelectionOptionTypeUndefined)</li></ul> |
| PTOpportunityResolver, clase,protocolo PTOpportunityResolver | Clase utilizada para procesar indicaciones en el manifiesto que se utilizarán como colocaciones para el proceso de toma de decisiones y anuncios de Adobe Primetime. |
| PTOpportunityResolverDelegate | Protocolo que describe los métodos que la resolución de oportunidades personalizada ( PTOpportunityResolver ) debe utilizar para comunicar al delegado el estado de la resolución de la oportunidad. |
| PTSDK | Describe la versión del TVSDK y sus capacidades. |
| PTSDKConfig | Expone la configuración global de TVSDK y permite que una aplicación se suscriba a etiquetas HLS personalizadas. |
| PTTextStyleRule | Define constantes que representan claves de atributos de estilo de texto que forman el diccionario de reglas. |
