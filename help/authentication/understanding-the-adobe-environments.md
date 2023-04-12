---
title: Explicación de los entornos de Adobe
description: Explicación de los entornos de Adobe
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# Explicación de los entornos de Adobe {#understanding-the-adobe-environments}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

La documentación oficial que describe los entornos de Adobe está disponible [Configuración del entorno y pruebas en Pre-qual](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md):

Los entornos de Adobe se resumen en unas pocas palabras:

Adobe tiene dos entornos: **Pre-Calificación** y **Versión**.

* En el entorno de precalificación, estamos preparando la nueva compilación para su lanzamiento.

* La versión actual se encuentra en el entorno de versión.

Cada entorno tiene dos perfiles : **ensayo** y **producción**.

* El perfil de ensayo se conecta al servidor de ensayo de MVPD
* El perfil de producción se conecta al perfil de producción de los MVPD.

La razón de tener los dos perfiles es que en el perfil de ensayo estamos preparando nuevos socios para que se activen, y les gustaría probar el sistema con la próxima compilación (Pre-Qualification) o con la versión una (más estable).

Si un socio desea probar la nueva versión, hay que realizar un par de pasos adicionales. Consulte [Configuración del entorno y pruebas en Pre-qual](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md).

Al seguir los pasos anteriores, se garantiza que la próxima versión se probará en el entorno de precalificación.
