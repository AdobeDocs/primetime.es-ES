---
description: Creación del administrador de Video Analytics
title: Creación del administrador de Video Analytics
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---


# Crear el administrador de Video Analytics {#create-the-video-analytics-manager}

Se ha añadido una nueva clase de administrador ( `VAManager`) a la implementación de referencia de Android. `VAManager` simplemente crea y destruye una instancia de la  `VideoHeartbeat` clase. La implementación de referencia crea una instancia `VAManager` cuando se crea un `MediaPlayer` nuevo y destruye esa instancia cuando se destruye el `MediaPlayer`. Esto se implementa en `PlayerFragment.java`.

## Para crear un nuevo Administrador de análisis de vídeo

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

La variable de configuración es una implementación concreta de `IVAConfig` y contiene las configuraciones `VideoHeartbeat` de tiempo de ejecución.

>[!NOTE]
>
>Si la aplicación de Android no está configurada con una cuenta de Adobe Analytics, no se generarán los datos de seguimiento de vídeo, aunque se cree y habilite una instancia de `VAManager`.

