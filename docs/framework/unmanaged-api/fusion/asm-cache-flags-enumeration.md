---
title: ASM_CACHE_FLAGS 列挙型
ms.date: 03/30/2017
api_name:
- ASM_CACHE_FLAGS
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- ASM_CACHE_FLAGS
helpviewer_keywords:
- ASM_CACHE_FLAGS enumeration [.NET Framework fusion]
ms.assetid: 82e9a7da-321b-48b8-b239-52eaffda6be8
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0e3e9da3db71d3e24b2a60ff032a631680055b88
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795274"
---
# <a name="asm_cache_flags-enumeration"></a>ASM_CACHE_FLAGS 列挙型
グローバルアセンブリキャッシュ内の[Iassemblycacheitem](iassemblycacheitem-interface.md)によって表されるアセンブリのソースを示します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum {  
    ASM_CACHE_ZAP       = 0x01,  
    ASM_CACHE_GAC       = 0x02,  
    ASM_CACHE_DOWNLOAD  = 0x04,  
    ASM_CACHE_ROOT      = 0x08,  
    ASM_CACHE_ROOT_EX   = 0x80  
} ASM_CACHE_FLAGS;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`ASM_CACHE_ZAP`|Ngen.exe を使用して、プリコンパイル済みアセンブリのキャッシュを列挙します。|  
|`ASM_CACHE_GAC`|グローバルアセンブリキャッシュを列挙します。|  
|`ASM_CACHE_DOWNLOAD`|要求時にダウンロードされた、またはシャドウコピーされたアセンブリを列挙します。|  
|`ASM_CACHE_ROOT`|[Getcachepath](getcachepath-function.md)関数が、共通言語ランタイム (CLR) バージョン2.0 のグローバルアセンブリキャッシュへのパスを返す必要があることを示します。 [Getcachepath](getcachepath-function.md)への呼び出しのコンテキストでのみ意味があります。|  
|`ASM_CACHE_ROOT_EX`|[Getcachepath](getcachepath-function.md)関数が CLR version 4 のグローバルアセンブリキャッシュへのパスを返す必要があることを示します。 [Getcachepath](getcachepath-function.md)への呼び出しのコンテキストでのみ意味があります。|  
  
## <a name="requirements"></a>必要条件  
 **・** [システム要件](../../get-started/system-requirements.md)に関するページを参照してください。  
  
 **ヘッダー:** Fusion. h  
  
 **ライブラリ**Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [GetCachePath 関数](getcachepath-function.md)
- [IAssemblyCacheItem インターフェイス](iassemblycacheitem-interface.md)
- [Fusion 列挙型](fusion-enumerations.md)
