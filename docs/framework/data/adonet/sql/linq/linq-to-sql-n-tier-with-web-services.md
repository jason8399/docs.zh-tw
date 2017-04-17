---
title: "搭配 Web 服務使用 LINQ to SQL N-Tier | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9cb10eb8-957f-4beb-a271-5f682016fed2
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 搭配 Web 服務使用 LINQ to SQL N-Tier
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 是專為在鬆散結合的資料存取層 \(DAL\) 中的中介層 \(例如 Web 服務\) 上使用所設計。  如果展示層是 ASP.NET 網頁，那麼您可以使用 <xref:System.Web.UI.WebControls.LinqDataSource> Web 伺服器控制項，管理使用者介面與中介層上的 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 之間的資料傳輸。  如果展示層不是 ASP.NET 網頁，則中介層和展示層都必須額外執行一些工作，以管理資料的序列化 \(Serialization\) 和還原序列化 \(Deserialization\)。  
  
## 設定中介層上的 LINQ to SQL  
 在 Web 服務或 N\-Tier 應用程式中，中介層包含資料內容和實體類別。  您可以手動建立這些類別，或者使用 SQLMetal.exe 或[!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)]建立類別 \(如文件他處所述\)。  在設計階段，您可以選擇是否要將實體類別設為可序列化。  如需詳細資訊，請參閱[HOW TO：如何將實體設為可序列化](../../../../../../docs/framework/data/adonet/sql/linq/how-to-make-entities-serializable.md)。  另一個選擇是另外建立一組類別來封裝要序列化的資料，然後當您在 [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] 查詢中傳回資料時，投影到這些可序列化的型別中。  
  
 您接著可以定義介面以及用戶端將呼叫來擷取、插入和更新資料的方法。  這些介面方法會包裝您的 [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] 查詢。  您可以使用任何一種序列化機制來處理遠端方法呼叫和序列化資料。  唯一的要求是，如果物件模型中存在循環或雙向關係，例如標準 Northwind 物件模型中的 Customers 與 Orders 之間的關係，那麼就必須使用支援此關係的序列化程式。  Windows Communication Foundation \(WCF\) <xref:System.Runtime.Serialization.DataContractSerializer> 支援雙向關聯性，但用於非 WCF Web 服務的 XmlSerializer 則否。如果您選擇使用 XmlSerializer，就必須確定物件模型沒有循環關聯性。  
  
 如需 Windows Communication Foundation 的詳細資訊，請參閱 [Windows Communication Foundation Services and WCF Data Services in Visual Studio](../Topic/Windows%20Communication%20Foundation%20Services%20and%20WCF%20Data%20Services%20in%20Visual%20Studio.md)。  
  
 在 <xref:System.Data.Linq.DataContext> 和實體類別上使用部分類別和方法連結 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 執行階段事件，以實作商務規則 \(Business Rule\) 或定義域特定邏輯。  如需詳細資訊，請參閱[實作 N\-Tier 商務邏輯](../../../../../../docs/framework/data/adonet/sql/linq/implementing-business-logic-linq-to-sql.md)。  
  
## 定義可序列化的型別  
 用戶端或展示層必須有將從中介層接收之類別的型別定義。  這些型別可以是實體類別本身，也可以是特殊類別，其中只包裝實體類別中用以遠端處理的特定欄位。  無論如何，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 一概不管展示層以何種方式取得這些型別定義。  例如，展示層可以使用 WCF 自動產生型別，或可以在 DLL 複本中定義這些型別，甚或是可以定義自己的型別版本。  
  
## 擷取和插入資料  
 中介層會定義介面，而此介面會指定展示層要如何存取資料。  例如 `GetProductByID(int productID)` 或 `GetCustomers()`。  在中介層上，方法主體通常會建立新的 <xref:System.Data.Linq.DataContext> 執行個體，然後對它的一個或多個資料表執行查詢。  中介層接著會以 <xref:System.Collections.Generic.IEnumerable%601> 傳回結果，其中 `T` 是實體類別或其他用來序列化的型別。  展示層絕不會直接傳送查詢變數給中介層，或直接從中介層接收查詢變數。  這兩層會交換值、物件和具體資料集合。  在收到集合之後，如有需要，展示層就可使用 [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] to Objects 來查詢它。  
  
 插入資料時，展示層可建構新物件並將它傳送到中介層，或可以讓中介層根據其所提供的值建構物件。  一般來說，在 N\-Tier 應用程式中擷取和插入資料，與在 2 層應用程式中的程序沒有太大差異。  如需詳細資訊，請參閱[查詢資料庫](../../../../../../docs/framework/data/adonet/sql/linq/querying-the-database.md)與[進行和提交資料變更](../../../../../../docs/framework/data/adonet/sql/linq/making-and-submitting-data-changes.md)。  
  
## 追蹤變更以更新和刪除  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 支援以時間戳記為基礎的開放式並行存取 \(Optimistic Concurrency\) \(也稱為 RowVersions\) 和以原始值為基礎的開放式並行存取。  如果資料庫資料表有時間戳記，則更新和刪除無論在中介層或展示層都不需要額外工作。  不過，如果必須使用原始值來進行開放式並行存取檢查，那麼展示層就必須負責追蹤這些值，並在更新時送回這些值。  這是因為對展示層上的實體所做的變更並不會在中介層上追蹤。  事實上，原始擷取實體的動作與最後更新它的動作，通常是由兩個完全不同的 <xref:System.Data.Linq.DataContext> 執行個體所執行。  
  
 展示層所做的變更愈多，追蹤這些變更並封裝送回中介層的工作就愈複雜。  溝通變更的機制如何實作，端視應用程式而定。  唯一的要求是，開放式並行存取檢查所需的這些原始值必須提供給 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]。  
  
 如需詳細資訊，請參閱[N\-Tier 應用程式中的資料擷取和 CUD 作業 \(LINQ to SQL\)](../../../../../../docs/framework/data/adonet/sql/linq/data-retrieval-and-cud-operations-in-n-tier-applications.md)。  
  
## 請參閱  
 [使用 LINQ to SQL 的 N\-Tier 和遠端應用程式](../../../../../../docs/framework/data/adonet/sql/linq/n-tier-and-remote-applications-with-linq-to-sql.md)   
 [NIB: LinqDataSource Web Server Control Overview](http://msdn.microsoft.com/zh-tw/104cfc3f-7385-47d3-8a51-830dfa791136)