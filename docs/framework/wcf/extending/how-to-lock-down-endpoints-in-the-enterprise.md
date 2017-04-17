---
title: "HOW TO：鎖定企業的端點 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1b7eaab7-da60-4cf7-9d6a-ec02709cf75d
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# HOW TO：鎖定企業的端點
大型企業通常需要在遵循企業安全性原則的環境中開發應用程式。  下列主題討論如何開發與安裝用戶端端點驗證器，以用於驗證所有安裝在電腦上的 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 用戶端應用程式。  
  
 在這種情況下，驗證程式會是用戶端驗證程式，因為這個端點行為會加入 machine.config 檔案中的用戶端 [\<commonBehaviors\>](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md) 區段。  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 只會為用戶端應用程式載入通用端點行為，並且只會為服務應用程式載入通用服務行為。  若要為服務應用程式安裝這個相同的驗證器，驗證器必須是服務行為。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [\<commonBehaviors\>](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md) 區段。  
  
> [!IMPORTANT]
>  當應用程式在部分信任環境中執行時，加入組態檔的 [\<commonBehaviors\>](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md) 區段但未以 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 屬性 \(APTCA\) 標記的服務或端點行為不會執行，並且發生這種情況時，也不會擲回例外狀況。  若要強制執行通用行為 \(例如驗證器\)，您必須執行下列其中一項：  
>   
>  \-\- 使用 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 屬性標記您的通用行為，讓它可以在部署為部分信任應用程式時執行。  請注意，您可以在電腦上設定登錄項目，以防止已標記 APTCA 的組件執行。  
>   
>  \-\- 確定應用程式是否會部署為完全信任的應用程式，而使用者是否無法修改程式碼存取安全性設定以在部分信任環境中執行應用程式。  如果可以執行這項操作，自訂驗證器就不會執行，也不會擲回例外狀況。  如需確保這項操作的一種方法，請參閱使用[程式碼存取安全性原則工具 \(Caspol.exe\)](http://go.microsoft.com/fwlink/?LinkId=248222) 的 `levelfinal` 選項。  
>   
>  如需詳細資訊，請參閱[部分信任最佳做法](../../../../docs/framework/wcf/feature-details/partial-trust-best-practices.md)和[支援的部署案例](../../../../docs/framework/wcf/feature-details/supported-deployment-scenarios.md)。  
  
### 若要建立端點驗證器  
  
1.  以 <xref:System.ServiceModel.Description.IEndpointBehavior> 方法中所需的驗證步驟建立 <xref:System.ServiceModel.Description.IEndpointBehavior.Validate%2A>。  下列程式碼提供一個範例。  \(`InternetClientValidatorBehavior` 取自[安全性驗證](../../../../docs/framework/wcf/samples/security-validation.md)範例。\)  
  
     [!code-csharp[LockdownValidation#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/internetclientvalidatorbehavior.cs#2)]  
  
2.  建立新的 <xref:System.ServiceModel.Configuration.BehaviorExtensionElement>，它會註冊步驟 1 中建立的端點驗證器。  下列程式碼範例會顯示這點。  \(這個範例的原始程式碼位於[安全性驗證](../../../../docs/framework/wcf/samples/security-validation.md)範例中。\)  
  
     [!code-csharp[LockdownValidation#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/internetclientvalidatorelement.cs#3)]  
  
3.  請務必以強式名稱簽署編譯的組件。  如需詳細資訊，請參閱[強式名稱工具 \(SN.EXE\)](http://go.microsoft.com/fwlink/?LinkId=248217) 和您語言的編譯器命令。  
  
### 若要將驗證器安裝至目標電腦  
  
1.  使用適當的機制安裝端點驗證器。  在企業中，您可以使用群組原則和 Systems Management Server \(SMS\) 安裝端點驗證器。  
  
2.  使用 [Gacutil.exe \(全域組件快取工具\)](http://msdn.microsoft.com/library/ex0ss12c\(v=vs.110\).aspx) 將強式名稱的組件安裝至全域組件快取中。  
  
3.  使用 <xref:System.Configuration?displayProperty=fullName> 命名空間型別以：  
  
    1.  使用完整類型名稱將延伸加入 [\<behaviorExtensions\>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviorextensions.md) 區段，並鎖定項目。  
  
         [!code-csharp[LockdownValidation#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#5)]  
  
    2.  將行為項目加入 [\<commonBehaviors\>](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md) 區段的 `EndpointBehaviors` 屬性，並鎖定項目。  \(若要在服務上安裝驗證器，驗證器必須是 <xref:System.ServiceModel.Description.IServiceBehavior> 並加入至 `ServiceBehaviors` 屬性\)。 下列程式碼範例將示範如何在步驟 a.  和 b. 後進行適當的設定，唯一的例外是沒有強式名稱時。  
  
         [!code-csharp[LockdownValidation#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#6)]  
  
    3.  儲存 machine.config 檔。  下列程式碼範例執行步驟 3 中所有的工作，但將修改過的 machine.config 檔案複本儲存在本機上。  
  
         [!code-csharp[LockdownValidation#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#7)]  
  
## 範例  
 下列程式碼範例示範如何將通用行為新增至 machine.config 檔案，並將複本儲存至磁碟上。  `InternetClientValidatorBehavior` 取自[安全性驗證](../../../../docs/framework/wcf/samples/security-validation.md)範例。  
  
 [!code-csharp[LockdownValidation#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#1)]  
  
## .NET Framework 安全性  
 您可能也要加密組態檔項目。  如需詳細資訊，請參閱「請參閱」一節。  
  
## 請參閱  
 [使用 DPAPI 的加密組態檔項目](http://go.microsoft.com/fwlink/?LinkId=94954)   
 [使用 RSA 的加密組態檔項目](http://go.microsoft.com/fwlink/?LinkId=94955)