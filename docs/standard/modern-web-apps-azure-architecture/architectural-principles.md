---
title: "架構原則"
description: "使用 ASP.NET Core 和 Azure 的現代化 Web 應用程式架構設計人員 |架構原則"
author: ardalis
ms.author: wiwagn
ms.date: 10/06/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: bdb215d64253fb7d22ae2c5648030336850006b5
ms.sourcegitcommit: f28752eab00d2bd97e971542c0f49ce63cfbc239
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/29/2018
---
# <a name="architectural-principles"></a>架構原則

> 「如果建築工人像工程師寫軟體那樣蓋房子，那第一隻飛來的啄木鳥就能毀掉人類文明。」  
> _\- Gerald Weinberg_

## <a name="summary"></a>總結

您應該架構設計人員和設計軟體解決方案與可維護性記住。 本章節中所述的原則可協助引導您向將產生的全新、 可維護應用程式的架構決策。 一般而言，這些原則會引導您向建置出不同的元件未緊密結合的應用程式其他部分，但而不是透過明確的介面進行通訊的應用程式] 或 [郵件系統。

## <a name="common-design-principles"></a>常見的設計原則

### <a name="separation-of-concerns"></a>重要性分離

開發時的指導原則是**分離的考量**。 這個原則判斷提示的軟體，則應以根據它所執行的工作種類。 比方說，假設應用程式中包含邏輯來識別值得注意的項目可以顯示給使用者，而且其中格式化此類項目，使其更值得注意的特定方式。 選擇要格式化的項目應該有所區隔負責格式項目，因為這些個別考量只正巧彼此相關的行為的責任的行為。

在架構上，您可以以邏輯方式分隔從基礎結構和使用者介面邏輯核心商務行為遵循這個原則建立應用程式。 在理想情況下，商務規則和邏輯應該位於個別的專案，不應依賴其他應用程式中的專案。 這有助於確保商務模型很容易測試並沒有緊密結合低層級的實作詳細資料就能持續改進。 重要性分離是使用應用程式架構中的圖層的索引鍵的考量。

### <a name="encapsulation"></a>封裝

應用程式的不同部分應該使用**封裝**它們的應用程式其他部分隔離。 應用程式元件和層級應該能夠調整的內部實作，而不會中斷其共同作業者，只要不違反外部的合約。 正確使用的封裝 （encapsulation） 可協助達到鬆散偶合和應用程式設計中的模組化，因為物件與封裝可以取代為替代的實作，只要維持相同的介面。

在類別中，封裝達成外部類別的內部狀態的存取限制。 如果外部執行者想要管理物件的狀態，則應如此做透過妥善定義的函式 （或屬性 setter），而不是直接存取物件的私用狀態。 同樣地，應用程式元件和應用程式本身應該公開妥善定義的介面，它們共同作業者來使用，而非讓它們直接進行修改的狀態。 這會釋出應用程式的內部設計隨著時間而不用，這樣做，將會中斷共同作業者，只要會維護的公用合約。

### <a name="dependency-inversion"></a>相依性反向

在應用程式內的相依性的方向應該是抽象，不實作詳細資料的方向。 大部分的應用程式會寫入使執行階段執行的方向流程編譯時間相依性。 這會產生直接相依性圖形。 也就是說，如果模組 A 呼叫 B，模組中的函式呼叫的函式在模組中 C，則在編譯時間的取決於所示圖 4-1，會隨著 C、 B。

![](./media/image4-1.png)

**圖 4-1.** 直接的相依性圖形。

套用相依性反向原則允許 A 呼叫 B，讓其能夠 a 呼叫 B，在執行階段，會實作抽象方法但 b 相依於介面由控制的編譯時期 (因此，*反轉*一般編譯時間相依性）。 在執行階段，控制程式執行流程維持不變，但是介面簡介表示不同的實作這些介面可以輕鬆地裝載。

![](./media/image4-2.png)

**圖 4-2。** 反向的相依性圖形。

**相依性反向**是建置鬆散偶合的應用程式，因為實作詳細資料可以寫入而定，實作較高的層級抽象概念，而不是利用其他方式的重要部分。 產生的應用程式會因此是可測試、 模組化，和可維護性。 一種作法*相依性插入*即可進行反轉遵循相依性。

### <a name="explicit-dependencies"></a>明確的相依性

**方法和類別應該明確需要共同作業正常運作所需的任何物件。** 類別建構函式會提供一個機會，以識別它們需要為了處於有效狀態，並正常運作的項目類別。 如果您定義的類別，可以建構和呼叫，但其中只有正常運作特定的全域或基礎結構元件已就緒時，這些類別正在*誠實*其用戶端。 建構函式合約告訴它只需要的項目指定 （可能是沒有任何類別只會使用預設建構函式），但接著在結果物件的執行階段的用戶端真的需要其他項目。

遵循明確的相依性原則，您的類別和方法正在誠實與他們的用戶端需它們需要才能運作。 這樣多個可以自我記錄您的程式碼和程式碼合約更加易懂易記，因為使用者會具備信任，只要它們提供所需格式的方法或建構函式參數，他們所處理之物件的行為正確地在執行階段。

### <a name="single-responsibility"></a>單一的責任

物件導向設計，適用於單一責任原則，但也可視為類似的重要性分離架構原則。 指出物件應該只有一個責任，而且您應該有只有一個變更的原因。 具體而言，唯一物件應該變更的情況是如果必須更新它會執行其一個責任的方式。 此原則可協助產生更鬆散偶合而模組化系統，因為許多種新行為可以實作做為新的類別，而不是新增至現有類別的額外責任。 加入新類別永遠是比變更現有的類別，因為沒有程式碼更安全，但相依於新的類別。

在整合應用程式中，我們可以套用在高層級的單一責任原則至應用程式中的圖層。 簡報責任應保留在 UI 專案，資料存取時責任應保留在基礎結構專案中。 商務邏輯應該放在應用程式核心專案，它可以輕鬆地測試和可以從其他責任的獨立進行。

當此原則會套用至應用程式架構，並採取其邏輯的端點時，您會取得 microservices。 給定的微服務應該有單一的責任。 如果您需要擴充系統的行為，它通常會比較好這樣做，藉由新增其他 microservices，而不是新增至現有的責任。

[深入了解 microservices 架構](http://aka.ms/MicroservicesEbook)

### <a name="dont-repeat-yourself-dry"></a>不要重複自行 （乾）

應用程式應避免指定相關的多個位置的特定概念，因為這是常見的錯誤來源的行為。 在某個時間點，在需求變更將需要變更此行為與可能性行為至少一個執行個體將會更新失敗會導致系統的不一致的行為。

而不是複製邏輯，請將它封裝在程式設計建構。 將此建構此行為，透過單一的授權單位，而且有應用程式需要這個行為使用新建構的任何其他部分。

> [!NOTE]
> 避免繫結在一起才正巧重複的行為。 例如，只是兩個不同的常數這兩個具有相同的值，因為這不表示您應該只有一個常數，如果在概念上所指不同的項目。

### <a name="persistence-ignorance"></a>永續性無知之

**永續性無知之**(PI) 指的是類型，需要保存，但是其程式碼不會受到持續性技術的選項。 這種型別在.NET 中的有時稱為純舊 CLR 物件 (POCOs)，因為它們不需要特定的基底類別繼承或實作特定介面。 永續性無知之是有用的因為它可讓保存在多個方面，提供額外的彈性，應用程式的相同商務模型。 持續性選項可能會隨著時間變更，到另一個資料庫技術或其他形式的持續性系統可能會要求除了與啟動任何應用程式 (例如，使用 Redis 快取或 Azure DocumentDb 除了關聯式資料庫）。

違反這個原則的一些範例包括：

-   必要的基底類別

-   所需的介面實作

-   類別負責儲存本身 （例如使用中的記錄模式）

-   必要的預設建構函式

-   需要 virtual 關鍵字的屬性

-   特定的持續性所需的屬性

類別有任何上述功能或行為的需求加入要保存的類型和持續性技術，使其更難以將來採用新的資料存取策略的選項之間的結合。

### <a name="bounded-contexts"></a>已繫結的內容

**繫結內容**是中央 Domain-Driven 設計模式。 它們分成不同的概念模組提供一種處理大型應用程式或組織的複雜度。 每個概念模組則表示可分開其他內容的內容 （因此，界限），並可以獨立進行。 每個繫結的內容應在理想情況下自由選擇自己的概念，名稱，而且應該具有獨佔存取權它自己的持續性存放區。

最少個別 web 應用程式應該致力於自己已繫結的內容中，使用自己的持續性存放區，其商務模型，而不是與其他應用程式共用一個資料庫。 透過程式設計介面，而不是透過共用的資料庫，可讓商務邏輯，就會發生繫結的內容之間的通訊，事件才會將回應進行的變更。 與 historyinsert-spg 內容地圖密切 microservices，也理想的情況下實作為自己的個別繫結內容。

> ### <a name="references--modern-web-applications"></a>參考 – 現代化 Web 應用程式
> - 重要性分離  
> <http://deviq.com/separation-of-concerns/>
> - **Encapsulation** <http://deviq.com/encapsulation/>
> - **相依性反向原則**  
> <http://deviq.com/dependency-inversion-principle/>
> - **明確相依性準則**  
> <http://deviq.com/explicit-dependencies-principle/>
> - **不要重複自行**  
> <http://deviq.com/don-t-repeat-yourself/>
> - 永續性無知之  
> <http://deviq.com/persistence-ignorance/>
> - **已繫結的內容**  
> <https://martinfowler.com/bliki/BoundedContext.html>

> [!div class="step-by-step"]
[上一個](choose-between-traditional-web-and-single-page-apps.md) [下一步] (常見的 web 層應用程式-architectures.md)
