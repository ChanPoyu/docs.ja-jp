---
title: COR_ARRAY_LAYOUT 構造体
ms.date: 03/30/2017
api_name:
- COR_ARRAY_LAYOUT
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_ARRAY_LAYOUT
helpviewer_keywords:
- COR_DEBUG_IL_TO_NATIVE_MAP structure [.NET Framework debugging]
ms.assetid: aa20ac3d-6f60-4aa2-91c5-f3a86f82eba8
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ec9c4f3afb8f3b7e75e22874996d57d29ce8cf16
ms.sourcegitcommit: 3caa92cb97e9f6c31f21769c7a3f7c4304024b39
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2019
ms.locfileid: "71274214"
---
# <a name="cor_array_layout-structure"></a>COR_ARRAY_LAYOUT 構造体
メモリ内の配列オブジェクトのレイアウトに関する情報が提供されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef struct COR_ARRAY_LAYOUT {  
    COR_TYPEID componentID;  
    CorElementType componentType;  
    ULONG32 firstElementOffset;  
    ULONG32 elementSize;  
    ULONG32 countOffset;   
    ULONG32 rankSize;   
    ULONG32 numRanks;   
    ULONG32 rankOffset;   
} COR_ARRAY_LAYOUT;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`componentID`|配列に格納されているオブジェクトの型の識別子。|  
|`componentType`|コンポーネントがガベージコレクション参照、値クラス、またはプリミティブであるかどうかを示す CorElementType 列挙値。|  
|`firstElementOffset`|配列内の最初の要素へのオフセット。|  
|`elementSize`|各要素のサイズ。|  
|`countOffset`|配列内の要素の数へのオフセット。|  
|`rankSize`|ランクのサイズ (バイト単位)。|  
|`numRanks`|配列内のランクの数。|  
|`rankOffset`|ランクの開始位置を示すオフセット。|  
  
## <a name="remarks"></a>コメント  
 この`rankSize`フィールドは、多次元配列内のランクのサイズを指定します。 これは、1次元配列に対しても正確です。  
  
 の`numRanks`値は、1次元`N`配列の場合は1、次元の`N`多次元配列の場合は1になります。  
  
## <a name="requirements"></a>要件  
 **・** [システム要件](../../get-started/system-requirements.md)に関するページを参照してください。  
  
 **ヘッダー:** CorDebug .idl、CorDebug. h  
  
 **ライブラリ**CorGuids .lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグ構造体](debugging-structures.md)
- [デバッグ](index.md)
