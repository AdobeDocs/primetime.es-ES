---
title: Creación de la aplicación de AIR del Administrador de Flashes Access
description: Creación de la aplicación de AIR del Administrador de Flashes Access
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# Creación de la aplicación de AIR del Administrador de Flashes Access {#building-the-flash-access-manager-air-application}

Para crear el archivo de AIR del Administrador de Flashes Access a partir del código fuente, necesita instalar el SDK de Flex y AIR en el equipo. Para poder empaquetar y ejecutar la aplicación, debe compilar el código de MXML en un archivo SWF mediante el compilador [!DNL amxmlc]. El compilador [!DNL amxmlc] se puede encontrar en el directorio [!DNL bin] del SDK de Flex 4 o posterior. Si lo desea, puede configurar la variable de entorno de ruta para que incluya el directorio bin del SDK para Flex con el fin de facilitar la ejecución de las utilidades en la línea de comandos.

Utilice el siguiente procedimiento para crear el archivo AIR del Administrador de Flashes Access:

1. Abra un shell de comandos o un terminal y vaya a la carpeta del proyecto de la aplicación de AIR del Administrador de Flashes Access ( [!DNL UI Tools\Flash Access Manager] en el directorio Implementación de referencia).
1. Introduzca el siguiente comando:

   ```
   amxmlc src\FlashAccessmanager.mxml
   ```

   La ejecución de [!DNL amxmlc] produce [!DNL FlashAccessManager.swf], que contiene el código compilado de la aplicación.

El SDK de Adobe AIR incluye la utilidad AIR Developer Tool (ADT) para empaquetar aplicaciones AIR y generar certificados. Las aplicaciones de AIR deben firmarse digitalmente; los usuarios recibirán una advertencia al instalar aplicaciones que no estén firmadas correctamente o que no estén firmadas. Para generar un certificado mediante la línea de comandos, abra una ventana de la consola en la misma carpeta que la aplicación de AIR y escriba lo siguiente:

```
adt -certificate -cn SelfSigned 1024-RSA testCert.pfx  
<i class="+ topic ph hi-d="" i "="">
  some_password 
</i class="+ topic>
```

Sustituya *some_password* por una contraseña de su elección. Después de unos segundos, ADT debe completar su proceso de generación de certificados y debe tener un nuevo archivo [!DNL testCert.pfx] en el directorio de la aplicación.

A continuación, utilice ADT para empaquetar la aplicación en un archivo [!DNL .air], utilizando el comando :

```
adt -package -storetype pkcs12 -keystore testCert.pfx FlashAccessManager.air src\FlashAccessManager-app.xml . -C src assets
```

Este comando indica a ADT que empaquete su aplicación utilizando el archivo clave en [!DNL testCert.pfx]. En la línea anterior, se configura ADT para empaquetar toda la aplicación en un archivo denominado [!DNL FlashAccessManager.air], y para incluir los archivos [!DNL FlashAccessManager-app.xml] y [!DNL FlashAccessManager.swf] y las imágenes del directorio de recursos.

Como parte de este proceso, se le pedirá la contraseña que configure para el nuevo archivo de certificado. Ingrelo, espere un momento y aparecerá un archivo [!DNL FlashAccessManager.air] en el mismo directorio que los archivos de proyecto.
