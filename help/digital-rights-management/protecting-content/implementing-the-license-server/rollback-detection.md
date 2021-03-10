---
title: Detección de reversión
description: Detección de reversión
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Detección de reversión {#rollback-detection}

Para la detección de reversión, algunas reglas de uso requieren que el cliente mantenga la información de estado para la aplicación de los derechos. Por ejemplo, para aplicar la regla de uso de la ventana de reproducción, el cliente almacena la fecha y la hora en que el usuario empezó a ver el contenido por primera vez. Este evento déclencheur el inicio de la ventana de reproducción. Para aplicar de forma segura la ventana de reproducción, el servidor debe asegurarse de que el usuario no realiza una copia de seguridad y restaurar el estado del cliente para eliminar la hora de inicio de la ventana de reproducción almacenada en el cliente. El servidor hace esto rastreando el valor del contador de reversión del cliente.

Para cada solicitud, el servidor obtiene el valor del contador llamando a `RequestMessageBase.getClientState()` para obtener el objeto `ClientState` y luego llamando a `ClientState.getCounter()` para obtener el valor actual del contador de estado del cliente. El servidor debe almacenar este valor para cada cliente (utilice `MachineId.getUniqueId()` para identificar el cliente asociado con el valor del contador de reversión) y luego llamar a `ClientState.incrementCounter()` para aumentar el valor del contador en uno. Si el servidor detecta que el valor de contador es menor que el último valor visto por el servidor, es posible que el estado del cliente se haya revertido.

Consulte la documentación de referencia de la API `ClientState` para obtener más información sobre la detección de manipulaciones en el estado del cliente.
