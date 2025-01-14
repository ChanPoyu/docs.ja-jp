---
title: COR_GC_REFERENCE 構造体
ms.date: 03/30/2017
api_name:
- COR_GC_REFERENCE
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_GC_REFERENCE
helpviewer_keywords:
- COR_GC_REFERENCE structure [.NET Framework debugging]
ms.assetid: 162e8179-0cd4-4110-8f06-5f387698bd62
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cc0b67621f77c0741e0b63b84ab1794530d6280b
ms.sourcegitcommit: 3caa92cb97e9f6c31f21769c7a3f7c4304024b39
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2019
ms.locfileid: "71274222"
---
# <a name="cor_gc_reference-structure"></a>COR_GC_REFERENCE 構造体
ガベージ コレクトされるオブジェクトに関する情報が含まれます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef struct _COR_GC_REFERENCE {  
    ICorDebugAppDomain *domain;   
    ICorDebugValue *location;  
    CorGCReferenceType type;  
    UINT64 extraData;  
} COR_GC_REFERENCE;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`domain`|ハンドルまたはオブジェクトが属するアプリケーションドメインへのポインター。 この値は`null`、の場合もあります。|  
|`location`|ガベージコレクションされるオブジェクトに対応する ICorDebugValue またはの値のインターフェイス。|  
|`type`|ルートの取得元を示す[Corgcreの Encetype](corgcreferencetype-enumeration.md)列挙値。 詳細については、「解説」を参照してください。|  
|`extraData`|ガベージコレクションされるオブジェクトに関する追加データ。 この情報は`type` 、フィールドに示されているように、オブジェクトのソースによって異なります。 詳細については、「解説」を参照してください。|  
  
## <a name="remarks"></a>コメント  
 フィールドは、参照の取得元を示す[corgcreの型](corgcreferencetype-enumeration.md)の列挙値です。 `type` 特定`COR_GC_REFERENCE`の値には、次のいずれかの種類のマネージオブジェクトを反映できます。  
  
- すべてのマネージスタックのオブジェクト`CorGCReferenceType.CorReferenceStack`()。 これには、マネージコードのライブ参照や、共通言語ランタイムによって作成されたオブジェクトが含まれます。  
  
- ハンドルテーブルからのオブジェクト (`CorGCReferenceType.CorHandle*`)。 これには、モジュール`HNDTYPE_STRONG`内`HNDTYPE_REFCOUNT`の厳密な参照 (および) と静的変数が含まれます。  
  
- ファイナライザーキュー (`CorGCReferenceType.CorReferenceFinalizer`) からのオブジェクト。 ファイナライザーが実行されるまで、ファイナライザーはオブジェクトをキューに置いています。  
  
 フィールド`extraData`には、参照のソース (または型) に応じて追加のデータが含まれます。 指定できる値は次のとおりです。  
  
- `DependentSource`。 がの場合、このフィールドはオブジェクトであり、alive の場合、ガベージコレクト`COR_GC_REFERENCE.Location`されるオブジェクトがルートになります。 `CorGCREferenceType.CorHandleStrongDependent` `type`  
  
- `RefCount`。 `type` が`CorGCREferenceType.CorHandleStrongRefCount`の場合、このフィールドはハンドルの参照カウントです。  
  
- `Size`。 がの場合`CorGCREferenceType.CorHandleStrongSizedByref`、このフィールドはガベージコレクターによってオブジェクトのルートが計算されたオブジェクトツリーの最後のサイズになります。 `type` この計算は必ずしも最新の状態ではないことに注意してください。  
  
## <a name="requirements"></a>要件  
 **・** [システム要件](../../get-started/system-requirements.md)に関するページを参照してください。  
  
 **ヘッダー:** CorDebug .idl、CorDebug. h  
  
 **ライブラリ**CorGuids .lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグ構造体](debugging-structures.md)
- [デバッグ](index.md)
