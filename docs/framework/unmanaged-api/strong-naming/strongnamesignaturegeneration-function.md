---
title: StrongNameSignatureGeneration 関数
ms.date: 03/30/2017
api_name:
- StrongNameSignatureGeneration
api_location:
- mscoree.dll
- mscorsn.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameSignatureGeneration
helpviewer_keywords:
- StrongNameSignatureGeneration function [.NET Framework strong naming]
ms.assetid: 839b765c-3e41-44ce-bf1b-dc10453db18e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 48cdd550e5d8c7c75a603d74456e99a066d5c599
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798967"
---
# <a name="strongnamesignaturegeneration-function"></a>StrongNameSignatureGeneration 関数
指定したアセンブリに対して厳密な名前の署名が生成されます。  
  
 この関数は非推奨とされます。 代わりに[ICLRStrongName:: StrongNameSignatureGeneration](../hosting/iclrstrongname-strongnamesignaturegeneration-method.md)メソッドを使用してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
BOOLEAN StrongNameSignatureGeneration (   
    [in]  LPCWSTR   wszFilePath,  
    [in]  LPCWSTR   wszKeyContainer,  
    [in]  BYTE      *pbKeyBlob,  
    [in]  ULONG     cbKeyBlob,  
    [out] BYTE      **ppbSignatureBlob,  
    [out] ULONG     *pcbSignatureBlob  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `wszFilePath`  
 から厳密な名前の署名が生成されるアセンブリのマニフェストを含むファイルへのパス。  
  
 `wszKeyContainer`  
 から公開キーと秘密キーのペアを格納するキーコンテナーの名前。  
  
 が`pbKeyBlob` null の場合`wszKeyContainer` 、では、暗号化サービスプロバイダー (CSP) 内の有効なコンテナーを指定する必要があります。 この場合、コンテナーに格納されているキーペアがファイルの署名に使用されます。  
  
 が`pbKeyBlob` null でない場合、キーペアは、バイナリラージオブジェクト (BLOB) に格納されていると見なされます。  
  
 キーは 1024-Rivest-shamir-adleman-Rivest-shamir-adleman (RSA) 署名キーである必要があります。 この時点では、他の種類のキーはサポートされていません。  
  
 `pbKeyBlob`  
 から公開/秘密キーのペアへのポインター。 このペアは、Win32 `CryptExportKey`関数によって作成される形式です。 が`pbKeyBlob` null の場合、によって指定`wszKeyContainer`されたキーコンテナーには、キーのペアが含まれていると見なされます。  
  
 `cbKeyBlob`  
 からの`pbKeyBlob`サイズ (バイト単位)。  
  
 `ppbSignatureBlob`  
 入出力共通言語ランタイムが署名を返す場所へのポインター。 が`ppbSignatureBlob` null の場合、ランタイムはによって`wszFilePath`指定されたファイルに署名を格納します。  
  
 が`ppbSignatureBlob` null でない場合は、共通言語ランタイムによって、署名を返す領域が割り当てられます。 呼び出し元は、 [StrongNameFreeBuffer](strongnamefreebuffer-function.md)関数を使用してこの領域を解放する必要があります。  
  
 `pcbSignatureBlob`  
 入出力返されたシグネチャのサイズ (バイト単位)。  
  
## <a name="return-value"></a>戻り値  
 `true`正常に完了した場合は。それ以外`false`の場合は。  
  
## <a name="remarks"></a>Remarks  
 署名を作成`wszFilePath`せずに署名のサイズを計算するには、に null を指定します。  
  
 署名は、ファイルに直接格納するか、呼び出し元に返すことができます。  
  
 関数が正常に完了しない場合は、[StrongNameErrorInfo](strongnameerrorinfo-function.md) 関数を呼び出して、最後に生成されたエラーを取得します。`StrongNameSignatureGeneration`  
  
## <a name="requirements"></a>必要条件  
 **・** [システム要件](../../get-started/system-requirements.md)に関するページを参照してください。  
  
 **ヘッダー:** StrongName  
  
 **ライブラリ**Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [StrongNameSignatureGeneration メソッド](../hosting/iclrstrongname-strongnamesignaturegeneration-method.md)
- [StrongNameSignatureGenerationEx メソッド](../hosting/iclrstrongname-strongnamesignaturegenerationex-method.md)
- [ICLRStrongName インターフェイス](../hosting/iclrstrongname-interface.md)
