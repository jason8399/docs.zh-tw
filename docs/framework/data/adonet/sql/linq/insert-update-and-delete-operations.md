---
title: "插入、更新和刪除作業 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 26a43a4f-83c9-4732-806d-bb23aad0ff6b
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 插入、更新和刪除作業
您可以加入、變更和移除物件模型 \(Object Model\) 中的物件，以便在 `Insert` 中執行 `Update`、`Delete` 和 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 作業。  根據預設，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 會將您的動作轉譯成 SQL 並將變更提交至資料庫。  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 提供相當大的彈性來操作和保存您對物件所做的變更。  一旦取得實體物件 \(透過查詢加以擷取或重新加以建構\)，您就可以將它們變更為應用程式中的典型物件。  也就是說，您可以變更這些實體物件的值，將它們加入至集合中，以及從集合中加以移除。  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 會追蹤這些變更，而且在您呼叫 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 時準備好將變更傳送回資料庫。  
  
> [!NOTE]
>  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 不支援或辨識串聯 \(Cascade\) 刪除作業。  如果您要刪除有限制式之資料表中的資料列，必須在資料庫的外部索引鍵限制式中設定 `ON DELETE CASCADE` 規則，或者使用您自己的程式碼，先刪除使父物件無法刪除的子物件。否則，會擲回例外狀況。  如需詳細資訊，請參閱[HOW TO：從資料庫刪除資料列](../../../../../../docs/framework/data/adonet/sql/linq/how-to-delete-rows-from-the-database.md)。  
  
 下列摘錄會使用 Northwind 範例資料庫中的 `Customer` 和 `Order` 類別。  為了簡單起見，並不會顯示類別定義。  
  
 [!code-csharp[DLinqCRUDOps#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCRUDOps/cs/Program.cs#1)]
 [!code-vb[DLinqCRUDOps#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCRUDOps/vb/Module1.vb#1)]  
  
 當您呼叫 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 時，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 會自動產生及執行必要的 SQL 命令，以便將變更傳送回資料庫。  
  
> [!NOTE]
>  您通常可以透過預存程序 \(Stored Procedure\)，使用自訂邏輯來覆寫這個行為。  如需詳細資訊，請參閱[開發人員覆寫預設行為的責任](../../../../../../docs/framework/data/adonet/sql/linq/responsibilities-of-the-developer-in-overriding-default-behavior.md)。  
>   
>  使用 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] 的開發人員可以使用 [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] 來開發預存程序，以達到此目的。  
  
## 請參閱  
 [下載範例資料庫](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)   
 [自訂插入、更新和刪除作業](../../../../../../docs/framework/data/adonet/sql/linq/customizing-insert-update-and-delete-operations.md)