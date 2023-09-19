---
title: Detección de reversión
description: Detección de reversión
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# Detección de reversión{#rollback-detection}

Para la detección de reversiones, algunas reglas de uso requieren que el cliente mantenga la información de estado para la aplicación de los derechos. Por ejemplo, para aplicar la regla de uso de la ventana de reproducción, el cliente almacena la fecha y la hora en que el usuario empezó a ver el contenido por primera vez. Este evento déclencheur el inicio de la ventana de reproducción. Para aplicar de forma segura la ventana de reproducción, el servidor debe asegurarse de que el usuario no realiza una copia de seguridad ni restaura el estado del cliente para eliminar el tiempo de inicio de la ventana de reproducción almacenado en el cliente. Para ello, el servidor realiza un seguimiento del valor del contador de reversión del cliente. Para cada solicitud, el servidor obtiene el valor del contador llamando a `RequestMessageBase.getClientState()` para obtener la `ClientState` objeto, luego llamar a `ClientState.getCounter()` para obtener el valor actual del contador de estado del cliente. El servidor debe almacenar este valor para cada cliente (utilice `MachineId.getUniqueId()` para identificar al cliente asociado con el valor del contador de reversión y, a continuación, llame a `ClientState.incrementCounter()` para aumentar el valor del contador en uno. Si el servidor detecta que el valor del contador es menor que el último valor que vio el servidor, es posible que se haya revertido el estado del cliente. Para obtener más información sobre la detección de alteraciones de estado de cliente, consulte la `ClientState` Documentación de referencia de API.
