---
title: クレームベースの ID モデル
ms.date: 03/30/2017
ms.assetid: 4a96a9af-d980-43be-bf91-341a23401431
author: BrucePerlerMS
ms.openlocfilehash: c09d3e177d8b0638f0260b76c163bf668235db29
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045523"
---
# <a name="claims-based-identity-model"></a>クレームベースの ID モデル
クレーム対応アプリケーションをビルドすると、ユーザー ID はアプリケーションでクレーム セットとして表されます。 1つの要求にユーザーの名前を指定することも、電子メールアドレスを指定することもできます。 これは、ユーザーが要求を行うたびにユーザーの識別に必要なすべての情報がアプリケーションに提供されるように外部 ID システムを構成し、同時に、信頼できるソースから提供される ID データを暗号化によって保護するという考え方です。  
  
 このモデルでは、シングル サインオンが非常に簡単になり、アプリケーションで次の処理を実行する必要がありません。  
  
- ユーザーを認証する。  
  
- ユーザー アカウントとパスワードを格納する。  
  
- エンタープライズ ディレクトリを呼び出して、ユーザー ID の詳細を検索する。  
  
- 他のプラットフォームまたは企業の ID システムを統合する。  
  
 このモデルでは、ユーザーを認証したシステムによって提供されたクレームに基づいて、アプリケーションが ID 関連の決定を行います。 たとえば、ユーザーの名前を使用してアプリケーションの簡単なパーソナル化を行ったり、アプリケーションのより重要な機能やリソースへのユーザー アクセスを承認したりできます。  
  
 ここでは、次の情報について説明します。  
  
