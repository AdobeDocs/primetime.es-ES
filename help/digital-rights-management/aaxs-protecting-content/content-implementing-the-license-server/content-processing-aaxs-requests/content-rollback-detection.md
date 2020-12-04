---
seo-title: Detección de retroceso
title: Detección de retroceso
uuid: cc554194-2848-4104-85eb-f697a86c72f2
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# Detección de rollback{#rollback-detection}

Para la detección de rollback, algunas reglas de uso requieren que el cliente mantenga la información de estado para la aplicación de los derechos. Por ejemplo, para aplicar la regla de uso de la ventana de reproducción, el cliente almacena la fecha y la hora en que el usuario comenzó a ver el contenido por primera vez. Este evento desencadena el inicio de la ventana de reproducción. Para aplicar de forma segura la ventana de reproducción, el servidor debe asegurarse de que el usuario no realiza copias de seguridad y restaura el estado del cliente para eliminar el tiempo de inicio de la ventana de reproducción almacenado en el cliente. El servidor hace esto rastreando el valor del contador de rollback del cliente. Para cada solicitud, el servidor obtiene el valor del contador llamando a `RequestMessageBase.getClientState()` para obtener el objeto `ClientState` y luego llamando a `ClientState.getCounter()` para obtener el valor actual del contador de estado del cliente. El servidor debe almacenar este valor para cada cliente (utilice `MachineId.getUniqueId()` para identificar el cliente asociado con el valor del contador de rollback) y luego llame a `ClientState.incrementCounter()` para aumentar el valor del contador en uno. Si el servidor detecta que el valor del contador es menor que el último valor visto por el servidor, es posible que el estado del cliente se haya revertido. Para obtener más información sobre la detección de manipulaciones en el estado del cliente, consulte la documentación de referencia de la API `ClientState`.
