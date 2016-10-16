---
title: "Server and Client Configuration Issues in ClickOnce Deployments"
ms.custom: na
ms.date: 10/10/2016
ms.devlang: 
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
ms.assetid: 929e5fcc-dd56-409c-bb57-00bd9549b20b
caps.latest.revision: 33
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
# Server and Client Configuration Issues in ClickOnce Deployments
If you use Internet Information Services (IIS) on Windows Server, and your deployment contains a file type that Windows does not recognize, such as a Microsoft Word file, IIS will refuse to transmit that file, and your deployment will not succeed.  
  
 Additionally, some Web servers and Web application software, such as ASP.NET, contain a list of files and file types that you cannot download. For example, ASP.NET prevents the download of all Web.config files. These files may contain sensitive information such as user names and passwords.  
  
 Although this restriction should cause no problems for downloading core ClickOnce files such as manifests and assemblies, this restriction may prevent you from downloading data files included as part of your ClickOnce application. In ASP.NET, you can resolve this error by removing the handler that prohibits downloading of such files from the IIS configuration manager. See the IIS server documentation for additional details.  
  
 Some Web servers might block files with extensions such as .dll, .config, and .mdf. Windows-based applications typically include files with some of these extensions. If a user attempts to run a ClickOnce application that accesses a blocked file on a Web server, an error will result. Rather than unblocking all file extensions, ClickOnce publishes every application file with a ".deploy" file extension by default. Therefore, the administrator only needs to configure the Web server to unblock the following three file extensions:  
  
-   .application  
  
-   .manifest  
  
