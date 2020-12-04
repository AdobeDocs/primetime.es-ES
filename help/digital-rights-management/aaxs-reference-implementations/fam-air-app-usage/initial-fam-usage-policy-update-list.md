---
seo-title: Lista de actualización de directivas
title: Lista de actualización de directivas
uuid: ecc74b66-5b53-4ec3-9641-8b78929e2932
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Lista de actualización de directivas {#policy-update-list}

Puede utilizar Listas de actualización de directivas para comunicar los cambios de directivas a un servidor de licencias. Si se modifica una directiva después de usarla para empaquetar contenido, es conveniente que el servidor de licencias tenga en cuenta la versión más reciente de la directiva, de modo que se pueda utilizar esa versión para emitir una licencia.

Para crear una Lista de actualización de directiva por primera vez, haga clic en **[!UICONTROL Add policies]** para vista de todas las directivas disponibles en el servidor. Para las directivas que se hayan actualizado desde que se utilizaron para empaquetar contenido, seleccione el botón de opción **[!UICONTROL update]**.

Si ya no desea usar una política para emitir licencias y la política ya se utilizó para empaquetar contenido, puede que desee revocar la directiva. Para ello, seleccione el botón de opción **[!UICONTROL revoke]**. Cuando se hayan seleccionado las directivas deseadas, elija **[!UICONTROL Create Policy Update List]**. Un archivo llamado [!DNL PolicyUpdateList.dat] se guardará en el directorio [!DNL Resources].

Para modificar una Lista de actualización de directiva existente, haga clic en **[!UICONTROL Add policies]** para vista de todas las directivas disponibles en el servidor. Elija las directivas adicionales que desee agregar o revocar. Las entradas existentes en la Lista Actualización de directiva se pueden cambiar en la sección superior de la pantalla. Las políticas marcadas como **[!UICONTROL updated]** pueden cambiarse a **[!UICONTROL revoked]**, pero una vez que una política es **[!UICONTROL revoked]**, no se puede cambiar a **[!UICONTROL updated]**.

Cuando se hayan realizado los cambios deseados, elija **[!UICONTROL Create Policy Update List]** y se vuelva a generar el archivo [!DNL PolicyUpdateList.dat]. Si una directiva ya está en la lista de actualización de directiva y se ha actualizado desde la última vez que se generó la lista, se utilizará la versión más reciente de la directiva cuando se vuelva a generar la Lista de actualización de directiva.
