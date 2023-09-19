---
description: Normalmente, todas las licencias DRM de Primetime, en el momento de la creación, están enlazadas a un dispositivo único. Este enlace impide que los usuarios compartan licencias entre dispositivos distintos sin autorización. Además del enlace por dispositivo, Primetime DRM permite enlazar licencias a un dominio de dispositivo o a un grupo de dispositivos.
title: Reproducción de contenido cifrado mediante la compatibilidad con dominios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Compatibilidad con dominio de dispositivo {#device-domain-support}

Normalmente, todas las licencias DRM de Primetime, en el momento de la creación, están enlazadas a un dispositivo único. Este enlace impide que los usuarios compartan licencias entre dispositivos distintos sin autorización. Además del enlace por dispositivo, Primetime DRM permite enlazar licencias a un dominio de dispositivo o a un grupo de dispositivos.

Si los metadatos de contenido especifican que se requiere el registro del dominio del dispositivo, la aplicación puede invocar una API para unirse a un grupo de dispositivos. Esta acción almacena en déclencheur una solicitud de registro de dominio para enviarla al servidor de dominio. Una vez que se emite una licencia para un grupo de dispositivos, esta se puede exportar y compartir con otros dispositivos que se hayan unido al grupo de dispositivos.

La información del grupo de dispositivos se utiliza en la `DRMContentData` `VoucherAccessInfo` , que se utilizará para presentar la información necesaria para recuperar y consumir correctamente una licencia.

## Reproducción de contenido cifrado mediante la compatibilidad con dominios {#play-encrypted-content-using-domain-support}

Para reproducir contenido cifrado con Primetime DRM , realice los siguientes pasos:

1. Uso de `VoucherAccessInfo.deviceGroup`, compruebe si se requiere el registro del grupo de dispositivos.
1. Si se requiere autenticación:
   1. Utilice el `DeviceGroupInfo.authenticationMethod` propiedad averigüe si se requiere autenticación.
   1. Si se requiere autenticación, autentique el usuario realizando UNO de los siguientes pasos:

      * Obtener el nombre de usuario y la contraseña del usuario e invocar `DRMManager.authenticate(deviceGroup.serverURL, deviceGroup.domain, username, password)`.
      * Obtenga un token de autenticación en caché o generado previamente e invoque `DRMManager.setAuthenticationToken()`.

   1. Invocar `DRMManager.addToDeviceGroup()`
1. Obtenga la licencia para el contenido realizando una de las siguientes tareas:
   1. Utilice el `DRMManager.loadVoucher()` método.
   1. Obtenga la licencia de un dispositivo diferente registrado en el mismo grupo de dispositivos y proporcione la licencia al `DRMManager` a través de `DRMManager.storeVoucher()` método.
1. Reproducir el contenido cifrado con `Primetime.play()` método.
Para exportar la licencia para el contenido, cualquiera de los dispositivos puede proporcionar los bytes sin procesar de la licencia utilizando `DRMVoucher.toByteArray()` después de obtener la licencia del servidor de licencias DRM de Primetime. Los proveedores de contenido suelen limitar el número de dispositivos en un grupo de dispositivos. Si se alcanza el límite, es posible que tenga que llamar al `DRMManager.removeFromDeviceGroup()` método en un dispositivo no utilizado antes de registrar el dispositivo actual.
