---
title: PreBindAssemblyEx 関数
ms.date: 03/30/2017
api_name:
- PreBindAssemblyEx
api_location:
- fusion.dll
api_type:
- DLLExport
f1_keywords:
- PreBindAssemblyEx
helpviewer_keywords:
- PreBindAssemblyEx function [.NET Framework fusion]
ms.assetid: bd285233-a4a2-4b52-bbca-0025a60e4864
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8aa2d174200db76f5c7a6db43e14bb6904604226
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70796330"
---
# <a name="prebindassemblyex-function"></a>PreBindAssemblyEx 関数
アセンブリのポリシー後の表示名を取得します。  
  
 この関数は、.NET Framework インフラストラクチャをサポートします。独自に作成したコードから直接使用するためのものではありません。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT PreBindAssemblyEx (  
    [in]  IApplicationContext *pAppCtx,  
    [in]  IAssemblyName       *pName,  
    [in]  IAssembly           *pAsmParent,  
    [in]  LPCWSTR             pwzRuntimeVersion,  
    [out] IAssemblyName       **ppNamePostPolicy,  
    [in]  LPVOID              pvReserved  
 );  
```  
  
## <a name="parameters"></a>パラメーター  
 `pAppCtx`  
 からアプリケーションコンテキストを識別します。  
  
 `pName`  
 からアセンブリ名を識別します。  
  
 `pAsmParent`  
 から親アセンブリを識別します。 このパラメーターは無視されます。  
  
 `pwzRuntimeVersion`  
 からランタイムのバージョンを識別します。  
  
 `ppNamePostPolicy`  
 入出力ポリシー後の表示名を格納します。  
  
 `pvReserved`  
 [入力] 将来の機能拡張に備えて予約されています。 `pvReserved`null 参照である必要があります。  
  
## <a name="remarks"></a>Remarks  
 `ppNamePostPolicy`出力パラメーターは、関数が HRESULT FUSION_E_REF_DEF_MISMATCH を返す場合にのみ設定されます。 それ以外の場合は null になります。  
  
## <a name="requirements"></a>必要条件  
 **・** [システム要件](../../get-started/system-requirements.md)に関するページを参照してください。  
  
 **ヘッダー:** Fusion. h  
  
 **ライブラリ**Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [Fusion グローバル静的関数](fusion-global-static-functions.md)
