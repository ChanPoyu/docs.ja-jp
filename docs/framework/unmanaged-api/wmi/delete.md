---
title: Delete 関数 (アンマネージ API リファレンス)
description: Delete 関数は、指定されたプロパティとそのすべての修飾子を CIM クラス定義から削除します。
ms.date: 11/06/2017
api_name:
- Delete
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- Delete
helpviewer_keywords:
- Delete function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a1bf9bd5d93d1affee649588138456269411d280
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798673"
---
# <a name="delete-function"></a>Delete 関数

指定したプロパティとそのすべての修飾子を CIM クラス定義から削除します。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>構文

```cpp
HRESULT Delete (
   [in] int               vFunc,
   [in] IWbemClassObject* ptr,
   [in] LPCWSTR           wszName
);
```

## <a name="parameters"></a>パラメーター

`vFunc`\
からこのパラメーターは使用されていません。

`ptr`\
から[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)インスタンスへのポインター。

`wszName`\
から削除するプロパティの名前。 `wszName`は、有効`LPCWSTR`なへのポインターである必要があります。

## <a name="return-value"></a>戻り値

この関数によって返される次の値は、 *WbemCli*ヘッダーファイルで定義されています。また、コード内で定数として定義することもできます。

|定数  |Value  |説明  |
|---------|---------|---------|
| `WBEM_E_FAILED` | 0x80041001 | 特定できないエラーが発生しました。 |
| `WBEM_E_INVALID_OPERATION` | 0x80041016 | プロパティを削除できません。 |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | `wszName` が無効です。 |
| `WBEM_E_NOT_FOUND` | 0x80041002 | 指定されたプロパティが存在しません。 |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 操作を完了するために必要なメモリが不足しています。 |
| `WBEM_E_PROPAGATED_PROPERTY` | 0x8004101c | プロパティは、基本クラスから継承されます。 |
| `WBEM_E_SYSTEM_PROPERTY` | | プロパティはシステムプロパティです。 |
|`WBEM_S_NO_ERROR` | 0 | 関数の呼び出しに成功しました。  |
| `WBEM_E_RESET_TO_DEFAULT` | 0x80041030 | 関数は、現在のクラスのオーバーライドの既定値を削除しました。 親クラスのこのプロパティの既定値は再アクティブ化されています。 |

## <a name="remarks"></a>Remarks

この関数は、 [IWbemClassObject::D e)](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-delete)メソッドの呼び出しをラップします。

## <a name="requirements"></a>必要条件

**・** [システム要件](../../get-started/system-requirements.md)に関するページを参照してください。

**ヘッダー:** WMINet_Utils

**.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンスカウンター (アンマネージ API リファレンス)](index.md)