- [クレーム ベース ID の概要](claims-based-identity-model.md#BKMK_1)  
  
- [クレーム ベース ID モデルの基本的なシナリオ](claims-based-identity-model.md#BKMK_2)  
  
<a name="BKMK_1"></a>   
## <a name="introduction-to-claims-based-identity"></a>クレーム ベース ID の概要  
 ここでは、この新しい ID アーキテクチャを理解するうえで役に立つ用語および概念について説明します。  
  
### <a name="identity"></a>同一。  
 Windows Identity Foundation (WIF) でプログラミング モデルを説明する目的で、ここでは "ID" という用語を使用して、保護するシステムのユーザーやその他のエンティティを説明する属性のセットを表しています。  
  
### <a name="claim"></a>クレーム  
 要求は、販売ロールの名前、電子メールアドレス、年齢、メンバーシップなどの id 情報の一部として考えてください。 アプリケーションが受け取るクレームが多くなるほど、ユーザーに関して得られる情報が増えます。 これがエンタープライズ ディレクトリの説明で一般的に使用される "属性" ではなく、"クレーム" と呼ばれているのはなぜでしょうか。 その理由は、配信方法に関係があります。 このモデルでは、アプリケーションはユーザー属性をディレクトリで検索しません。 代わりに、ユーザーがクレームをアプリケーションに配信し、アプリケーションはそのクレームを調べます。 各要求は発行者により作成され、クレームの信頼度は、その発行者の信頼度に基づきます。 たとえば、自分の会社のドメイン コントローラーで作成されたクレームの方が、ユーザーによって作成されたクレームよりも信頼できます。 WIF は <xref:System.Security.Claims.Claim> 型でクレームを表します。この型には、クレームの発行者を見つけるために使用できる <xref:System.Security.Claims.Claim.Issuer%2A> プロパティが含まれます。  
  
### <a name="security-token"></a>セキュリティ トークン  
 ユーザーは、要求と共にクレーム セットをアプリケーションに配信します。 Web サービスでは、これらのクレームは、SOAP エンベロープのセキュリティ ヘッダーに含まれます。 ブラウザー ベースの Web アプリケーションでは、クレームは、ユーザーのブラウザーから HTTP POST 経由で受け取ります。 これらのクレームは受信方法に関係なく、シリアル化されていなければなりません。ここでセキュリティ トークンが提供されます。 セキュリティ トークンは、シリアル化されたクレーム セットであり、発行機関によってデジタル署名されています。 署名は重要です。署名により、ユーザーが単に多数のクレームを作成して送信しただけではないことが保証されます。 暗号化が不要な (要求されない) セキュリティ レベルの低い状況では、署名されていないトークンを使用できますが、このシナリオについてはここでは説明しません。  
  
 セキュリティ トークンを作成して読み取る機能は、WIF の中心的な機能の 1 つです。 WIF および .NET Framework は、すべての暗号化作業を処理し、読み取り可能なクレーム セットでアプリケーションを表します。  
  
### <a name="issuing-authority"></a>発行機関  
 発行機関の種類は、Kerberos チケットを発行するドメイン コントローラーから、X.509 証明書を発行する証明機関まで数多くありますが、ここで説明するのは、クレームが含まれるセキュリティ トークンを発行する機関です。 この発行機関は、セキュリティ トークンの発行方法を認識する Web アプリケーションまたは Web サービスです。 発行機関では、適切なクレームを発行するために、要求を行う対象の証明書利用者およびユーザーに関する十分な情報が必要です。また、ユーザー ストアとやり取りしてクレームを検索し、ユーザー認証を独自に行う場合もあります。  
  
 どの発行機関を選択しても、その機関は ID ソリューションで中心的な役割を果たします。 クレームを信頼することでアプリケーションから認証を除外すると、その機関に認証機能が委任され、その機関でユーザーの認証が行われます。  
  
### <a name="security-token-service-sts"></a>STS (セキュリティ トークン サービス)  
 セキュリティ トークン サービス (STS) は、WS-Trust プロトコルおよび WS-Federation プロトコルに従って、セキュリティ トークンの構築、署名、および発行を行うサービス コンポーネントです。 これらのプロトコルを実装するには多大な労力を伴いますが、必要な作業はすべて WIF が吸収するため、これらのプロトコルに習熟していなくても、無理なく STS を利用し、最小限の作業量で運用することができます。 [Active Directory® フェデレーション サービス (AD FS) 2.0](https://go.microsoft.com/fwlink/?LinkID=247516) などの既成の STS や、[Microsoft Azure のアクセス制御サービス (ACS)](https://go.microsoft.com/fwlink/?LinkID=247517) などのクラウド STS を使用することもできますが、カスタム トークンを発行したり、カスタム認証/承認の機能を実装する必要がある場合には、WIF を使用してカスタム STS を自分で作成することもできます。 WIF を使用すると、独自の STS を簡単に作成できます。  
  
### <a name="relying-party-application"></a>証明書利用者アプリケーション  
 クレームに依存するアプリケーションをビルドする場合は、証明書利用者 (RP) アプリケーションをビルドします。 RP は、"クレーム対応アプリケーション"、"クレーム ベースのアプリケーション" とも呼ばれます。 Web アプリケーションと Web サービスは両方とも RP にできます。 RP アプリケーションは STS によって発行されたトークンを使用し、トークンからクレームを抽出して、それを ID 関連のタスクに使用します。 WIF には、RP アプリケーションのビルドに役立つ機能が用意されています。  
  
### <a name="standards"></a>標準  
 このすべての相互運用を実現するために、前のシナリオでは WS-* 標準がいくつか使用されています。 ポリシーは WS-MetadataExchange を使用して取得されますが、そのポリシー自体は WS-Policy 仕様に準拠しています。 STS では、WS-Trust 仕様が実装されているエンドポイントを公開します。この仕様には、セキュリティ トークンを要求および受信する方法が記述されています。 現在、ほとんどの sts は Security Assertion Markup Language (SAML) でフォーマットされたトークンを発行しています。 SAML は、相互運用可能な方法でクレームを表現できる、業界で認められた XML ボキャブラリです。 つまり、マルチプラットフォームでは、まったく異なるプラットフォーム上の STS と通信でき、プラットフォームに関係なくすべてのアプリケーションでシングル サインオンを実現できます。  
  
### <a name="browser-based-applications"></a>ブラウザー ベースのアプリケーション  
 クレーム ベースの ID モデルを使用できるのはスマート クライアントだけではありません。 この ID モデルは、ブラウザーベースのアプリケーション (パッシブ クライアントとも呼ばれます) でも使用できます。 次のシナリオでは、そのしくみについて説明します。  
  
 最初に、ユーザーがブラウザーでクレーム対応アプリケーション (証明書利用者アプリケーション) にアクセスします。 Web アプリケーションは、ユーザーを認証できるようにブラウザーを STS にリダイレクトします。 STS は単純な Web アプリケーションでホストされています。このアプリケーションで、受信した要求を読み取り、標準的な HTTP メカニズムを使用してユーザーを認証してから、SAML トークンを作成し、JavaScript コードを使用して応答します。このコードによって、ブラウザーで SAML トークンを RP に送り返す HTTP POST が開始されます。 この POST の本文に、RP が要求したクレームが含まれています。 ここでは、一般的に RP ではクレームを Cookie にパッケージ化して、要求が行われるたびにユーザーをリダイレクトする必要がないようにします。  
  
<a name="BKMK_2"></a>   
## <a name="basic-scenario-for-a-claims-based-identity-model"></a>クレーム ベース ID モデルの基本的なシナリオ  
 次に、クレーム ベースのシステムの例を示します。  
  
 ![パートナー認証の依存のフロー](./media/conc-relying-partner-processc.png "conc_relying_partner_processc")  
  
 この図は、認証に WIF を使用するように構成された Web サイト (証明書利用者アプリケーション、RP) と、そのサイトを使用するクライアント (Web ブラウザー) を示しています。  
  
1. 認証されていないユーザーがページを要求すると、ブラウザーは id プロバイダー (IdP) ページにリダイレクトされます。  
  
2. IdP では、ユーザーはユーザー名/パスワードや Kerberos 認証などの資格情報を提示する必要があります。  
  
3. IdP は、ブラウザーに返されるトークンをに発行します。  
  
4. ブラウザーは、最初に要求されたページにリダイレクトされます。ここで WIF は、トークンがページにアクセスするための要件を満たしているかどうかを判断します。 満たしている場合は、Cookie が発行されてセッションが確立されるため、認証が必要なのは 1 回だけです。その後、コントロールはアプリケーションに渡されます。
