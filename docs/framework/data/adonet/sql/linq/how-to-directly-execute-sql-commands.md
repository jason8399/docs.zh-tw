---
title: "如何：直接執行 SQL 命令"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
ms.assetid: 04671bb0-40c0-4465-86e5-77986f454661
caps.latest.revision: "2"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: 9f87572b27cfca7cc1188ab0986dadcba7bb3e29
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="how-to-directly-execute-sql-commands"></a>如何：直接執行 SQL 命令
在假設使用 <xref:System.Data.Linq.DataContext> 集合的情況下，您可以使用 <xref:System.Data.Linq.DataContext.ExecuteCommand%2A> 執行不會傳回物件的 SQL 命令。  
  
## <a name="example"></a>範例  
 下列範例會讓 SQL Server 將 UnitPrice 增加 1.00。  
  
 [!code-csharp[DLinqCommunicatingWithDatabase#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCommunicatingWithDatabase/cs/Program.cs#3)]
 [!code-vb[DLinqCommunicatingWithDatabase#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCommunicatingWithDatabase/vb/Module1.vb#3)]  
  
## <a name="see-also"></a>請參閱  
 [如何：直接執行 SQL 查詢](../../../../../../docs/framework/data/adonet/sql/linq/how-to-directly-execute-sql-queries.md)  
 [與資料庫通訊](../../../../../../docs/framework/data/adonet/sql/linq/communicating-with-the-database.md)
