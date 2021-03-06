---
title: "如何：建立簡單繫結"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- simple binding [WPF], creating
- data binding [WPF], creating simple bindings
- binding data [WPF], creating
ms.assetid: 69b80f72-6259-44cb-8294-5bdcebca1e08
caps.latest.revision: 
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: a595f255b014e08b4b5b2036a7b1940e46df268f
ms.sourcegitcommit: 973a12d1e6962cd9a9c263fbfaad040ec8267fe9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/22/2018
---
# <a name="how-to-create-a-simple-binding"></a>如何：建立簡單繫結
此範例將示範如何建立簡單<xref:System.Windows.Data.Binding>。  
  
## <a name="example"></a>範例  
 在此範例中，您必須`Person`物件具有名為字串屬性`PersonName`。 `Person`物件定義在命名空間稱為`SDKSample`。  
  
 包含反白顯示的列`<src>`項目，在下列範例會具現化`Person`物件`PersonName`屬性值為`Joe`。 這是`Resources`區段，並指派`x:Key`。  
  
 [!code-xaml[SimpleBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml?highlight=9,37)]  
  
 包含反白顯示的列`<TextBlock>`接著繫結項目<xref:System.Windows.Controls.TextBlock>控制權傳輸至`PersonName`屬性。 如此一來，<xref:System.Windows.Controls.TextBlock>隨即出現，並 「 Joe"的值。  
  
## <a name="see-also"></a>請參閱  
 [資料繫結概觀](../../../../docs/framework/wpf/data/data-binding-overview.md)  
 [HOW-TO 主題](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)
