---
title: "Implementing the UI Automation Grid Control Pattern | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "control patterns, grid"
  - "grid control pattern"
  - "UI Automation, grid control pattern"
ms.assetid: 234d11a0-7ce7-4309-8989-2f4720e02f78
caps.latest.revision: 27
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 27
---
# Implementing the UI Automation Grid Control Pattern
> [!NOTE]
>  這份文件適用於想要使用 <xref:System.Windows.Automation> 命名空間中定義之 Managed [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 的最新資訊，請參閱 [Windows Automation API：使用者介面自動化](http://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主題簡介實作 <xref:System.Windows.Automation.Provider.IGridProvider> 的方針和慣例，包括屬性、方法和事件的相關資訊。 其他參考的連結會在概觀的結尾列出。  
  
 <xref:System.Windows.Automation.GridPattern> 控制項模式是用以支援當作子項目集合的容器使用的控制項。 此項目的子系必須實作 <xref:System.Windows.Automation.Provider.IGridItemProvider>，並組合管理成資料列與資料行可周遊的二維邏輯座標系統。 如需實作此控制項模式的控制項範例，請參閱[Control Pattern Mapping for UI Automation Clients](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md)。  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## 實作方針和慣例  
 實作方格控制項模式時，請注意下列方針和慣例：  
  
-   方格座標是從左上角 \(或根據地區為右上儲存格\) 以零為起始，座標為 \(0, 0\)。  
  
-   如果儲存格是空的，仍必須傳回使用者介面自動化項目，才能支援該儲存格的 <xref:System.Windows.Automation.Provider.IGridItemProvider.ContainingGrid%2A> 屬性。 當子項目在方格中的配置類似不完全陣列 \(請參閱以下範例\)，就可能發生這種情形。  
  
 ![顯示不完全配置的 Windows 檔案總管檢視](../../../docs/framework/ui-automation/media/uia-gridpattern-ragged-array.PNG "UIA\_GridPattern\_Ragged\_Array")  
座標是空的方格控制項範例  
  
-   單一項目的方格仍必須實作 <xref:System.Windows.Automation.Provider.IGridProvider>，才能在邏輯上視為是方格。 方格中的子項目數為多少都沒關係。  
  
-   根據提供者實作而定，隱藏資料列和資料行可能會載入到 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 樹狀結構，因此會反映在 <xref:System.Windows.Automation.GridPattern.GridPatternInformation.RowCount%2A> 和 <xref:System.Windows.Automation.GridPattern.GridPatternInformation.ColumnCount%2A> 屬性。 如果隱藏資料列和資料行未載入，則應不會列入計數。  
  
-   <xref:System.Windows.Automation.Provider.IGridProvider> 不會啟用方格的使用中操作，而必須實作 <xref:System.Windows.Automation.Provider.ITransformProvider> 才能啟用此功能。  
  
-   使用 <xref:System.Windows.Automation.StructureChangedEventHandler> 接聽方格的結構或配置變更，例如新增、移除或合併儲存格。  
  
-   使用 <xref:System.Windows.Automation.AutomationFocusChangedEventHandler> 追蹤方格項目或儲存格的周遊情形。  
  
<a name="Required_Members_for_IGridProvider"></a>   
## IGridProvider 的必要成員  
 以下是實作 IGridProvider 介面的必要屬性和方法。  
  
|必要成員|類型|備註|  
|----------|--------|--------|  
|<xref:System.Windows.Automation.Provider.IGridProvider.RowCount%2A>|屬性|無|  
|<xref:System.Windows.Automation.Provider.IGridProvider.ColumnCount%2A>|屬性|無|  
|<xref:System.Windows.Automation.Provider.IGridProvider.GetItem%2A>|方法|無|  
  
 此控制項模式沒有任何相關聯的事件。  
  
<a name="Exceptions"></a>   
## 例外狀況  
 提供者必須擲回下列例外狀況。  
  
|例外狀況類型|條件|  
|------------|--------|  
|<xref:System.ArgumentOutOfRangeException>|<xref:System.Windows.Automation.Provider.IGridProvider.GetItem%2A><br /><br /> -   如果要求的資料列座標大於 <xref:System.Windows.Automation.Provider.IGridProvider.RowCount%2A> 或資料行座標大於 <xref:System.Windows.Automation.Provider.IGridProvider.ColumnCount%2A>。|  
|<xref:System.ArgumentOutOfRangeException>|<xref:System.Windows.Automation.Provider.IGridProvider.GetItem%2A><br /><br /> -   如果要求的資料列或資料行座標小於零。|  
  
## 請參閱  
 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [Support Control Patterns in a UI Automation Provider](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)   
 [UI Automation Control Patterns for Clients](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [Implementing the UI Automation GridItem Control Pattern](../../../docs/framework/ui-automation/implementing-the-ui-automation-griditem-control-pattern.md)   
 [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)   
 [Use Caching in UI Automation](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)