---
title: "How to: Create a Product Manifest"
ms.custom: na
ms.date: 10/03/2016
ms.devlang: 
  - FSharp
  - VB
  - CSharp
  - C++
ms.prod: visual-studio-dev14
ms.reviewer: na
ms.suite: na
ms.technology: 
  - vs-ide-deployment
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2d316aaa-8bc0-4ce5-90ab-23b3eac0b5dd
caps.latest.revision: 10
manager: wpickett
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - it-it
  - ja-jp
  - ko-kr
  - pl-pl
  - pt-br
  - ru-ru
  - tr-tr
  - zh-cn
  - zh-tw
---
# How to: Create a Product Manifest
To deploy prerequisites for your application, you can create a bootstrapper package. A bootstrapper package contains a single product manifest file but a package manifest for each locale. The package manifest contains localization-specific aspects of your package. This includes strings, end-user license agreements, and the language packs.  
  
 For more information about product manifests, see [How to: Create a Package Manifest](../VS_IDE/How-to--Create-a-Package-Manifest.md).  
  
## Creating the Product Manifest  
  
#### To create the product manifest  
  
1.  Create a directory for the bootstrapper package. This example uses C:\package.  
  
2.  In Visual Studio, create a new XML file called `product.xml`, and save it to the C:\package folder.  
  
3.  Add the following XML to describe the XML namespace and product code for the package. Replace the product code with a unique identifier for the package.  
  
    ```  
    <Product  
    xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"   
    ProductCode="Custom.Bootstrapper.Package">  
    ```  
  
4.  Add XML to specify that the package has a dependency. This example uses a dependency on Microsoft Windows Installer 3.1.  
  
    ```  
    <RelatedProducts>  
        <DependsOnProduct Code="Microsoft.Windows.Installer.3.1" />  
      </RelatedProducts>  
    ```  
  
5.  Add XML to list all the files that are in the bootstrapper package. This example uses the package file name CorePackage.msi.  
  
    ```  
    <PackageFiles>  
        <PackageFile Name="CorePackage.msi"/>  
    </PackageFiles>  
    ```  
  
6.  Copy or move the CorePackage.msi file to the C:\package folder.  
  
7.  Add XML to install the package by using bootstrapper commands. The bootstrapper automatically adds the **/qn** flag to the .msi file, which will install silently. If the file is an .exe, the bootstrapper runs the .exe file by using the shell. The following XML shows no arguments to CorePackage.msi, but you can put command line argument into the Arguments attribute.  
  
    ```  
    <Commands>  
        <Command PackageFile="CorePackage.msi" Arguments="">  
    ```  
  
8.  Add the following XML to check if this bootstrapper package is installed. Replace the product code with the GUID for the redistributable component.  
  
    ```  
    <InstallChecks>  
        <MsiProductCheck   
            Property="IsMsiInstalled"   
            Product="{XXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}"/>  
    </InstallChecks>  
    ```  
  
9. Add XML to change the bootstrapper behavior depending on if the bootstrapper component is already installed. If the component is installed, the bootstrapper package does not run. The following XML checks if the current user is an administrator because this component requires administrative privileges.  
  
    ```  
    <InstallConditions>  
        <BypassIf   
           Property="IsMsiInstalled"   
           Compare="ValueGreaterThan" Value="0"/>  
        <FailIf Property="AdminUser"   
            Compare="ValueNotEqualTo" Value="True"  
            String="NotAnAdmin"/>  
    </InstallConditions>  
    ```  
  
10. Add XML to set exit codes if the installation is successful and if a reboot is necessary. The following XML demonstrates the Fail and FailReboot exit codes, which indicate that the bootstrapper will not continue installing packages.  
  
    ```  
    <ExitCodes>  
        <ExitCode Value="0" Result="Success"/>  
        <ExitCode Value="1641" Result="SuccessReboot"/>  
        <ExitCode Value="3010" Result="SuccessReboot"/>  
        <DefaultExitCode Result="Fail" String="GeneralFailure"/>  
    </ExitCodes>  
    ```  
  
11. Add the following XML to end the section for bootstrapper commands.  
  
    ```  
        </Command>  
    </Commands>  
    ```  
  
12. Move the C:\package folder to the Visual Studio bootstrapper directory. For Visual Studio 2010, this is the \Program Files\Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages directory.  
  
## Example  
 The product manifest contains installation instructions for custom prerequisites.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<Product  
  xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"  
  ProductCode="Custom.Bootstrapper.Package">  
  
  <RelatedProducts>  
    <DependsOnProduct Code="Microsoft.Windows.Installer.3.1" />  
  </RelatedProducts>  
  
  <PackageFiles>  
    <PackageFile Name="CorePackage.msi"/>  
  </PackageFiles>  
  
  <InstallChecks>  
    <MsiProductCheck Product="IsMsiInstalled"   
      Property="{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}"/>  
  </InstallChecks>  
  
  <Commands>  
    <Command PackageFile="CorePackage.msi" Arguments="">  
  
      <InstallConditions>  
        <BypassIf Property="IsMsiInstalled"  
          Compare="ValueGreaterThan" Value="0"/>  
        <FailIf Property="AdminUser"   
          Compare="ValueNotEqualTo" Value="True"  
         String="NotAnAdmin"/>  
      </InstallConditions>  
  
      <ExitCodes>  
        <ExitCode Value="0" Result="Success"/>  
        <ExitCode Value="1641" Result="SuccessReboot"/>  
        <ExitCode Value="3010" Result="SuccessReboot"/>  
        <DefaultExitCode Result="Fail" String="GeneralFailure"/>  
      </ExitCodes>  
    </Command>  
  </Commands>  
</Product>  
```  
  
## See Also  
 [Product and Package Schema Reference](../VS_IDE/Product-and-Package-Schema-Reference.md)