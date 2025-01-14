---
title: <legacyCorruptedStateExceptionsPolicy> 要素
ms.date: 03/30/2017
helpviewer_keywords:
- <legacyCorruptedStateExceptionsPolicy> element
- legacyCorruptedStateExceptionsPolicy element
ms.assetid: e0a55ddc-bfa8-4f3e-ac14-d1fc3330e4bb
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6566437d899b768cda1bab74bb1310deb7aa74db
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252516"
---
# <a name="legacycorruptedstateexceptionspolicy-element"></a>\<legacyCorruptedStateExceptionsPolicy > 要素
共通言語ランタイムで、マネージコードがアクセス違反とその他の破損状態例外をキャッチできるようにするかどうかを指定します。  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<ランタイム >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<legacyCorruptedStateExceptionsPolicy>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<legacyCorruptedStateExceptionsPolicy enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`enabled`|必須の属性です。<br /><br /> アプリケーションがアクセス違反などの破損状態の例外エラーをキャッチすることを指定します。|  
  
## <a name="enabled-attribute"></a>enabled 属性  
  
|値|説明|  
|-----------|-----------------|  
|`false`|アプリケーションでは、アクセス違反などの破損状態の例外エラーはキャッチされません。 既定値です。|  
|`true`|アプリケーションは、アクセス違反などの破損状態の例外エラーをキャッチします。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`runtime`|アセンブリのバインディングとガベージ コレクションに関する情報が含まれています。|  
  
## <a name="remarks"></a>Remarks  
 .NET Framework バージョン3.5 以前では、共通言語ランタイムは、破損したプロセス状態によって発生した例外をキャッチするために、マネージコードを許可しました。 この種類の例外の例として、アクセス違反があります。  
  
 .NET Framework 4 以降では、マネージコードはブロック内の`catch`これらの種類の例外をキャッチしなくなりました。 ただし、次の2つの方法で、この変更をオーバーライドし、破損状態例外の処理を維持することができます。  
  
- 要素の`enabled`属性をに`true`設定します。 `<legacyCorruptedStateExceptionsPolicy>` この構成設定は、プロセス全体に適用され、すべてのメソッドに影響します。  
  
 \- または -  
  
- <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute?displayProperty=nameWithType> 例外`catch`ブロックを含むメソッドに属性を適用します。  
  
 この構成要素は、.NET Framework 4 以降でのみ使用できます。  
  
## <a name="example"></a>例  
 次の例では、アプリケーションが .NET Framework 4 より前の動作に戻し、すべての破損状態の例外エラーをキャッチするように指定する方法を示します。  
  
```xml  
<configuration>  
   <runtime>  
      <legacyCorruptedStateExceptionsPolicy enabled="true" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute>
- [ランタイム設定スキーマ](index.md)
- [構成ファイル スキーマ](../index.md)
