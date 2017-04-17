---
title: "Implementing the UI Automation SelectionItem Control Pattern | Microsoft Docs"
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
  - "Selection Item control pattern"
  - "UI Automation, Selection Item control pattern"
  - "control patterns, Selection Item"
ms.assetid: 76b0949a-5b23-4cfc-84cc-154f713e2e12
caps.latest.revision: 22
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 22
---
# Implementing the UI Automation SelectionItem Control Pattern
> [!NOTE]
>  這份文件適用於想要使用 <xref:System.Windows.Automation> 命名空間中定義之 Managed [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 類別的 .NET Framework 開發人員。 如需 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 的最新資訊，請參閱 [Windows Automation API：使用者介面自動化](http://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主題簡介實作 <xref:System.Windows.Automation.Provider.ISelectionItemProvider> 的方針和慣例，包括屬性、方法和事件的相關資訊。 其他參考的連結會在概觀的結尾列出。  
  
 <xref:System.Windows.Automation.SelectionItemPattern> 控制項模式用來支援控制項，其支援的控制項作用如同實作 <xref:System.Windows.Automation.Provider.ISelectionProvider> 之容器控制項的個別可選取子項目。 如需實作選取項目控制項模式的控制項，請參閱[Control Pattern Mapping for UI Automation Clients](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md)。  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## 實作方針和慣例  
 實作選取項目控制項模式時，請注意下列方針和慣例：  
  
-   若單一選取控制項有實作 <xref:System.Windows.Automation.Provider.IRawElementProviderFragmentRoot> 的子控制項，例如 \[顯示內容\] 對話方塊中的 \[螢幕解析度\] 滑桿，應實作 <xref:System.Windows.Automation.Provider.ISelectionProvider>，且其子系應實作 <xref:System.Windows.Automation.Provider.IRawElementProviderFragment> 和 <xref:System.Windows.Automation.Provider.ISelectionItemProvider>。  
  
<a name="Required_Members_for_the_IValueProvider_Interface"></a>   
## ISelectionItemProvider 的必要成員  
 實作 <xref:System.Windows.Automation.Provider.ISelectionItemProvider> 需要下列屬性、方法和事件。  
  
|必要成員|成員類型|備註|  
|----------|----------|--------|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.CanSelectMultiple%2A>|屬性|無|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.IsSelectionRequired%2A>|屬性|無|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.GetSelection%2A>|方法|無|  
|<xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent>|事件|當容器中的選項大幅變更，需要傳送比 <xref:System.Windows.Automation.Provider.AutomationInteropProvider.InvalidateLimit> 常數所允許的更多 <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent> 和 <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent> 事件時，就會引發此事件。|  
  
-   如果 <xref:System.Windows.Automation.SelectionItemPattern.Select%2A>、<xref:System.Windows.Automation.SelectionItemPattern.AddToSelection%2A> 或 <xref:System.Windows.Automation.SelectionItemPattern.RemoveFromSelection%2A> 的結果是單一選取的項目，則應引發 <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent>，否則應視情況傳送 <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementAddedToSelectionEvent>\/ <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent>。  
  
<a name="Exceptions"></a>   
## 例外狀況  
 提供者必須擲回下列例外狀況。  
  
|例外狀況類型|條件|  
|------------|--------|  
|<xref:System.InvalidOperationException>|當嘗試下列任一項時：<br /><br /> -   在 <xref:System.Windows.Automation.SelectionPattern.IsSelectionRequiredProperty> \= `true` 且已選取項目的單一選取容器上呼叫 <xref:System.Windows.Automation.Provider.ISelectionItemProvider.RemoveFromSelection%2A>。<br />-   在 <xref:System.Windows.Automation.SelectionPattern.IsSelectionRequiredProperty> \= `true` 且只選取一個項目的多重選取容器上呼叫 <xref:System.Windows.Automation.Provider.ISelectionItemProvider.RemoveFromSelection%2A>。<br />-   在 <xref:System.Windows.Automation.SelectionPattern.CanSelectMultipleProperty> \= `false` 且已選取另一個項目的單一選取容器上呼叫 <xref:System.Windows.Automation.Provider.ISelectionItemProvider.AddToSelection%2A>。|  
  
## 請參閱  
 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [Support Control Patterns in a UI Automation Provider](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)   
 [UI Automation Control Patterns for Clients](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [Implementing the UI Automation Selection Control Pattern](../../../docs/framework/ui-automation/implementing-the-ui-automation-selection-control-pattern.md)   
 [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)   
 [Use Caching in UI Automation](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)   
 [Fragment Provider Sample](http://msdn.microsoft.com/zh-tw/778ef1bc-8610-4bc9-886e-aeff94a8a13e)