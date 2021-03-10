---
title: Creación de un controlador DRMStatusEvent
description: Creación de un controlador DRMStatusEvent
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# Crear un controlador DRMStatusEvent{#create-a-drmstatusevent-handler}

En el siguiente ejemplo se crea un controlador de eventos que genera la información de estado del contenido de DRM para el objeto Primetime que originó el evento.

Agregue un controlador de eventos a un objeto Primetime que señale al contenido protegido:

```
function drmStatusEventHandler(event:DRMStatusEvent):void { trace(event); } 
```

