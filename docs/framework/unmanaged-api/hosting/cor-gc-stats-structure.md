---
title: COR_GC_STATS 構造体
ms.date: 03/30/2017
api_name:
- COR_GC_STATS
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- COR_GC_STATS
helpviewer_keywords:
- COR_GC_STATS structure [.NET Framework hosting]
ms.assetid: 8d4ff73e-739b-40f6-9349-359fbc99c2f9
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1085bec812d797d3fbe4ea63ef447d4c466149f2
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69965056"
---
# <a name="cor_gc_stats-structure"></a>COR_GC_STATS 構造体
共通言語ランタイム (CLR) のガベージコレクション機構に関する統計情報を提供します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef struct _COR_GC_STATS {  
    ULONG   Flags;   
    SIZE_T  ExplicitGCCount;  
    SIZE_T  GenCollectionsTaken[3];  
    SIZE_T  CommittedKBytes;   
    SIZE_T  ReservedKBytes;  
    SIZE_T  Gen0HeapSizeKBytes;  
    SIZE_T  Gen1HeapSizeKBytes;  
    SIZE_T  Gen2HeapSizeKBytes;  
    SIZE_T  LargeObjectHeapSizeKBytes;  
    SIZE_T  KBytesPromotedFromGen0;  
    SIZE_T  KBytesPromotedFromGen1;  
} COR_GC_STATS;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`Flags`|計算および返されるフィールド値を示します。|  
|`ExplicitGCCount`|外部要求によって強制されたガベージコレクションの数を示します。|  
|`GenCollectionsTaken`|生成のたびに実行されるガベージコレクションの数を示します。|  
|`CommittedKBytes`|すべてのヒープでコミットされた合計キロバイト数。|  
|`ReservedKBytes`|すべてのヒープに予約されているキロバイト数の合計です。|  
|`Gen0HeapSizeKBytes`|ジェネレーションゼロヒープのサイズ (kb 単位)。|  
|`Gen1HeapSizeKBytes`|ジェネレーション1のヒープのサイズ (kb 単位)。|  
|`Gen2HeapSizeKBytes`|ジェネレーション2のヒープのサイズ (kb 単位)。|  
|`LargeObjectHeapSizeKBytes`|ラージオブジェクトヒープのサイズ (kb 単位)。|  
|`KBytesPromotedFromGen0`|ジェネレーション0からジェネレーション1に昇格されたオブジェクトのサイズ (kb 単位)。|  
|`KBytesPromotedFromGen1`|ジェネレーション1からジェネレーション2に昇格されたオブジェクトのサイズ (kb 単位)。|  
  
## <a name="remarks"></a>Remarks  
 [ICLRGCManager:: getstats](../../../../docs/framework/unmanaged-api/hosting/iclrgcmanager-getstats-method.md)メソッドでは、 `Flags`設定する統計を指定するために、 `COR_GC_STATS`構造体のフィールドを[COR_GC_STAT_TYPES](../../../../docs/framework/unmanaged-api/hosting/cor-gc-stat-types-enumeration.md)列挙の1つ以上の値に設定する必要があります。  
  
 次の表は、この構造体によって提供される統計を、 `COR_GC_COUNTS`と`COR_GC_MEMORYUSAGE`の2つの [COR_GC_STAT_TYPES](../../../../docs/framework/unmanaged-api/hosting/cor-gc-stat-types-enumeration.md) 列挙値にマップします。  
  
|指定された COR_GC_COUNTS|指定された COR_GC_MEMORYUSAGE|  
|----------------------------------|---------------------------------------|  
|`ExplicitGCCount`<br /><br /> `GenCollectionsTaken`|`CommittedKBytes`<br /><br /> `ReservedKBytes`<br /><br /> `Gen0HeapSizeKBytes`<br /><br /> `Gen1HeapSizeKBytes`<br /><br /> `Gen2HeapSizeKBytes`<br /><br /> `LargeObjectHeapSizeKBytes`<br /><br /> `KBytesPromotedFromGen0`<br /><br /> `KBytesPromotedFromGen1`|  
  
 使用例を次に示します。  
  
```cpp  
COR_GC_STATS GCStats;  
GCStats.Flags = COR_GC_COUNTS | COR_GC_MEMORYUSAGE;  
pCLRGCManager->GetStats(&GCStats);  
```  
  
## <a name="requirements"></a>必要条件  
 **・** [システム要件](../../../../docs/framework/get-started/system-requirements.md)に関するページを参照してください。  
  
 **ヘッダー:** GCHost  
  
 **ライブラリ**Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ホスト構造体](../../../../docs/framework/unmanaged-api/hosting/hosting-structures.md)
- [自動メモリ管理](../../../standard/automatic-memory-management.md)
- [ガベージ コレクション](../../../standard/garbage-collection/index.md)
