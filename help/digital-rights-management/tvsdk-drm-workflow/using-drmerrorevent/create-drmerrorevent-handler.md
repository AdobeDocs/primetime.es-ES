---
seo-title: Creación de un controlador DRMErrorEvent
title: Creación de un controlador DRMErrorEvent
uuid: dde660fc-6899-47d4-97d4-46acda2db262
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc

---


# Creación de un controlador DRMErrorEvent{#create-a-drmerrorevent-handler}

Cree un controlador de eventos para procesar los eventos de error enviados desde Primetime cuando detecte un error al intentar reproducir contenido protegido.

Normalmente, cuando una aplicación encuentra un error, realiza cualquier cantidad de tareas de limpieza. A continuación, informa al usuario del error y proporciona opciones para resolverlo.

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```

