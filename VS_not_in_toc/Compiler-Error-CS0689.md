---
title: "Compiler Error CS0689"
ms.custom: na
ms.date: 10/02/2016
ms.devlang: 
  - CSharp
ms.prod: visual-studio-dev14
ms.reviewer: na
ms.suite: na
ms.technology: 
  - devlang-csharp
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c555c2e-8e71-4097-8dbf-52dbafe7bf57
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
# Compiler Error CS0689
Cannot derive from 'identifier' because it is a type parameter  
  
 Base classes or interfaces for generic classes cannot be specified by a type parameter. Derive from a specific class or interface, or a specific generic class instead, or include the unknown type as a member.  
  
 The following sample generates CS0689:  
  
```  
// CS0689.cs  
class A<T> : T   // CS0689  
{  
}  
```