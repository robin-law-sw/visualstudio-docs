---
title: "Compiler Error CS1908"
ms.custom: na
ms.date: "10/13/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: na
ms.suite: na
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: na
ms.topic: "article"
f1_keywords: 
  - "CS1908"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS1908"
ms.assetid: d7da31c2-48ef-4401-b885-3459b4d7f6f6
caps.latest.revision: 8
ms.author: "billchi"
manager: "douge"
translation.priority.ht: 
  - "de-de"
  - "es-es"
  - "fr-fr"
  - "it-it"
  - "ja-jp"
  - "ko-kr"
  - "ru-ru"
  - "zh-cn"
  - "zh-tw"
translation.priority.mt: 
  - "cs-cz"
  - "pl-pl"
  - "pt-br"
  - "tr-tr"
---
# Compiler Error CS1908
The type of the argument to the DefaultValue attribute must match the parameter type  
  
 This error is generated when you use the wrong argument for the \<xref:System.ComponentModel.DefaultValueAttribute> attribute value. Use a value that matches the parameter type.  
  
## Example  
 The following sample generates CS1908.  
  
```  
// CS1908.cs  
// compile with: /target:library  
using System.Runtime.InteropServices;  
  
public interface ISomeInterface  
{  
   void Bad([Optional] [DefaultParameterValue("true")] bool b);   // CS1908  
  
   void Good([Optional] [DefaultParameterValue(true)] bool b);   // OK  
}  
```