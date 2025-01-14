---
title: <network> 要素 (ネットワーク設定)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#network
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/mailSettings/smtp/network
helpviewer_keywords:
- <network> element
- network element
ms.assetid: 2c2c6ad4-ed11-48ab-b28e-2bc0ba9b42c7
ms.openlocfilehash: ee60b990bc749dbb9c5d0e7426c57e9392ddf9d4
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69920976"
---
# <a name="network-element-network-settings"></a>\<network > 要素 (ネットワーク設定)
外部の簡易メール転送プロトコル (SMTP) サーバーのネットワークオプションを構成します。  
  
 \<configuration>  
\<system.net>  
\<mailSettings>  
\<smtp>  
\<network>  
  
## <a name="syntax"></a>構文  
  
```xml  
<network  
  clientDomain="string"   
  defaultCredentials="true|false"  
  enableSsl="true|false"  
  host="string"   
  password="string"  
  port="integer"   
  targetName="string"  
  userName="string"  
/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`clientDomain`|SMTP メールサーバーに接続するための最初の SMTP プロトコル要求で使用するクライアントドメイン名を指定します。 既定値は、要求を送信しているローカルコンピューターの localhost 名です。|  
|`defaultCredentials`|Smtp トランザクションの SMTP メールサーバーへのアクセスに、既定のユーザー資格情報を使用するかどうかを指定します。 既定値は `false` です。|  
|`enableSsl`|SMTP メールサーバーへのアクセスに SSL を使用するかどうかを指定します。 既定値は `false` です。|  
|`host`|SMTP トランザクションに使用する SMTP メールサーバーのホスト名を指定します。 この属性には既定値はありません。|  
|`password`|SMTP メールサーバーへの認証に使用するパスワードを指定します。 この属性には既定値はありません。|  
|`port`|SMTP メールサーバーへの接続に使用するポート番号を指定します。 既定値は、25 です。|  
|`targetName`|SMTP トランザクションの拡張保護を使用するときに認証に使用するサービスプロバイダー名 (SPN) を指定します。 この属性には既定値はありません。|  
|`userName`|SMTP メールサーバーへの認証に使用するユーザー名を指定します。 この属性には既定値はありません。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<smtp> 要素 (ネットワーク設定)](smtp-element-network-settings.md)|簡易メール転送プロトコル (SMTP) 電子メールの送信オプションを構成します。|  
  
## <a name="remarks"></a>Remarks  
 一部の SMTP サーバーでは、使用する前にサーバーに対して認証を行う必要があります。 ホストで既定のネットワーク資格情報を使用して認証する場合は、 `defaultCredentials`属性をに`true`設定します。 プロパティ<xref:System.Net.Configuration.SmtpNetworkElement.DefaultCredentials%2A?displayProperty=nameWithType>は、適用可能`defaultCredentials`な構成ファイルから属性の現在の値を取得するために使用できます。  
  
 基本認証 (ユーザー名とパスワード) を使用して、SMTP サーバーに対する認証を行うこともできます。 このオプションを使用するには、指定した SMTP サーバーの有効なユーザー名とパスワードを指定する必要があります。  
  
> [!NOTE]
> 基本認証は、 `userName`および`password`の値を暗号化せずにサーバーに送信します。 ネットワークトラフィックを監視するすべてのユーザーは、資格情報を表示し、それらを使用してサーバーに接続できます。 Kerberos や NT LAN Manager (NTLM) など、より安全な認証メカニズムの使用を検討する必要があります。`defaultCredentials` が`true`の場合、サーバーがこれらのプロトコルをサポートする場合、Kerberos または NTLM が使用されます。  
  
 基本認証および既定のネットワーク資格情報オプションは、同時には指定できません。をに`defaultCredentials` `true`設定し、ユーザー名とパスワードを指定した場合、既定のネットワーク資格情報が使用され、基本認証データは無視されます。  
  
 基本認証でを指定`userName`する場合は、メールサーバーに対して自分で認証`password`を行うようにを指定する必要もあります。  
  
 プロパティ<xref:System.Net.Configuration.SmtpNetworkElement.UserName%2A?displayProperty=nameWithType>は、適用可能`userName`な構成ファイルから属性の現在の値を取得するために使用できます。 プロパティ<xref:System.Net.Configuration.SmtpNetworkElement.Password%2A?displayProperty=nameWithType>は、適用可能`password`な構成ファイルから属性の現在の値を取得するために使用できます。 通常`password` 、セキュリティ上の理由から、属性を構成ファイルに入力することはできません。  
  
 属性`clientDomain`は、smtp プロトコルの初期要求で使用されるクライアントのドメイン名を smtp サーバーに変更します。 属性`clientDomain`は、既定で使用される localhost 名ではなく、ローカルコンピューターの完全修飾ドメイン名に設定できます。 これにより、SMTP プロトコル標準への準拠が向上します。 既定値は、要求を送信しているローカルコンピューターの localhost 名です。 プロパティ<xref:System.Net.Configuration.SmtpNetworkElement.ClientDomain%2A?displayProperty=nameWithType>は、適用可能`clientDomain`な構成ファイルから属性の現在の値を取得するために使用できます。  
  
 拡張`targetName`保護を使用する場合、この属性は認証に使用されます。 既定値は "SMTPSVC/\<host >" の形式です。ここ\<で、host > は SMTP メールサーバーのホスト名です。 プロパティ<xref:System.Net.Configuration.SmtpNetworkElement.TargetName%2A?displayProperty=nameWithType>は、適用可能`targetName`な構成ファイルから属性の現在の値を取得するために使用できます。  
  
 属性`enableSsl`では、SMTP メールサーバーへのアクセスに SSL を使用するかどうかを指定します。 <xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType>クラスでサポートされているのは、RFC 3207 で定義されているトランスポート層セキュリティ経由の Secure smtp に対する smtp サービス拡張のみです。 このモードでは、暗号化されていないチャネルで SMTP セッションが開始され、SSL を使用してセキュリティで保護された通信に切り替えるために、クライアントからサーバーに STARTTLS コマンドが発行されます。 詳細については、インターネット技術標準化委員会 (IETF) によって発行された RFC 3207 を参照してください。  
  
 代替の接続方法では、プロトコルコマンドが送信される前に、SSL セッションが事前に確立されます。 この接続方法は SMTPS とも呼ばれ、既定ではポート465を使用します。 SSL を使用したこの代替接続方法は、現在サポートされていません。  
  
 プロパティ<xref:System.Net.Configuration.SmtpNetworkElement.EnableSsl%2A?displayProperty=nameWithType>は、適用可能`enableSsl`な構成ファイルから属性の現在の値を取得するために使用できます。  
  
## <a name="example"></a>例  
 次の例では、既定のネットワーク資格情報を使用して電子メールを送信するための適切な SMTP パラメーターを指定しています。  
  
```xml  
<configuration>  
  <system.net>  
    <mailSettings>  
      <smtp deliveryMethod="Network">  
        <network  
          clientDomain="www.contoso.com"  
          defaultCredentials="true"  
          enableSsl="false"  
          host="mail.contoso.com"  
          port="25"  
        />  
      </smtp>  
    </mailSettings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Net.Configuration.SmtpNetworkElement?displayProperty=nameWithType>
- <xref:System.Net.Configuration.SmtpSection?displayProperty=nameWithType>
- <xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType>
- [ネットワーク設定スキーマ](index.md)
