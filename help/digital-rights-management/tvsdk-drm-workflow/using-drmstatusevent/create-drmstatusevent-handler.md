---
seo-title: Creación de un controlador DRMStatusEvent
title: Creación de un controlador DRMStatusEvent
uuid: 64f539d9-344c-4372-88b8-c8d098af9dd8
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc

---


# Creación de un controlador DRMStatusEvent{#create-a-drmstatusevent-handler}

En el ejemplo siguiente se crea un controlador de eventos que genera la información de estado del contenido de DRM para el objeto Primetime que originó el evento.

Agregue un controlador de eventos a un objeto Primetime que apunte a contenido protegido:

```
function drmStatusEventHandler(event:DRMStatusEvent):void { trace(event); } 
```

