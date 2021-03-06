---
title: "如何： 投影新類型 (LINQ to XML) (Visual Basic)"
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8cfb24f5-89b2-4cfb-b85d-e7963f8f1845
caps.latest.revision: "3"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 73b677e45be1d457d54de01331c93f60348e6bfd
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/18/2017
---
# <a name="how-to-project-a-new-type-linq-to-xml-visual-basic"></a>如何： 投影新類型 (LINQ to XML) (Visual Basic)
本節中的其他範例顯示的查詢會傳回結果，當做 <xref:System.Collections.Generic.IEnumerable%601> 之 <xref:System.Xml.Linq.XElement>, <xref:System.Collections.Generic.IEnumerable%601> 的 `string`，以及 <xref:System.Collections.Generic.IEnumerable%601> 的 `int`。 這些是常見的結果型別，但這些型別不適用於每個案例。 在許多情況下，您會希望您的查詢傳回其他型別的 <xref:System.Collections.Generic.IEnumerable%601>。  
  
## <a name="example"></a>範例  
 此範例顯示如何具現化 `Select` 子句中的物件。 此程式碼會先利用建構函式定義新的類別，然後修改 `Select` 陳述式，讓運算式成為新類別的新執行個體。  
  
 此範例使用下列 XML 文件︰[範例 XML 檔：典型採購訂單 (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-typical-purchase-order-linq-to-xml.md)。  
  
```vb  
Public Class NameQty  
    Public name As String  
    Public qty As Integer  
    Public Sub New(ByVal n As String, ByVal q As Integer)  
        name = n  
        qty = q  
    End Sub  
End Class  
  
Public Class Program  
    Shared Sub Main()  
        Dim po As XElement = XElement.Load("PurchaseOrder.xml")  
  
        Dim nqList As IEnumerable(Of NameQty) = _  
            From n In po...<Item> _  
            Select New NameQty( _  
                n.<ProductName>.Value, CInt(n.<Quantity>.Value))  
  
        For Each n As NameQty In nqList  
            Console.WriteLine(n.name & ":" & n.qty)  
        Next  
    End Sub  
End Class  
```  
  
 這個範例會使用`M:System.Xml.Linq.XElement.Element`方法主題中導入[How to： 擷取單一子項目 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-a-single-child-element-linq-to-xml.md)。 它也會使用轉換以擷取 `M:System.Xml.Linq.XElement.Element` 方法所傳回的元素值。  
  
 這個範例會產生下列輸出：  
  
```  
Lawnmower:1  
Baby Monitor:2  
```  
  
## <a name="see-also"></a>另請參閱  
 [投影和轉換 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/projections-and-transformations-linq-to-xml.md)
