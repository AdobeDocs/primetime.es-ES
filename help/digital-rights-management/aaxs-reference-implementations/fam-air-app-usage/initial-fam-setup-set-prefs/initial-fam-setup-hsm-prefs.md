---
seo-title: Preferencias de HSM
title: Preferencias de HSM
uuid: 1b97d582-d4b6-48cd-9c24-2d13493571e9
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Preferencias de HSM {#hsm-preferences}

Las preferencias de esta ficha solo deben especificarse si la casilla de verificación está seleccionada en la ficha Packager (Packager) **[!UICONTROL Enable HSM]** . En la tabla siguiente se describen estas preferencias:

| Preferencia | Descripción |
|---|---|
| Nombre del archivo de configuración PKCS#11 de Sun | Ruta completa al archivo de configuración del proveedor PKCS#11 de Sun. Consulte la Guía de referencia de Java PKCS#11 en el sitio web de Sun para obtener más información sobre el contenido de este archivo de configuración. |
| Contraseña de partición | La contraseña de la partición HSM especificada en el archivo de configuración PKCS#11. |
| Alias de certificado de servidor de licencias | Alias para el certificado de servidor de licencias emitido por Adobe almacenado en HSM. Este certificado se utiliza para cifrar el CEK durante el empaquetado. Especifique esto en lugar de Certificado *de servidor de* licencias en la ficha Packager. |
| Alias de certificado de transporte del servidor de licencias | Alias para el certificado de transporte de servidor emitido por Adobe almacenado en HSM. Este certificado se utiliza para asegurar las comunicaciones entre el cliente y el servidor de licencias. Especifique esto en lugar del certificado *de transporte del servidor de* licencias en la ficha Packager. |
| Alias de credencial de Packager | Alias para las credenciales de empaquetador emitidas por Adobe (certificado y clave privada) almacenadas en HSM. Se utiliza para firmar los metadatos durante el empaquetado. Especifique esto en lugar de *Packager Credential* en la ficha Packager. |
| Alias de credenciales del servidor de licencias | Alias para las credenciales del servidor de licencias emitidas por Adobe (certificado y clave privada) almacenadas en HSM. Esta credencial se utiliza para firmar listas de actualización de directivas. Especifique esto en lugar de Credenciales *del servidor de* licencias en la ficha Lista de actualizaciones de directivas. (Es probable que este alias sea el mismo que el alias *de certificado del servidor* de licencias). |

