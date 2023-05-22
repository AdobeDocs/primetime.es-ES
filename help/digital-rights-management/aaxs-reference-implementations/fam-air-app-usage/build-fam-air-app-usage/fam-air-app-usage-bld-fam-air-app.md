---
title: Generación de la aplicación AIR de Flash Access Manager
description: Generación de la aplicación AIR de Flash Access Manager
copied-description: true
exl-id: f15fe9d2-d5e8-43ef-a1d5-1211752d54da
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Generación de la aplicación AIR de Flash Access Manager {#building-the-flash-access-manager-air-application}

Para generar el archivo AIR del Administrador de Flash Access a partir del código fuente, necesita instalar en el equipo el SDK de Flex y AIR. MXML Antes de poder empaquetar y ejecutar la aplicación, debe compilar el código de la aplicación en un archivo de SWF utilizando el comando [!DNL amxmlc] compilador. El [!DNL amxmlc] El compilador de se puede encontrar en [!DNL bin] del SDK de Flex 4 o posterior. Si lo desea, puede configurar la variable de entorno de ruta para incluir el directorio bin del SDK de Flex para facilitar la ejecución de las utilidades en la línea de comandos.

Utilice el siguiente procedimiento para generar el archivo AIR de Flash Access Manager:

1. Abra un shell de comandos o un terminal y vaya a la carpeta del proyecto de la aplicación AIR de Flash Access Manager ( [!DNL UI Tools\Flash Access Manager] en el directorio Implementación de referencia).
1. Introduzca el siguiente comando:

   ```
   amxmlc src\FlashAccessmanager.mxml
   ```

   Ejecutando [!DNL amxmlc] produce [!DNL FlashAccessManager.swf], que contiene el código compilado de la aplicación.

El SDK de Adobe AIR incluye la utilidad AIR Developer Tool (ADT) para empaquetar aplicaciones de AIR y generar certificados. Las aplicaciones de AIR deben estar firmadas digitalmente; los usuarios recibirán una advertencia al instalar aplicaciones que no estén firmadas correctamente o que no estén firmadas en absoluto. Para generar un certificado mediante la línea de comandos, abra una ventana de consola en la misma carpeta que la aplicación de AIR y escriba lo siguiente:

```
adt -certificate -cn SelfSigned 1024-RSA testCert.pfx  
<i class="+ topic ph hi-d="" i "="">
  some_password 
</i class="+ topic>
```

Sustituir *some_password* con una contraseña de su elección. Después de unos segundos, ADT debe completar su proceso de generación de certificados y debe tener un nuevo [!DNL testCert.pfx] en el directorio de la aplicación.

A continuación, utilice ADT para empaquetar la aplicación en un [!DNL .air] , mediante el comando:

```
adt -package -storetype pkcs12 -keystore testCert.pfx FlashAccessManager.air src\FlashAccessManager-app.xml . -C src assets
```

Este comando indica a ADT que empaquete la aplicación mediante el archivo de claves incluido en [!DNL testCert.pfx]. En la línea anterior, configure ADT para empaquetar toda la aplicación en un archivo denominado [!DNL FlashAccessManager.air]y para incluir los archivos [!DNL FlashAccessManager-app.xml] y [!DNL FlashAccessManager.swf] y las imágenes del directorio de recursos.

Como parte de este proceso, se le pedirá la contraseña que ha establecido para el nuevo archivo de certificado. Ingrese, espere un momento y un [!DNL FlashAccessManager.air] Este archivo debe aparecer en el mismo directorio que los archivos de proyecto.
