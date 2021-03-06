---
title: "如何：繫結至 XML 查詢結果的 XDocument、XElement 或 LINQ"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data binding [WPF], binding to XDocument
- data binding [WPF], binding to XElement
ms.assetid: 6a629a49-fe1c-465d-b76a-3dcbf4307b64
caps.latest.revision: "21"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: ceb6023157d487aebeff4fb5335b58c0958f2851
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-bind-to-xdocument-xelement-or-linq-for-xml-query-results"></a>如何：繫結至 XML 查詢結果的 XDocument、XElement 或 LINQ
此範例示範如何將繫結至 XML 資料<xref:System.Windows.Controls.ItemsControl>使用<xref:System.Xml.Linq.XDocument>。  
  
## <a name="example"></a>範例  
 下列 XAML 程式碼定義<xref:System.Windows.Controls.ItemsControl>並包含類型之資料的資料範本`Planet`中`http://planetsNS`XML 命名空間。 佔用命名空間的 XML 資料類型必須將命名空間放在大括號中，而如果它出現在 XAML 標記延伸可能出現的位置，則必須在命名空間前面加上大括號逸出序列。 此程式碼會繫結至動態屬性會對應至<xref:System.Xml.Linq.XContainer.Element%2A>和<xref:System.Xml.Linq.XElement.Attribute%2A>方法<xref:System.Xml.Linq.XElement>類別。 動態屬性可以讓 XAML 繫結至共用方法名稱的動態屬性。 若要深入了解，請參閱 [LINQ to XML 動態屬性](/visualstudio/designers/linq-to-xml-dynamic-properties)。 請注意，XML 的預設命名空間宣告不適用於屬性名稱。  
  
 [!code-xaml[XLinqExample#StackPanelResources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml#stackpanelresources)]  
[!code-xaml[XLinqExample#ItemsControl](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml#itemscontrol)]  
  
 下列 C# 程式碼呼叫<xref:System.Xml.Linq.XDocument.Load%2A>然後堆疊面板資料內容設為所指名項目的所有子元素`SolarSystemPlanets`中`http://planetsNS`XML 命名空間。  
  
 [!code-csharp[XLinqExample#LoadDCFromFile](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml.cs#loaddcfromfile)]
 [!code-vb[XLinqExample#LoadDCFromFile](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/XLinqExample/visualbasic/window1.xaml.vb#loaddcfromfile)]  
  
 XML 資料可以儲存為 XAML 資源使用<xref:System.Windows.Data.ObjectDataProvider>。 如需完整的範例，請參閱 [L2DBForm.xaml 原始程式碼](http://msdn.microsoft.com/library/624e96d4-6d27-4195-8ac2-2f3835f6c57e)。 下列範例顯示程式碼如何將資料內容設定為物件資源。  
  
 [!code-csharp[XLinqExample#LoadDCFromXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml.cs#loaddcfromxaml)]
 [!code-vb[XLinqExample#LoadDCFromXAML](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/XLinqExample/visualbasic/window1.xaml.vb#loaddcfromxaml)]  
  
 動態屬性會對應至<xref:System.Xml.Linq.XContainer.Element%2A>和<xref:System.Xml.Linq.XElement.Attribute%2A>提供 XAML 中的彈性。 您的程式碼也可以繫結至 LINQ for XML 查詢的結果。 此範例會繫結至依照元素值排序的查詢結果。  
  
 [!code-csharp[XLinqExample#BindToResults](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml.cs#bindtoresults)]
 [!code-vb[XLinqExample#BindToResults](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/XLinqExample/visualbasic/window1.xaml.vb#bindtoresults)]  
  
## <a name="see-also"></a>請參閱  
 [繫結來源概觀](../../../../docs/framework/wpf/data/binding-sources-overview.md)  
 [WPF 資料繫結與 LINQ to XML 概觀](/visualstudio/designers/wpf-data-binding-with-linq-to-xml-overview)  
 [使用 LINQ to XML 的 WPF 資料繫結範例](/visualstudio/designers/wpf-data-binding-using-linq-to-xml-example)  
 [LINQ to XML 動態屬性](/visualstudio/designers/linq-to-xml-dynamic-properties)
