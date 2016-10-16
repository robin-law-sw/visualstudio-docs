---
title: "Compiler Error CS0656"
ms.custom: na
ms.date: 10/01/2016
ms.devlang: 
  - CSharp
ms.prod: visual-studio-dev14
ms.reviewer: na
ms.suite: na
ms.technology: 
  - devlang-csharp
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e695280a-e75d-4e8c-aec2-1f3fb455544a
caps.latest.revision: 6
manager: douge
translation.priority.ht: 
  - de-de
  - es-es
  - fr-fr
  - it-it
  - ja-jp
  - ko-kr
  - ru-ru
  - zh-cn
  - zh-tw
translation.priority.mt: 
  - cs-cz
  - pl-pl
  - pt-br
  - tr-tr
---
# Compiler Error CS0656
Missing compiler required member 'object.member'  
  
 One of the following problems exists:  
  
-   Your installation of the common language runtime is corrupt.  
  
-   You have a reference to an assembly that defines a type that is also found in the common language runtime. However, your assembly's type is not defined the way the C# compiler expects.  
  
 Check your references to ensure that you are using the correct version of the common language runtime.