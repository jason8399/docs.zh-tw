---
title: "&lt;新增&gt;元素&lt;接聽程式&gt;如&lt;來源&gt;"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sources/source/listeners/add
helpviewer_keywords:
- initializeData attribute
- add element for <listeners> for <source>
- <add> element for <listeners> for <source>
ms.assetid: 4ce36ac1-81ef-48e8-b8b2-b5a5b0e2adcb
caps.latest.revision: 
author: mcleblanc
ms.author: markl
manager: markl
ms.workload:
- dotnet
ms.openlocfilehash: 86177010d8ed70302b51ec9c416a3295009e7394
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/22/2017
---
# <a name="ltaddgt-element-for-ltlistenersgt-for-ltsourcegt"></a>&lt;新增&gt;元素&lt;接聽程式&gt;如&lt;來源&gt;
將接聽項新增至追蹤來源的 `Listeners` 集合。  
  
 \<configuration>  
\<system.diagnostics >  
\<來源 >  
\<來源 >  
\<接聽項 >  
\<add>  
  
## <a name="syntax"></a>語法  
  
```xml  
<add name="name"   
  type="TraceListenerClassName, Version, Culture, PublicKeyToken"  
  initializeData="data"/>  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子項目和父項目。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|`type`|必要屬性，除非您正在參考中的接聽程式`sharedListeners`集合中的情況下，您只需要依名稱參考它 (請參閱[範例](#example))。<br /><br /> 指定接聽程式的類型。 您必須使用符合在指定之需求的字串[指定限定的型別名稱](../../../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md)。|  
|`initializeData`|選擇性屬性。<br /><br /> 指定的類別傳遞至建構函式的字串。 A<xref:System.Configuration.ConfigurationException>如果類別沒有可接受 string 建構函式會擲回。|  
|`name`|選擇性屬性。<br /><br /> 指定的接聽程式名稱。|  
|`traceOutputOptions`|選擇性屬性。<br /><br /> 指定<xref:System.Diagnostics.TraceListener.TraceOutputOptions%2A>追蹤接聽程式的屬性值。|  
|[自訂屬性]|選擇性屬性。<br /><br /> 指定的值所識別的接聽程式的特定屬性<xref:System.Diagnostics.TraceListener.GetSupportedAttributes%2A>該接聽項的方法。 <xref:System.Diagnostics.DelimitedListTraceListener.Delimiter%2A>是唯一的額外屬性範例<xref:System.Diagnostics.DelimitedListTraceListener>類別。|  
  
### <a name="child-elements"></a>子元素  
  
|項目|描述|  
|-------------|-----------------|  
|[\<filter>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/filter-element-for-add-for-listeners-for-source.md)|將篩選新增至追蹤來源之 `Listeners` 集合中的接聽項。|  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|`configuration`|通用語言執行平台和 .NET Framework 應用程式所使用之每個組態檔中的根項目。|  
|`system.diagnostics`|指定用於收集、儲存及路由傳送訊息的追蹤接聽項，以及設定追蹤參數的層級。|  
|`sources`|包含起始追蹤訊息的追蹤來源。|  
|`source`|指定起始追蹤訊息的追蹤來源。|  
|`listeners`|指定接聽程式以收集、 儲存和路由傳送訊息。|  
  
## <a name="remarks"></a>備註  
 .NET Framework 所隨附的接聽程式類別衍生自<xref:System.Diagnostics.TraceListener>類別。  
  
 如果您未指定`name`屬性的追蹤接聽項，<xref:System.Diagnostics.TraceListener.Name%2A>追蹤接聽項的屬性會預設為空字串 ("")。 如果您的應用程式只能有一個接聽程式，而不指定名稱，可以將它加入，您可以藉由指定名稱為空字串中移除。 不過，如果您的應用程式有多個接聽程式，您應該指定每個追蹤接聽程式，可讓您識別及管理中的個別追蹤接聽項的唯一名稱<xref:System.Diagnostics.TraceSource.Listeners%2A?displayProperty=nameWithType>集合。  
  
> [!NOTE]
>  加入一個以上的追蹤接聽程式相同的型別且具有相同名稱只能有一個追蹤接聽項中的該類型的結果和名稱新增至`Listeners`集合。 不過，您可以程式設計方式加入至多個相同的接聽程式`Listeners`集合。  
  
 值`initializeData`屬性取決於您所建立的接聽程式的類型。 並非所有的追蹤接聽程式會要求您指定`initializeData`。  
  
> [!NOTE]
>  當您使用`initializeData`屬性，可能會遇到的編譯器警告"未宣告 'initializeData' 屬性。 」 發生這個警告是因為組態設定會根據抽象基底類別來驗證<xref:System.Diagnostics.TraceListener>，其無法辨識`initializeData`屬性。 一般而言，您可以忽略此警告具有參數的建構函式的追蹤接聽程式實作。  
  
 下表顯示隨附於.NET Framework 追蹤接聽項，並描述的值及其`initializeData`屬性。  
  
|追蹤接聽程式類別|initializeData 屬性值|  
|--------------------------|------------------------------------|  
|<xref:System.Diagnostics.ConsoleTraceListener?displayProperty=nameWithType>|`useErrorStream`值<xref:System.Diagnostics.ConsoleTraceListener.%23ctor%2A>建構函式。  設定`initializeData`屬性設定為"`true`"來寫入追蹤和偵錯輸出到標準錯誤資料流中，將它設定為"`false`"寫入標準輸出資料流。|  
|<xref:System.Diagnostics.DelimitedListTraceListener?displayProperty=nameWithType>|檔案的名稱<xref:System.Diagnostics.DelimitedListTraceListener>寫入。|  
|<xref:System.Diagnostics.EventLogTraceListener?displayProperty=nameWithType>|現有的事件記錄檔來源的名稱。|  
|<xref:System.Diagnostics.EventSchemaTraceListener?displayProperty=nameWithType>|檔案的名稱，<xref:System.Diagnostics.EventSchemaTraceListener>寫入。|  
|<xref:System.Diagnostics.TextWriterTraceListener?displayProperty=nameWithType>|檔案的名稱，<xref:System.Diagnostics.TextWriterTraceListener>寫入。|  
|<xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=nameWithType>|檔案的名稱，<xref:System.Diagnostics.XmlWriterTraceListener>寫入。|  
  
## <a name="configuration-file"></a>組態檔  
 此項目可以用於電腦組態檔 (Machine.config) 和應用程式組態檔。  
  
## <a name="example"></a>範例  
 下列範例示範如何使用`<add>`項目將接聽項`console`和`textListener`至`Listeners`追蹤來源的集合`TraceSourceApp`。 `textListener`接聽程式會將追蹤輸出寫入檔案 myListener.log。  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="TraceSourceApp" switchName="sourceSwitch"   
        switchType="System.Diagnostics.SourceSwitch">  
        <listeners>  
          <add name="console"   
            type="System.Diagnostics.ConsoleTraceListener"/>  
          <add name="textListener"/>  
          <remove name="Default"/>  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add name="textListener"   
        type="System.Diagnostics.TextWriterTraceListener"   
        initializeData="myListener.log"/>  
    </sharedListeners>  
    <switches>  
      <add name="sourceSwitch" value="Warning"/>  
    </switches>  
  </system.diagnostics>  
</configuration>   
```  
  
## <a name="see-also"></a>請參閱  
 <xref:System.Diagnostics.TraceSource>  
 <xref:System.Diagnostics.TraceListener>  
 [追蹤和偵錯設定結構描述](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)  
 [追蹤接聽項](../../../../../docs/framework/debug-trace-profile/trace-listeners.md)
