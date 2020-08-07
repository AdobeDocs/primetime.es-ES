---
description: 'null'
seo-description: 'null'
seo-title: Preparación de contraseñas para los archivos de propiedades del servidor
title: Preparación de contraseñas para los archivos de propiedades del servidor
uuid: 3e00ba9b-b692-4713-8306-5ab896461f2a
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Preparación de contraseñas para los archivos de propiedades del servidor{#prepare-passwords-for-the-server-properties-files}

La implementación de referencia proporciona `ScrambleUtil.class`, una clase que garantiza la seguridad de la contraseña de la credencial.

Utilice esta herramienta para cifrar la contraseña antes de incluirla en el [!DNL flashaccess-refimpl.properties] archivo.

Para ejecutar la herramienta, puede utilizar una secuencia de comandos Ant o Java.

La utilidad genera la contraseña cifrada, que debe copiar en el [!DNL flashaccess-refimpl.properties] archivo.

>[!NOTE]
>
>Las contraseñas que se han codificado con el `ScrambleUtil.class` que se ha proporcionado con la implementación de referencia no funcionan con Primetime DRM Server para flujo protegido.
