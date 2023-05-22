---
title: Crear un controlador DRMStatusEvent
description: Crear un controlador DRMStatusEvent
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# Crear un controlador DRMStatusEvent{#create-a-drmstatusevent-handler}

En el ejemplo siguiente se crea un controlador de eventos que genera la información de estado de contenido DRM para el objeto Primetime que originó el evento.

Agregue un controlador de eventos a un objeto Primetime que señale a contenido protegido:

```
function drmStatusEventHandler(event:DRMStatusEvent):void { trace(event); } 
```

