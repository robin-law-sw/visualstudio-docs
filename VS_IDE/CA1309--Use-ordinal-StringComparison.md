---
title: "CA1309: Use ordinal StringComparison"
ms.custom: na
ms.date: 10/03/2016
ms.prod: visual-studio-dev14
ms.reviewer: na
ms.suite: na
ms.technology: 
  - vs-devops-test
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 19be0854-cb6e-4efd-a4c8-a5c1fc6f7a71
caps.latest.revision: 15
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
# CA1309: Use ordinal StringComparison
|||  
|-|-|  
|TypeName|UseOrdinalStringComparison|  
|CheckId|CA1309|  
|Category|Microsoft.Globalization|  
|Breaking Change|Non-breaking|  
  
## Cause  
 A string comparison operation that is nonlinguistic does not set the <xref:System.StringComparison?qualifyHint=False> parameter to either **Ordinal** or **OrdinalIgnoreCase**.  
  
## Rule Description  
 Many string operations, most important the <xref:System.String.Compare?qualifyHint=True> and <xref:System.String.Equals?qualifyHint=True> methods, now provide an overload that accepts a <xref:System.StringComparision?qualifyHint=True> enumeration value as a parameter.  
  
 When you specify either **StringComparison.Ordinal** or **StringComparison.OrdinalIgnoreCase**, the string comparison will be nonlinguistic. That is, the features that are specific to the natural language are ignored when comparison decisions are made. This means the decisions are based on simple byte comparisons and ignore casing or equivalence tables that are parameterized by culture. As a result, by explicitly setting the parameter to either the **StringComparison.Ordinal** or **StringComparison.OrdinalIgnoreCase**, your code often gains speed, increases correctness, and becomes more reliable.  
  
## How to Fix Violations  
 To fix a violation of this rule, change the string comparison method to an overload that accepts the <xref:System.StringComparison?qualifyHint=True> enumeration as a parameter, and specify either **Ordinal** or **OrdinalIgnoreCase**. For example, change `String.Compare(str1, str2)` to `String.Compare(str1, str2, StringComparison.Ordinal)`.  
  
## When to Suppress Warnings  
 It is safe to suppress a warning from this rule when the library or application is intended for a limited local audience or when the semantics of the current culture should be used.  
  
## See Also  
 [Globalization Warnings](../VS_IDE/Globalization-Warnings.md)   
 [CA1307: Specify StringComparison](../VS_IDE/CA1307--Specify-StringComparison.md)