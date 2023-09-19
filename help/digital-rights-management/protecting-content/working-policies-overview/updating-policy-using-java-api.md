---
title: Actualización de una directiva DRM con la API de Java
description: Actualización de una directiva DRM con la API de Java
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Actualización de una directiva DRM con la API de Java {#updating-a-drm-policy-with-the-java-api}

Para actualizar una directiva DRM con la API de Java:

1. Configure su entorno de desarrollo e incluya en su proyecto todos los archivos JAR enumerados en [Configuración del entorno de desarrollo](../../protecting-content/setting-up-the-sdk/setup-dev-env.md).
1. Creación de una DRM `Policy` y leer la directiva DRM desde un archivo o base de datos.

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. Actualización del DRM `Policy` estableciendo sus propiedades, como el nombre y las reglas de uso.

   ```java
   // Change the DRM policy name.  
   policy.setName("UpdatedDemoPolicy");  
   
   // Add DRM module restrictions to the play right  
   for (Right r: policy.getRights()) {  
       if (r instanceof PlayRight) {  
           PlayRight pr = (PlayRight) r;  
           // Disallow Linux versions up to and including 1.9.  Allow  
           // all other OSes and Linux versions above 1.9  
           VersionInfo toExclude = new VersionInfo();  
           toExclude.setOS("Linux");  
           toExclude.setReleaseVersion("1.9");  
           Collection<VersionInfo> exclusions = new ArrayList<VersionInfo>();  
           exclusions.add(toExclude);  
           ModuleRequirements drmRestrictions = new ModuleRequirements();  
           drmRestrictions.setExcludedVersions(exclusions);  
           pr.setDRMModuleRequirements(drmRestrictions);  
           break;  
       }  
   }
   ```

1. Serialización del DRM actualizado `Policy` y almacenarlo en un archivo o base de datos.

   ```java
   // Serialize the DRM policy.  
   byte[] policyBytes = policy.getBytes();  
   System.out.println("New DRM policy revision number: "  
       +  policy.getRevision());      
   // Write the DRM policy to a file.   
   // Alternatively, the DRM policy may be stored in a database.  
   FileOutputStream out = new FileOutputStream("demopolicy-updated.pol");  
   out.write(policyBytes);  
   out.close();
   ```

Consulte `com.adobe.flashaccess.samples.policy.UpdatePolicy` en las herramientas de línea de comandos de implementación de referencia [!DNL samples] para el origen de este código de ejemplo.
