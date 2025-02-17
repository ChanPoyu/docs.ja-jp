---
title: ICLRPolicyManager::SetTimeoutAndAction メソッド
ms.date: 03/30/2017
api_name:
- ICLRPolicyManager.SetTimeoutAndAction
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRPolicyManager::SetTimeoutAndAction
helpviewer_keywords:
- ICLRPolicyManager::SetTimeoutAndAction method [.NET Framework hosting]
- SetTimeoutAndAction method [.NET Framework hosting]
ms.assetid: 60454f91-d855-4ddf-bb6d-60a02f5eabab
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 120dbfdc463a7441cce8ca7d87561998a8e28eda
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916961"
---
# <a name="iclrpolicymanagersettimeoutandaction-method"></a>ICLRPolicyManager::SetTimeoutAndAction メソッド
指定された操作のタイムアウト値を設定し、操作が発生したときに共通言語ランタイム (CLR) が実行するポリシーアクションを指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetTimeoutAndAction (  
    [in] EClrOperation operation,  
    [in] DWORD dwMilliseconds,  
    [in] EPolicyAction action  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `operation`  
 からタイムアウトとポリシー `action`を設定する操作を示す [EClrOperation](../../../../docs/framework/unmanaged-api/hosting/eclroperation-enumeration.md) 値の1つ。 次の値がサポートされています。  
  
- OPR_AppDomainUnload  
  
- OPR_ProcessExit  
  
- OPR_ThreadRudeAbortInCriticalRegion  
  
- OPR_ThreadRudeAbortInNonCriticalRegion  
  
 `dwMilliseconds`  
 から新しいタイムアウト値 (ミリ秒単位)。 値が無限である`operation`と、タイムアウトしません。  
  
 `action`  
 から[Epolicyaction](../../../../docs/framework/unmanaged-api/hosting/epolicyaction-enumeration.md)値の1つ。 CLR が発生したとき`operation`に実行するポリシーアクションを示します。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`SetTimeoutAndAction`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドから E_FAIL が返された後は、そのプロセス内で CLR を使用できなくなります。 後続のホストメソッドの呼び出しでは、HOST_E_CLRNOTAVAILABLE が返されます。|  
|E_INVALIDARG|指定され`operation`たに対してタイムアウトを設定できないか、に`action`無効な値が指定されました。|  
  
## <a name="remarks"></a>Remarks  
 `SetTimeoutAndAction`[ICLRPolicyManager:: SetTimeout](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-settimeout-method.md)メソッドと[ICLRPolicyManager:: SetActionOnTimeout](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-setactionontimeout-method.md)メソッドの機能をカプセル化し、これら2つのメソッドの順次呼び出しの代わりに呼び出すことができます。  
  
> [!IMPORTANT]
> すべてのポリシーアクション値は、CLR 操作のタイムアウト動作として指定できるわけではありません。 有効な値については、これら2つの方法に関するトピックの「解説」セクションを参照してください。  
  
## <a name="requirements"></a>必要条件  
 **・** [システム要件](../../../../docs/framework/get-started/system-requirements.md)に関するページを参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ**Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [EClrOperation 列挙型](../../../../docs/framework/unmanaged-api/hosting/eclroperation-enumeration.md)
- [EPolicyAction 列挙型](../../../../docs/framework/unmanaged-api/hosting/epolicyaction-enumeration.md)
- [ICLRPolicyManager インターフェイス](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-interface.md)
- [SetActionOnTimeout メソッド](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-setactionontimeout-method.md)
- [ICLRPolicyManager:: SetTimeoutAndAction](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-settimeoutandaction-method.md)
