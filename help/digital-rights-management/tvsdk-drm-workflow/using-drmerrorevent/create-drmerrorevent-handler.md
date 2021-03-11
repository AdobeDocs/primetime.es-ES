---
title: Creación de un controlador DRMErrorEvent
description: Creación de un controlador DRMErrorEvent
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# Crear un controlador DRMErrorEvent{#create-a-drmerrorevent-handler}

Cree un controlador de eventos para procesar eventos de error distribuidos desde Primetime cuando detecte un error al intentar reproducir contenido protegido.

Normalmente, cuando una aplicación encuentra un error, realiza cualquier cantidad de tareas de limpieza. A continuación, informa al usuario del error y proporciona opciones para solucionarlo.

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```

