---
title: "如何：從檔案讀取文字"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- streams, reading text from files
- reading text files
- reading data, text files
- data streams, reading text from files
- I/O [.NET Framework], reading text from files
ms.assetid: ed180baa-dfc6-4c69-a725-46e87edafb27
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 6fbf9c910847986af1c02b5848c81266009e2e07
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="how-to-read-text-from-a-file"></a>如何：從檔案讀取文字
下列範例將示範如何以同步和非同步方式，從使用適用於桌面應用程式的 .NET 之文字檔讀取文字。 在這兩個範例中，當您建立 <xref:System.IO.StreamReader> 類別的執行個體時，會提供檔案的相對路徑或絕對路徑。 下列範例會假設名為 TestFile.txt 的檔案與應用程式位於相同資料夾中。  
  
 由於 Windows 執行階段提供不同的資料流類型來讀取和寫入檔案，因此這些程式碼不適用於 Windows 市集應用程式的開發工作。 如需示範如何在 Windows 市集應用程式的內容中從檔案讀取文字的範例，請參閱[快速入門：讀取和寫入檔案](http://msdn.microsoft.com/library/windows/apps/hh758325.aspx)。 如需如何在 .NET Framework 資料流和 Windows 執行階段資料流之間轉換的範例，請參閱[操作說明：在 .NET Framework 資料流與 Windows 執行階段資料流之間轉換](../../../docs/standard/io/how-to-convert-between-dotnet-streams-and-winrt-streams.md)。  
  
## <a name="example"></a>範例  
 第一個範例將示範在主控台應用程式內的同步讀取作業。 在這個範例中，會使用資料流讀取器開啟文字檔案，內容會複製到字串，而字串會輸出到主控台。  
  
 [!code-csharp[Conceptual.BasicIO.TextFiles#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/source3.cs#3)]
 [!code-vb[Conceptual.BasicIO.TextFiles#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/source3.vb#3)]  
  
## <a name="example"></a>範例  
 第二個範例將示範 Windows Presentation Foundation (WPF) 應用程式內的非同步讀取作業。  
  
 [!code-csharp[Conceptual.BasicIO.TextFiles#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/source6.cs#6)]
 [!code-vb[Conceptual.BasicIO.TextFiles#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/source6.vb#6)]  
  
## <a name="see-also"></a>請參閱  
 <xref:System.IO.StreamReader>  
 <xref:System.IO.File.OpenText%2A?displayProperty=nameWithType>  
 <xref:System.IO.StreamReader.ReadLine%2A?displayProperty=nameWithType>  
 [非同步檔案 I/O](../../../docs/standard/io/asynchronous-file-i-o.md)  
 [NIB：操作說明：建立目錄清單](http://msdn.microsoft.com/library/4d2772b1-b991-4532-a8a6-6ef733277e69)  
 [快速入門：讀取和寫入檔案](http://msdn.microsoft.com/library/windows/apps/hh758325.aspx)  
 [操作說明：在 .NET Framework 資料流與 Windows 執行階段資料流之間轉換](../../../docs/standard/io/how-to-convert-between-dotnet-streams-and-winrt-streams.md)  
 [如何：讀取和寫入新建立的資料檔案](../../../docs/standard/io/how-to-read-and-write-to-a-newly-created-data-file.md)  
 [操作說明：開啟並附加至記錄檔](../../../docs/standard/io/how-to-open-and-append-to-a-log-file.md)  
 [如何：將文字寫入檔案](../../../docs/standard/io/how-to-write-text-to-a-file.md)  
 [如何：從字串中讀取字元](../../../docs/standard/io/how-to-read-characters-from-a-string.md)  
 [如何：將字元寫入至字串](../../../docs/standard/io/how-to-write-characters-to-a-string.md)  
 [檔案和資料流 I-O](../../../docs/standard/io/index.md)
