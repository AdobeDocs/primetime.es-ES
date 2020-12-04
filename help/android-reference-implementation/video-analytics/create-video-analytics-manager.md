---
description: Creación del Administrador de análisis de vídeo
seo-description: Creación del Administrador de análisis de vídeo
seo-title: Creación del Administrador de análisis de vídeo
title: Creación del Administrador de análisis de vídeo
uuid: d72e1dfe-df70-47cc-9e00-bd09017d6127
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# Crear el Administrador de análisis de vídeo {#create-the-video-analytics-manager}

Se ha agregado una nueva clase de administrador ( `VAManager`) a la Implementación de referencia de Android. `VAManager` simplemente crea y destruye una instancia de la  `VideoHeartbeat` clase. La implementación de referencia crea una instancia `VAManager` cuando se crea una nueva `MediaPlayer` y destruye esa instancia cuando se destruye la `MediaPlayer`. Esto se implementa en `PlayerFragment.java`.

## Para crear un nuevo Administrador de análisis de vídeo

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

La variable config es una implementación concreta de `IVAConfig` y contiene las configuraciones `VideoHeartbeat` de tiempo de ejecución.

>[!NOTE]
>
>Si la aplicación de Android no está configurada con una cuenta de Adobe Analytics, no se generarán los datos del seguimiento de videos, aunque se cree y habilite una instancia de `VAManager`.

