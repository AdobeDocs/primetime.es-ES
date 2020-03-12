---
description: 'null'
seo-description: 'null'
seo-title: Preparación de contraseñas para los archivos de propiedades del servidor
title: Preparación de contraseñas para los archivos de propiedades del servidor
uuid: 3e00ba9b-b692-4713-8306-5ab896461f2a
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# Preparación de contraseñas para los archivos de propiedades del servidor{#prepare-passwords-for-the-server-properties-files}

La implementación de referencia proporciona `ScrambleUtil.class`, una clase que garantiza la seguridad de la contraseña de la credencial.

Utilice esta herramienta para cifrar la contraseña antes de incluirla en el [!DNL flashaccess-refimpl.properties] archivo.

Para ejecutar la herramienta, puede utilizar una secuencia de comandos Ant o Java.

La utilidad genera la contraseña cifrada, que debe copiar en el [!DNL flashaccess-refimpl.properties] archivo.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Las contraseñas que se han codificado con el `ScrambleUtil.class` que se ha proporcionado con la implementación de referencia no funcionan con Primetime DRM Server para flujo protegido.
