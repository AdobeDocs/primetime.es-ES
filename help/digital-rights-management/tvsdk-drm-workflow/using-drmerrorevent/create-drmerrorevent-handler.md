---
title: Crear un controlador DRMErrorEvent
description: Crear un controlador DRMErrorEvent
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# Crear un controlador DRMErrorEvent{#create-a-drmerrorevent-handler}

Cree un controlador de eventos para procesar los eventos de error distribuidos desde Primetime cuando encuentre un error al intentar reproducir contenido protegido.

Normalmente, cuando una aplicación encuentra un error, realiza cualquier cantidad de tareas de limpieza. A continuación, informa al usuario del error y proporciona opciones para resolverlo.

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```

