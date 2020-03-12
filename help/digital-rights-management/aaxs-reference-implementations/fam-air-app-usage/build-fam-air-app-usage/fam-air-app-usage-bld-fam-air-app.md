---
seo-title: Creación de la aplicación AIR de Flash Access Manager
title: Creación de la aplicación AIR de Flash Access Manager
uuid: 00927eb3-b8eb-4dd4-b528-91b70760c8cd
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Creación de la aplicación AIR de Flash Access Manager {#building-the-flash-access-manager-air-application}

Para crear el archivo AIR de Flash Access Manager a partir del código fuente, necesita tener instalado el SDK de Flex y AIR en el equipo. Para poder empaquetar y ejecutar la aplicación, debe compilar el código MXML en un archivo SWF mediante el [!DNL amxmlc] compilador. El [!DNL amxmlc] compilador se encuentra en el [!DNL bin] directorio del SDK de Flex 4 o posterior. Si lo desea, puede configurar la variable de entorno de ruta para que incluya el directorio bin del SDK de Flex para facilitar la ejecución de las utilidades en la línea de comandos.

Utilice el procedimiento siguiente para crear el archivo AIR de Flash Access Manager:

1. Abra un shell de comandos o un terminal y vaya a la carpeta del proyecto de la aplicación AIR de Flash Access Manager ( [!DNL UI Tools\Flash Access Manager] en el directorio de implementación de referencia).
1. Introduzca el siguiente comando:

   ```
   amxmlc src\FlashAccessmanager.mxml
   ```

   La ejecución [!DNL amxmlc] produce [!DNL FlashAccessManager.swf], que contiene el código compilado de la aplicación.

El SDK de Adobe AIR incluye la utilidad AIR Developer Tool (ADT) para empaquetar aplicaciones de AIR y generar certificados. las aplicaciones de AIR deben firmarse digitalmente; los usuarios recibirán una advertencia al instalar aplicaciones que no estén firmadas correctamente o que no estén firmadas en absoluto. Para generar un certificado mediante la línea de comandos, abra una ventana de la consola en la misma carpeta que la aplicación de AIR y escriba lo siguiente:

```
adt -certificate -cn SelfSigned 1024-RSA testCert.pfx  
<i class="+ topic ph hi-d="" i "="">
  some_password 
</i class="+ topic>
```

Sustituya *some_password* por una contraseña de su elección. Después de unos segundos, ADT debe completar el proceso de generación de certificados y debe tener un nuevo [!DNL testCert.pfx] archivo en el directorio de aplicaciones.

A continuación, utilice ADT para empaquetar la aplicación en un [!DNL .air] archivo, mediante el comando:

```
adt -package -storetype pkcs12 -keystore testCert.pfx FlashAccessManager.air src\FlashAccessManager-app.xml . -C src assets
```

Este comando indica a ADT que empaquete la aplicación mediante el uso del archivo clave en [!DNL testCert.pfx]. En la línea anterior, se configura ADT para empaquetar toda la aplicación en un archivo denominado [!DNL FlashAccessManager.air], e incluir los archivos [!DNL FlashAccessManager-app.xml] y [!DNL FlashAccessManager.swf] las imágenes del directorio assets.

Como parte de este proceso, se le pedirá la contraseña que configuró para el nuevo archivo de certificado. Ingrese, espere un momento y aparecerá un [!DNL FlashAccessManager.air] archivo en el mismo directorio que los archivos del proyecto.
