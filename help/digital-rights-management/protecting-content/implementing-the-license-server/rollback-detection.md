---
seo-title: Detección de retroceso
title: Detección de retroceso
uuid: ec124bac-a1d7-45be-bf09-a99d5eec5042
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Detección de retroceso {#rollback-detection}

Para la detección de rollback, algunas reglas de uso requieren que el cliente mantenga la información de estado para la aplicación de los derechos. Por ejemplo, para aplicar la regla de uso de la ventana de reproducción, el cliente almacena la fecha y la hora en que el usuario comenzó a ver el contenido por primera vez. Este evento desencadena el inicio de la ventana de reproducción. Para aplicar de forma segura la ventana de reproducción, el servidor debe asegurarse de que el usuario no realiza copias de seguridad y restaura el estado del cliente para eliminar la hora de inicio de la ventana de reproducción almacenada en el cliente. El servidor hace esto rastreando el valor del contador de rollback del cliente.

Para cada solicitud, el servidor obtiene el valor del contador llamando `RequestMessageBase.getClientState()` a obtener el `ClientState` objeto y luego `ClientState.getCounter()` a obtener el valor actual del contador de estado del cliente. El servidor debe almacenar este valor para cada cliente (utilizar `MachineId.getUniqueId()` para identificar el cliente asociado con el valor del contador de rollback) y, a continuación, llamar `ClientState.incrementCounter()` para aumentar el valor del contador en uno. Si el servidor detecta que el valor del contador es menor que el último valor visto por el servidor, es posible que el estado del cliente se haya revertido.

Consulte la documentación de referencia de la `ClientState` API para obtener más información sobre la detección de manipulaciones en el estado del cliente.
