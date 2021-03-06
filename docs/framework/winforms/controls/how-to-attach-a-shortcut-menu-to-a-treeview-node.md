---
title: "如何：將捷徑功能表附加至 TreeView 節點"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- shortcut menus [Windows Forms], adding to TreeView controls
- TreeView control [Windows Forms], adding shortcut menus
- tree nodes in TreeView control [Windows Forms], shortcut menus
ms.assetid: a23c6752-fd8f-44ad-b781-bab37962fc7c
caps.latest.revision: "11"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: ca251c9dec87db0ecb4b565b522839ace7f44479
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-attach-a-shortcut-menu-to-a-treeview-node"></a>如何：將捷徑功能表附加至 TreeView 節點
Windows Form<xref:System.Windows.Forms.TreeView>控制項會顯示節點階層，類似於檔案和資料夾顯示在 Windows 檔案總管 的左窗格中。 藉由設定<xref:System.Windows.Forms.Control.ContextMenuStrip%2A>屬性，您可以向使用者提供即時線上作業，當它們以滑鼠右鍵按一下<xref:System.Windows.Forms.TreeView>控制項。 透過建立關聯<xref:System.Windows.Forms.ContextMenuStrip>具有個別元件<xref:System.Windows.Forms.TreeNode>項目，您可以加入自訂層級的快顯功能表功能，以您<xref:System.Windows.Forms.TreeView>控制項。  
  
### <a name="to-associate-a-shortcut-menu-with-a-treenode-programmatically"></a>以程式設計的方式與樹狀結構節點的捷徑功能表  
  
1.  具現化<xref:System.Windows.Forms.TreeView>控制項具有適當的屬性設定，建立根目錄<xref:System.Windows.Forms.TreeNode>，然後再加入子節點。  
  
2.  具現化<xref:System.Windows.Forms.ContextMenuStrip>元件，然後再加入<xref:System.Windows.Forms.ToolStripMenuItem>您想要在執行階段提供每一項作業。  
  
3.  設定<xref:System.Windows.Forms.TreeNode.ContextMenuStrip%2A>屬性的適當<xref:System.Windows.Forms.TreeNode>您所建立的快顯功能表。  
  
4.  當設定這個屬性時，當您以滑鼠右鍵按一下節點將顯示的捷徑功能表。  
  
 下列程式碼範例會建立基本<xref:System.Windows.Forms.TreeView>和<xref:System.Windows.Forms.ContextMenuStrip>根相關聯<xref:System.Windows.Forms.TreeNode>的<xref:System.Windows.Forms.TreeView>。 您必須自訂功能表選項，以符合<xref:System.Windows.Forms.TreeView>您所開發。 此外，您會想要撰寫程式碼以處理<xref:System.Windows.Forms.ToolStripItem.Click>事件的這些功能表項目。  
  
 [!code-cpp[System.Windows.Forms.TreeNodeContextMenuStrip#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/system.windows.forms.TreeNodeContextMenuStrip/cpp/Form1.cpp#1)]
 [!code-csharp[System.Windows.Forms.TreeNodeContextMenuStrip#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/system.windows.forms.TreeNodeContextMenuStrip/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.TreeNodeContextMenuStrip#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/system.windows.forms.TreeNodeContextMenuStrip/VB/Form1.vb#1)]  
  
## <a name="see-also"></a>請參閱  
 <xref:System.Windows.Forms.ContextMenuStrip>  
 [TreeView 控制項](../../../../docs/framework/winforms/controls/treeview-control-windows-forms.md)
