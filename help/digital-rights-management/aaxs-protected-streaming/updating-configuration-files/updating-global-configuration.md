---
seo-title: Actualización del archivo de configuración global
title: Actualización del archivo de configuración global
uuid: f733550c-46c0-49c2-8fd1-15906f7d7b22
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---


# Actualización del archivo de configuración global{#updating-the-global-configuration-file}

La contraseña de HSM en [!DNL flashaccess-global.xml] puede modificarse en cualquier momento y los cambios tendrán efecto la próxima vez que el servidor vuelva a cargar el archivo de configuración. Sin embargo, los cambios en los elementos &quot;Registro&quot; y &quot;Almacenamiento en caché&quot; no se recargan; cualquier cambio en estos elementos requiere un reinicio del servidor.
