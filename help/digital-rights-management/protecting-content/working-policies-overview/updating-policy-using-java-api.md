---
seo-title: Actualización de una directiva DRM con la API de Java
title: Actualización de una directiva DRM con la API de Java
uuid: ec21351c-900e-48f5-845a-c0b430c210d7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Actualización de una directiva DRM con la API de Java {#updating-a-drm-policy-with-the-java-api}

Para actualizar una directiva DRM con la API de Java:

1. Configure el entorno de desarrollo e incluya en el proyecto todos los archivos JAR enumerados en [Configuración del entorno](../../protecting-content/setting-up-the-sdk/setup-dev-env.md)de desarrollo.
1. Cree una instancia de DRM `Policy` y lea la directiva de DRM desde un archivo o base de datos.

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. Actualice el objeto DRM `Policy` estableciendo sus propiedades, como su nombre y las reglas de uso.

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

1. Serialice el objeto DRM `Policy` actualizado y guárdelo en un archivo o base de datos.

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

Consulte `com.adobe.flashaccess.samples.policy.UpdatePolicy` [!DNL samples] en el directorio Reference Implementation Command Line Tools (Herramientas de línea de comandos de implementación de referencia) el origen de este código de muestra.
