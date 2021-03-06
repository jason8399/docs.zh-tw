---
title: "如何：變更 Windows Form ColorDialog 元件的外觀"
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
- ColorDialog component [Windows Forms], examples
- ColorDialog component [Windows Forms], formatting appearance
- color dialog box [Windows Forms], configuring appearance
ms.assetid: bba4e262-1cd7-4f63-89cf-330a36f7b539
caps.latest.revision: "13"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: af3a9ec6ba301a27a7940bc752ffaf12f345abec
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-change-the-appearance-of-the-windows-forms-colordialog-component"></a>如何：變更 Windows Form ColorDialog 元件的外觀
您可以設定 Windows Form 的外觀<xref:System.Windows.Forms.ColorDialog>元件使用其屬性的數目。 此對話方塊包含兩個區段，其中顯示基本色彩，可讓使用者定義自訂色彩的其中一個。  
  
 大部分的屬性會限制哪些使用者可以從對話方塊中選取的色彩。 如果<xref:System.Windows.Forms.ColorDialog.AllowFullOpen%2A>屬性設定為`true`，允許使用者定義自訂色彩。 <xref:System.Windows.Forms.ColorDialog.FullOpen%2A>屬性是`true`如果對話方塊中展開為定義自訂色彩; 否則，使用者必須按一下 」 定義自訂色彩 」 按鈕。 當<xref:System.Windows.Forms.ColorDialog.AnyColor%2A>屬性設定為`true`，對話方塊中顯示基本色彩集中的所有可用色彩。 如果<xref:System.Windows.Forms.ColorDialog.SolidColorOnly%2A>屬性設定為`true`，使用者無法選取遞色的色彩，則只有純色可用來選取。  
  
 如果<xref:System.Windows.Forms.ColorDialog.ShowHelp%2A>屬性設定為`true`，說明 按鈕會出現在對話方塊中。 當使用者按一下 [說明] 按鈕，<xref:System.Windows.Forms.ColorDialog>元件的<xref:System.Windows.Forms.CommonDialog.HelpRequest>就會引發事件。  
  
### <a name="to-configure-the-appearance-of-the-color-dialog-box"></a>若要設定 [色彩] 對話方塊的外觀  
  
1.  設定<xref:System.Windows.Forms.ColorDialog.AllowFullOpen%2A>， <xref:System.Windows.Forms.ColorDialog.AnyColor%2A>， <xref:System.Windows.Forms.ColorDialog.SolidColorOnly%2A>，和<xref:System.Windows.Forms.ColorDialog.ShowHelp%2A>所需值的屬性。  
  
    ```vb  
    ColorDialog1.AllowFullOpen = True  
    ColorDialog1.AnyColor = True  
    ColorDialog1.SolidColorOnly = False  
    ColorDialog1.ShowHelp = True  
    ```  
  
    ```csharp  
    colorDialog1.AllowFullOpen = true;  
    colorDialog1.AnyColor = true;  
    colorDialog1.SolidColorOnly = false;  
    colorDialog1.ShowHelp = true;  
    ```  
  
    ```cpp  
    colorDialog1->AllowFullOpen = true;  
    colorDialog1->AnyColor = true;  
    colorDialog1->SolidColorOnly = false;  
    colorDialog1->ShowHelp = true;  
    ```  
  
## <a name="see-also"></a>請參閱  
 <xref:System.Windows.Forms.ColorDialog>  
 [ColorDialog 元件](../../../../docs/framework/winforms/controls/colordialog-component-windows-forms.md)  
 [ColorDialog 元件概觀](../../../../docs/framework/winforms/controls/colordialog-component-overview-windows-forms.md)
