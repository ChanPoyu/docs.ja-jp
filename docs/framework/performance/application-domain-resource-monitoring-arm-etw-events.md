---
title: アプリケーション ドメインのリソース監視 (ARM) ETW イベント
ms.date: 03/30/2017
helpviewer_keywords:
- ETW, application domain monitoring events
- application domain monitoring events [.NET Framework]
ms.assetid: d38ff268-a2ee-434e-b504-d570880e0289
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f0e4002ae248022a9e4380c79174109494b5e4ca
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046769"
---
# <a name="application-domain-resource-monitoring-arm-etw-events"></a>アプリケーション ドメインのリソース監視 (ARM) ETW イベント
<a name="top"></a> これらのイベントは、アプリケーション ドメインの状態に関する詳細な診断の情報を提供します。 これらのイベントを使用することもできますが、アプリケーション ドメインのリソース監視 (ARM) の機能を使用しても同じ情報を得られます。  
  
 このカテゴリは、次のイベントで構成されます。  
  
- [ThreadCreated イベント](#threadcreated_event)  
  
- [AppDomainMemAllocated イベント](#appdomainmemallocated_event)  
  
- [AppDomainMemSurvived イベント](#appdomainmemsurvived_event)  
  
- [ThreadAppDomainEnter イベント](#threadappdomainenter_event)  
  
- [ThreadTerminated イベント](#threadterminated_event)  
  
<a name="threadcreated_event"></a>   
## <a name="threadcreated-event"></a>ThreadCreated イベント  
 このイベントは、ランダウン プロバイダーで `ThreadDC` としても発生します  ( `AppDomainResourceManagementRundownKeyword` キーワードで発生)。 これは、このカテゴリでランダウン プロバイダーで発生する唯一のイベントです。  
  
 次の表に、キーワードとレベルを示します。 (詳細については、「 [CLR ETW Keywords and Levels](clr-etw-keywords-and-levels.md)」を参照してください)。  
  
|イベントを発生させるキーワード|レベル|  
|-----------------------------------|-----------|  
|`AppDomainResourceManagementKeyword` (0x800)|情報通知 (4)|  
|`ThreadingKeyword` (0x10000)|情報通知 (4)|  
  
 次の表に、イベント情報を示します。  
  
|イベント|イベント ID|いつ発生するか|  
|-----------|--------------|-----------------|  
|`ThreadCreated`|85|アプリケーション ドメインに対してスレッドが作成された。|  
  
 次の表に、イベント データを示します。  
  
|フィールド名|データ型|説明|  
|----------------|---------------|-----------------|  
|ThreadID|win:UInt64|作成されたスレッドの ID。|  
|AppDomainID|win:UInt64|スレッドのアクティビティの報告対象のアプリケーション ドメインの識別子。|  
|フラグ|win:UInt32|スレッドの作成フラグ|  
|ManagedThreadIndex|win:UInt32|作成されたスレッドのマネージド インデックス。|  
|OSThreadID|win:UInt32|作成されたスレッドのオペレーティング システム ID。|  
|ClrInstanceID|win:UInt16|CLR または CoreCLR のインスタンスの一意の ID。|  
  
 [ページのトップへ](#top)  
  
<a name="appdomainmemallocated_event"></a>   
## <a name="appdomainmemallocated-event"></a>AppDomainMemAllocated イベント  
 次の表に、キーワードとレベルを示します。  
  
|イベントを発生させるキーワード|レベル|  
|-----------------------------------|-----------|  
|`AppDomainResourceManagementKeyword` (0x800)|情報通知 (4)|  
  
 次の表に、イベント情報を示します。  
  
|イベント|イベント ID|いつ発生するか|  
|-----------|--------------|-----------------|  
|`AppDomainMemAllocated`|83|アプリケーション ドメインに 4 MB ずつのメモリ (概算) が割り当てられる。|  
  
 次の表に、イベント データを示します。  
  
|フィールド名|データ型|説明|  
|----------------|---------------|-----------------|  
|AppDomainID|win:UInt64|リソースの使用状況の報告対象のアプリケーション ドメインの識別子。|  
|Allocated|win:UInt64|アプリケーション ドメインが作成されてから、このアプリケーション ドメインに割り当てられたバイトの合計数 (解放されたメモリの量は引かれない)。|  
|ClrInstanceID|win:UInt16|CLR または CoreCLR のインスタンスの一意の ID。|  
  
 [ページのトップへ](#top)  
  
<a name="appdomainmemsurvived_event"></a>   
## <a name="appdomainmemsurvived-event"></a>AppDomainMemSurvived イベント  
 次の表に、キーワードとレベルを示します。  
  
|イベントを発生させるキーワード|レベル|  
|-----------------------------------|-----------|  
|`AppDomainResourceManagementKeyword` (0x800)|情報通知 (4)|  
  
 次の表に、イベント情報を示します。  
  
|イベント|イベント ID|いつ発生するか|  
|-----------|--------------|-----------------|  
|`AppDomainMemSurvived`|84|各ガベージ コレクションが終了した。|  
  
 次の表に、イベント データを示します。  
  
|フィールド名|データ型|説明|  
|----------------|---------------|-----------------|  
|AppDomainID|win:UInt64|リソースの使用状況の報告対象のドメインの識別子。|  
|Survived|win:UInt64|最後のコレクションの実行後に残され、このアプリケーション ドメインによって保持されることが判明しているバイト数。 この数は、完全なコレクションの後では正確で完全ですが、短期コレクションの後では完全ではない可能性があります。|  
|ProcessSurvived|win:UInt64|最後のコレクション後に残った合計バイト数。 完全なコレクションの後では、この数はマネージド ヒープにライブで保持されるバイト数を表します。 短期コレクションの後では、この数は短期のジェネレーションにライブで保持されるバイト数を表します。|  
|ClrInstanceID|win:UInt16|CLR または CoreCLR のインスタンスの一意の ID。|  
  
 [ページのトップへ](#top)  
  
<a name="threadappdomainenter_event"></a>   
## <a name="threadappdomainenter-event"></a>ThreadAppDomainEnter イベント  
 次の表に、キーワードとレベルを示します。  
  
|イベントを発生させるキーワード|レベル|  
|-----------------------------------|-----------|  
|`AppDomainResourceManagementKeyword` (0x800)|情報通知 (4)|  
|`ThreadingKeyword` (0x10000)|情報通知 (4)|  
  
 次の表に、イベント情報を示します。  
  
|イベント|イベント ID|いつ発生するか|  
|-----------|--------------|-----------------|  
|`ThreadAppDomainEnter`|87|アプリケーション ドメインにスレッドが入力される。|  
  
 次の表に、イベント データを示します。  
  
|フィールド名|データ型|説明|  
|----------------|---------------|-----------------|  
|ThreadID|win:UInt64|スレッド ID です|  
|AppDomainID|win:UInt64|アプリケーション ドメインの識別子。|  
|ClrInstanceID|win:UInt16|CLR または CoreCLR のインスタンスの一意の ID。|  
  
 [ページのトップへ](#top)  
  
<a name="threadterminated_event"></a>   
## <a name="threadterminated-event"></a>ThreadTerminated イベント  
 次の表に、キーワードとレベルを示します。  
  
|イベントを発生させるキーワード|レベル|  
|-----------------------------------|-----------|  
|`AppDomainResourceManagementKeyword` (0x800)|情報通知 (4)|  
|`ThreadingKeyword` (0x10000)|情報通知 (4)|  
  
 次の表に、イベント情報を示します。  
  
|イベント|イベント ID|いつ発生するか|  
|-----------|--------------|-----------------|  
|`ThreadTerminated`|86|スレッドが終了する。|  
  
 次の表に、イベント データを示します。  
  
|フィールド名|データ型|説明|  
|----------------|---------------|-----------------|  
|ThreadID|win:UInt64|スレッド ID です|  
|AppDomainID|win:UInt64|アプリケーション ドメインの識別子。|  
|ClrInstanceID|win:UInt16|CLR または CoreCLR のインスタンスの一意の ID。|  
  
## <a name="see-also"></a>関連項目

- [CLR ETW イベント](clr-etw-events.md)
