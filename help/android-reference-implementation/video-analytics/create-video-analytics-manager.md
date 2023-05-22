---
description: Creación del Administrador de Video Analytics
title: Creación del Administrador de Video Analytics
exl-id: 8d2bbb39-10e2-43e8-8ed3-bc376b3f3cc8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Creación del Administrador de Video Analytics {#create-the-video-analytics-manager}

Una nueva clase de administrador ( `VAManager`) se ha añadido a la Implementación de referencia de Android. `VAManager` simplemente crea y destruye una instancia de `VideoHeartbeat` clase. La implementación de referencia crea un `VAManager` instancia cuando se crea un nuevo `MediaPlayer` se crea y destruye esa instancia cuando el `MediaPlayer` se destruye. Esto se implementa en `PlayerFragment.java`.

## Para crear un nuevo Administrador de Video Analytics

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

La variable de configuración es una implementación concreta de `IVAConfig` y contiene el tiempo de ejecución `VideoHeartbeat` configuraciones.

>[!NOTE]
>
>Si la aplicación de Android no está configurada con una cuenta de Adobe Analytics, los datos de seguimiento de vídeo no se generan, aunque se cree una instancia de `VAManager` se crea y se activa.
