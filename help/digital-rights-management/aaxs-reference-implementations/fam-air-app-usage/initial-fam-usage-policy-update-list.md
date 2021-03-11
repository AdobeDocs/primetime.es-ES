---
title: Lista de actualización de directivas
description: Lista de actualización de directivas
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Lista de actualización de directivas {#policy-update-list}

Puede utilizar Listas de actualización de directivas para comunicar los cambios de directivas a un servidor de licencias. Si se modifica una directiva después de usarla para empaquetar contenido, es deseable que el servidor de licencias tenga en cuenta la versión más reciente de la directiva, de modo que se pueda utilizar esa versión para emitir una licencia.

Para crear una Lista de actualización de directivas por primera vez, haga clic en **[!UICONTROL Add policies]** para ver todas las directivas disponibles en el servidor. Para las directivas que se hayan actualizado desde que se utilizaron para empaquetar contenido, seleccione el botón de opción **[!UICONTROL update]** .

Si ya no desea utilizar una directiva para emitir licencias y la directiva ya se utilizó para empaquetar contenido, puede que desee revocar la directiva. Para ello, seleccione el botón de opción **[!UICONTROL revoke]** . Cuando haya seleccionado las políticas deseadas, elija **[!UICONTROL Create Policy Update List]**. Un archivo llamado [!DNL PolicyUpdateList.dat] se guardará en el directorio [!DNL Resources].

Para modificar una lista de actualización de directivas existente, haga clic en **[!UICONTROL Add policies]** para ver todas las directivas disponibles en el servidor. Elija las directivas adicionales que desee agregar o revocar. Las entradas existentes en la Lista de actualización de directivas se pueden cambiar en la sección superior de la pantalla. Las directivas marcadas **[!UICONTROL updated]** pueden cambiarse a **[!UICONTROL revoked]**, pero una vez que una directiva es **[!UICONTROL revoked]**, no se puede volver a cambiar a **[!UICONTROL updated]**.

Cuando se hayan realizado los cambios deseados, elija **[!UICONTROL Create Policy Update List]** y el archivo [!DNL PolicyUpdateList.dat] se regenerará. Si una directiva ya está en la lista de actualización de directivas y se ha actualizado desde la última vez que se generó la lista, se utilizará la versión más reciente de la directiva cuando se vuelva a generar la lista de actualización de directivas.