-   .deploy  
  
 However, you can disable this option by clearing the **Use ".deploy" file extension** option on the [Publish Options Dialog Box](assetId:///fd9baa1b-7311-4f9e-8ffb-ae50cf110592), in which case you must configure the Web server to unblock all file extensions used in the application.  
  
 You will have to configure .manifest, .application, and .deploy, for example, if you are using IIS where you have not installed the .NET Framework, or if you are using another Web server (for example, Apache).  
  
## ClickOnce and Secure Sockets Layer (SSL)  
 A ClickOnce application will work fine over SSL, except when Internet Explorer raises a prompt about the SSL certificate. The prompt can be raised when there is something wrong with the certificate, such as when the site names do not match or the certificate has expired. To make ClickOnce work over an SSL connection, make sure that the certificate is up-to-date, and that the certificate data matches the site data.  
  
## ClickOnce and Proxy Authentication  
 ClickOnce provides support for Windows Integrated proxy authentication starting in .NET Framework 3.5. No specific machine.config directives are required. ClickOnce does not provide support for other authentication protocols such as Basic or Digest.  
  
 You can also apply a hotfix to .NET Framework 2.0 to enable this feature. For more information, see http://go.microsoft.com/fwlink/?LinkId=158730.  
  
 For more information, see [<defaultProxy\> Element (Network Settings)](../Topic/%3CdefaultProxy%3E%20Element%20\(Network%20Settings\).md).  
  
## ClickOnce and Web Browser Compatibility  
 Currently, ClickOnce installations will launch only if the URL to the deployment manifest is opened using Internet Explorer. A deployment whose URL is launched from another application, such as Microsoft Office Outlook, will launch successfully only if Internet Explorer is set as the default Web browser.  
  
> [!NOTE]
>  Mozilla Firefox is supported if the deployment provider is not blank or the Microsoft .NET Framework Assistant extension is installed. This extension is packaged with .NET Framework 3.5 SP1. For XBAP support, the NPWPF plug-in is activated when needed.  
  
## Activating ClickOnce Applications Through Browser Scripting  
 If you have developed a custom Web page that launches a ClickOnce application using Active Scripting, you may find that the application will not launch on some machines. Internet Explorer contains a setting called **Automatic prompting for file downloads**, which affects this behavior. This setting is available on the **Security** Tab in its **Options** menu that affects this behavior. It is called **Automatic prompting for file downloads**, and it is listed underneath the **Downloads** category. The property is set to **Enable** by default for intranet Web pages, and to **Disable** by default for Internet Web pages. When this setting is set to **Disable**, any attempt to activate a ClickOnce application programmatically (for example, by assigning its URL to the `document.location` property) will be blocked. Under this circumstance, users can launch applications only through a user-initiated download, for example, by clicking a hyperlink set to the application's URL.  
  
## Additional Server Configuration Issues  
  
##### Administrator Permissions Required  
 You must have Administrator permissions on the target server if you are publishing with HTTP. IIS requires this permissions level. If you are not publishing using HTTP, you only need write permission on the target path.  
  
##### Server Authentication Issues  
 When you publish to a remote server that has "Anonymous Access" turned off, you will receive the following warning:  
  
```  
"The files could not be downloaded from http://<remoteserver>/<myapplication>/.  The remote server returned an error: (401) Unauthorized."  
```  
  
> [!NOTE]
>  You can make NTLM (NT challenge-response) authentication work if the site prompts for credentials other than your default credentials, and, in the security dialog box, you click **OK** when you are prompted if you want to save the supplied credentials for future sessions. However, this workaround will not work for basic authentication.  
  
## Using Third-Party Web Servers  
 If you are deploying a ClickOnce application from a Web server other than IIS, you may experience a problem if the server is returning the incorrect content type for key ClickOnce files, such as the deployment manifest and application manifest. To resolve this problem, see your Web server's Help documentation about how to add new content types to the server, and make sure that all the file name extension mappings listed in the following table are in place.  
  
|File name extension|Content type|  
|-------------------------|------------------|  
|`.application`|`application/x-ms-application`|  
|`.manifest`|`application/x-ms-manifest`|  
|`.deploy`|`application/octet-stream`|  
|`.msu`|`application/octet-stream`|  
|`.msp`|`application/octet-stream`|  
  
## ClickOnce and Mapped Drives  
 If you use Visual Studio to publish a ClickOnce application, you cannot specify a mapped drive as the installation location. However, you can modify the ClickOnce application to install from a mapped drive by using the Manifest Generator and Editor (Mage.exe and MageUI.exe). For more information, see [Mage.exe (Manifest Generation and Editing Tool)](../Topic/Mage.exe%20\(Manifest%20Generation%20and%20Editing%20Tool\).md) and [MageUI.exe (Manifest Generation and Editing Tool, Graphical Client)](../Topic/MageUI.exe%20\(Manifest%20Generation%20and%20Editing%20Tool,%20Graphical%20Client\).md).  
  
## FTP Protocol Not Supported for Installing Applications  
 ClickOnce supports installing applications from any HTTP 1.1 Web server or file server. FTP, the File Transfer Protocol, is not supported for installing applications. You can use FTP to publish applications only. The following table summarizes these differences:  
  
|URL Type|Description|  
|--------------|-----------------|  
|ftp://|You can publish a ClickOnce application by using this protocol.|  
|http://|You can install a ClickOnce application by using this protocol.|  
|https://|You can install a ClickOnce application by using this protocol.|  
|file://|You can install a ClickOnce application by using this protocol.|  
  
## Windows XP SP2: Windows Firewall  
 By default, Windows XP SP2 enables the Windows Firewall. If you are developing your application on a computer that has Windows XP installed, you are still able to publish and run ClickOnce applications from the local server that is running IIS. However, you cannot access that server that is running IIS from another computer unless you open the Windows Firewall. See Windows Help for instructions on managing the Windows Firewall.  
  
## Windows Server: Enable FrontPage server extensions  
 FrontPage Server Extensions from Microsoft is required for publishing applications to a Windows Web server that uses HTTP.  
  
 By default, Windows Server does not have FrontPage Server Extensions installed. If you want to use Visual Studio to publish to a Windows Server Web server that uses HTTP with FrontPage Server Extensions, you must install FrontPage Server Extensions first. You can perform the installation by using the Manage Your Server administration tool in Windows Server.  
  
## Windows Server: Locked-Down Content Types  
 IIS on Windows Server 2003 locks down all file types except for certain known content types (for example, .htm, .html, .txt, and so on). To enable deployment of ClickOnce applications using this server, you need to change the IIS settings to allow downloading files of type .application, .manifest, and any other custom file types used by your application.  
  
 If you deploy using an IIS server, run inetmgr.exe and add new File Types for the default Web page:  
  
-   For the .application and .manifest extensions, the MIME type should be "application/x-ms-application." For other file types, the MIME type should be "application/octet-stream."  
  
-   If you create a MIME type with extension "*" and the MIME type "application/octet-stream," it will allow files of unblocked file type to be downloaded. (However, blocked file types such as .aspx and .asmx cannot be downloaded.)  
  
 For specific instructions on configuring MIME types on Windows Server, refer to Microsoft Knowledge Base article KB326965, "IIS 6.0 Does Not Serve Unknown MIME Types" at [http://support.microsoft.com/default.aspx?scid=kb;en-us;326965](http://support.microsoft.com/default.aspx?scid=kb;en-us;326965).  
  
## Content Type Mappings  
 When publishing over HTTP, the content type (also known as MIME type) for the .application file should be "application/x-ms-application." If you have .NET Framework 2.0 installed on the server, this will be set for you automatically. If this is not installed, then you need to create a MIME type association for the ClickOnce application vroot (or entire server).  
  
 If you deploy using an IIS server, run inetmgr.exe and add a new content type of "application/x-ms-application" for the .application extension.  
  
## HTTP Compression Issues  
 With ClickOnce, you can perform downloads that use HTTP compression, a Web server technology that uses the GZIP algorithm to compress a data stream before sending the stream to the client. The client—in this case, ClickOnce—decompresses the stream before reading the files.  
  
 If you are using IIS, you can easily enable HTTP compression. However, when you enable HTTP compression, it is only enabled for certain file types—namely, HTML and text files. To enable compression for assemblies (.dll), XML (.xml), deployment manifests (.application), and application manifests (.manifest), you must add these file types to the list of types for IIS to compress. Until you add the file types to your deployment, only text and HTML files will be compressed.  
  
 For detailed instructions for IIS, see [How to specify additional document types for HTTP compression](http://go.microsoft.com/fwlink/?LinkId=178459).  
  
## See Also  
 [Troubleshooting ClickOnce Deployments](../VS_IDE/Troubleshooting-ClickOnce-Deployments.md)   
 [Choosing a ClickOnce Deployment Strategy](../VS_IDE/Choosing-a-ClickOnce-Deployment-Strategy.md)   
 [Application Deployment Prerequisites](../VS_IDE/Application-Deployment-Prerequisites.md)