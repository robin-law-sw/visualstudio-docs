---
title: "Compiler Error CS0736"
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
ms.assetid: 06b14feb-81d5-495f-ab2d-6dc3f5e7216f
caps.latest.revision: 7
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
# Compiler Error CS0736
'type name' does not implement interface member 'member name'. 'method name' cannot implement an interface member because it is static.  
  
 This error is generated when a static method is either implicitly or explicitly declared as an implementation of an interface member.  
  
### To correct this error  
  
-   Remove the [static](../Topic/static%20\(C%23%20Reference\).md) modifier from the method declaration.  
  
-   Change the name of the interface method.  
  
-   Redefine the containing type so that it does not inherit from the interface.  
  
## Example  
 The following code generates CS0736 because `Program.testMethod` is declared as static:  
  
```  
// cs0736.cs  
namespace CS0736  
{     
  
    interface ITest  
    {  
        int testMethod(int x);  
    }  
  
    class Program : ITest // CS0736  
    {  
        public static int testMethod(int x) { return 0; }  
        // Try the following line instead.  
        // public int testMethod(int x) { return 0; }  
        public static void Main() { }  
    }      
}  
```  
  
## See Also  
 [Interfaces](../Topic/Interfaces%20\(C%23%20Programming%20Guide\).md)