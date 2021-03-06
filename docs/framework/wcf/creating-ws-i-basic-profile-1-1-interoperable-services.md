---
title: "建立 WS-I Basic Profile 1.1 互通服務"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- configuration [WCF], interoperable services
ms.assetid: 91b70a21-8f5c-4679-808c-2ed5fa6b2013
caps.latest.revision: 
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: d6bef68c8ba433e902cfd50e59a3b343e3af08cd
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="creating-ws-i-basic-profile-11-interoperable-services"></a>建立 WS-I Basic Profile 1.1 互通服務
將 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服務端點設成與 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] Web 服務用戶端互通：  
  
-   使用 <xref:System.ServiceModel.BasicHttpBinding?displayProperty=nameWithType> 型別作為服務端點的繫結型別。  
  
-   請勿使用回呼與工作階段合約功能，或在您服務端點上的交易行為  
  
 您可選擇啟用 HTTPS 支援及對繫結的傳輸層級用戶端驗證。  
  
 <xref:System.ServiceModel.BasicHttpBinding> 類別的下列功能需要 WS-I Basic Profile 1.1 以外的功能：  
  
-   訊息傳輸最佳化機制 (MTOM) 的訊息加密是由 <xref:System.ServiceModel.BasicHttpBinding.MessageEncoding%2A?displayProperty=nameWithType> 屬性控制。 將此屬性保留為預設值，也就是 <xref:System.ServiceModel.WSMessageEncoding.Text?displayProperty=nameWithType> 不使用 MTOM。  
  
-   <xref:System.ServiceModel.BasicHttpBinding.Security%2A?displayProperty=nameWithType> 值所控制的訊息安全性，提供符合 WS-I Basic Security Profile 1.0 的 WS-Security 支援。 將此屬性保留為預設值，也就是 <xref:System.ServiceModel.SecurityMode.Transport?displayProperty=nameWithType> 不使用 WS-Security。  
  
 若要將中繼資料給[!INCLUDE[indigo2](../../../includes/indigo2-md.md)]可用來服務[!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)]，使用 Web 服務用戶端產生工具： [Web 服務描述語言工具 (Wsdl.exe)](http://msdn.microsoft.com/library/b9210348-8bc2-4367-8c91-d1a04b403e88)， [Web 服務探索工具 (Disco.exe)](http://msdn.microsoft.com/library/acd88078-c581-42bc-94ca-6633e2851979)，而`Add Web Reference`功能[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]; 您必須啟用發行中繼資料。 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][發行中繼資料端點](../../../docs/framework/wcf/publishing-metadata-endpoints.md)。  
  
## <a name="example"></a>範例  
  
### <a name="description"></a>描述  
 下列程式碼範例示範如何將[!INCLUDE[indigo2](../../../includes/indigo2-md.md)]與相容的端點[!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)]Web 服務用戶端程式碼中的，或者，在組態檔中。  
  
### <a name="code"></a>程式碼  
 [!code-csharp[C_HowTo-WCFServiceAndASMXClient#0](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto-wcfserviceandasmxclient/cs/program.cs#0)]
 [!code-vb[C_HowTo-WCFServiceAndASMXClient#0](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto-wcfserviceandasmxclient/vb/program.vb#0)]  
 [!code-xml[C_HowTo-WCFServiceAndASMXClient#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto-wcfserviceandasmxclient/common/app.config#1)]  
  
## <a name="see-also"></a>請參閱  
 [與 ASP.NET Web 服務的互通性](../../../docs/framework/wcf/feature-details/interop-with-aspnet-web-services.md)
