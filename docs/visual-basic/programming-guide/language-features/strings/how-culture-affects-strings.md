---
title: Visual Basic においてカルチャが文字列に与える影響
ms.date: 07/20/2015
helpviewer_keywords:
- locale [Visual Basic], effect on strings
- strings [Visual Basic], locale dependence
ms.assetid: c4664444-ee0d-47bf-bef1-eaa3c54bdd7f
ms.openlocfilehash: d090a6e89a470958dd323c3f249ed0658dc1cefa
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69955097"
---
# <a name="how-culture-affects-strings-in-visual-basic"></a>Visual Basic においてカルチャが文字列に与える影響
このヘルプページでは、Visual Basic がカルチャ情報を使用して文字列の変換と比較を実行する方法について説明します。  
  
## <a name="when-to-use-culture-specific-strings"></a>カルチャ固有の文字列を使用する場合  
 通常は、ユーザーに表示されるすべてのデータに対してカルチャ固有の文字列を使用し、アプリケーションの内部データにカルチャに依存しない文字列を使用する必要があります。  
  
 たとえば、アプリケーションがユーザーに文字列として日付を入力するように要求した場合、ユーザーはカルチャに従って文字列を書式設定する必要があり、アプリケーションは文字列を適切に変換する必要があります。 その後、アプリケーションでその日付がユーザーインターフェイスに表示された場合は、ユーザーのカルチャに示されます。  
  
 ただし、アプリケーションが中央サーバーに日付をアップロードする場合は、異なる日付形式間の混乱を防ぐために、特定のカルチャに従って文字列の書式を設定する必要があります。  
  
## <a name="culture-sensitive-functions"></a>カルチャに依存する関数  
 すべての Visual Basic 文字列変換関数 ( `Str`および`Val`関数を除く) では、アプリケーションのカルチャ情報を使用して、変換と比較がアプリケーションのカルチャに適していることを確認します。ユーザーズ.  
  
 カルチャ設定が異なるコンピューターで実行されるアプリケーションで文字列変換関数を正常に使用するための鍵は、特定のカルチャ設定を使用し、現在のカルチャ設定を使用する関数について理解することです。 既定では、アプリケーションのカルチャ設定は、オペレーティングシステムのカルチャ設定から継承されていることに注意してください。 詳細については<xref:Microsoft.VisualBasic.Strings.Asc%2A>、「」 <xref:Microsoft.VisualBasic.Strings.ChrW%2A>、「」、「」、「」、「」、および「[型変換関数](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)」を参照してください<xref:Microsoft.VisualBasic.Conversion.Hex%2A> <xref:Microsoft.VisualBasic.Strings.AscW%2A>。 <xref:Microsoft.VisualBasic.Strings.Chr%2A> <xref:Microsoft.VisualBasic.Strings.Format%2A> <xref:Microsoft.VisualBasic.Conversion.Oct%2A>  
  
 (数値を文字列に変換します`Val` ) および (文字列を数値に変換) 関数は、文字列と数値を変換するときに、アプリケーションのカルチャ情報を使用しません。 `Str` 代わりに、ピリオド (.) のみが有効な小数点区切り記号として認識されます。 これらの関数のカルチャに対応するアナログは次のとおりです。  
  
- **現在のカルチャを使用する変換。** 関数`CStr`と`Format`関数は、数値を文字列に変換し、 `CDbl`関数`CInt`と関数は文字列を数値に変換します。  
  
- **特定のカルチャを使用する変換。** 各数値オブジェクトには`ToString(IFormatProvider)` 、数値を文字列に変換するメソッド`Parse(String, IFormatProvider)`と、文字列を数値に変換するメソッドがあります。 たとえば`Double` 、型にはメソッドと<xref:System.Double.ToString%28System.IFormatProvider%29> <xref:System.Double.Parse%28System.String%2CSystem.IFormatProvider%29>メソッドが用意されています。  
  
 詳細については、次のトピックを参照してください。 <xref:Microsoft.VisualBasic.Conversion.Str%2A> および <xref:Microsoft.VisualBasic.Conversion.Val%2A>  
  
## <a name="using-a-specific-culture"></a>特定のカルチャを使用する  
 たとえば、文字列形式の日付を Web サービスに送信するアプリケーションを開発しているとします。 この場合、アプリケーションでは、文字列変換に特定のカルチャを使用する必要があります。 理由を説明するために、日付の<xref:System.DateTime.ToString>メソッドを使用した結果を考えてみましょう。アプリケーションでこのメソッドを使用して2005年7月4日の日付が書式設定されている場合、米国 English (en-us) カルチャで実行すると "7/4/2005 12:00:00 AM" が返されますが、ドイツ語 (de) カルチャで実行すると "04.07.2005 00:00:00" が返されます。  
  
 特定のカルチャ形式で文字列変換を実行する必要がある場合は、.NET Framework に`CultureInfo`組み込まれているクラスを使用する必要があります。 カルチャ名を<xref:System.Globalization.CultureInfo.%23ctor%2A>コンストラクターに`CultureInfo`渡すことによって、特定のカルチャの新しいオブジェクトを作成できます。 サポートされているカルチャ名は<xref:System.Globalization.CultureInfo> 、クラスのヘルプページに記載されています。  
  
 または、 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType>プロパティから*インバリアントカルチャ*のインスタンスを取得することもできます。 インバリアントカルチャは英語のカルチャに基づいていますが、いくつかの違いがあります。 たとえば、インバリアントカルチャでは、12時間形式ではなく、24時間制が指定されています。  
  
 日付をカルチャの文字列に変換するには、 <xref:System.Globalization.CultureInfo>オブジェクトを date オブジェクトの<xref:System.DateTime.ToString%28System.IFormatProvider%29>メソッドに渡します。 たとえば、次のコードでは、アプリケーションのカルチャ設定に関係なく、"07/04/2005 00:00:00" が表示されます。  
  
 [!code-vb[VbVbalrConcepts#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConcepts/VB/Class1.vb#1)]  
  
> [!NOTE]
> 日付リテラルは、常に英語のカルチャに従って解釈されます。  
  
## <a name="comparing-strings"></a>文字列の比較  
 文字列を比較する必要がある重要な状況には、次の2つがあります。  
  
- **ユーザーに表示するデータを並べ替えます。** 文字列が適切に並べ替えられるように、現在のカルチャに基づいた操作を使用します。  
  
- **2つのアプリケーション内部文字列が完全に一致するかどうかを判断する (通常はセキュリティ上の理由で)。** 現在のカルチャを無視する操作を使用します。  
  
 Visual Basic <xref:Microsoft.VisualBasic.Strings.StrComp%2A>関数を使用すると、両方の種類の比較を実行できます。 比較の種類`Compare`を制御する省略可能な引数を`Text`指定します。完全`Binary`一致を確認するためのほとんどの入力と出力に使用します。  
  
 関数`StrComp`は、並べ替え順序に基づいて比較される2つの文字列の間の関係を示す整数を返します。 結果の正の値は、最初の文字列が2番目の文字列より大きいことを示します。 結果が負の値の場合は、最初の文字列が小さいことを示し、0は文字列の等価性を示します。  
  
 [!code-vb[VbVbalrStrings#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class1.vb#22)]  
  
 `StrComp`関数の .NET Framework パートナー <xref:System.String.Compare%2A?displayProperty=nameWithType> (メソッド) を使用することもできます。 これは、基本文字列クラスの静的でオーバーロードされたメソッドです。 次の例は、このメソッドの使用方法を示しています。  
  
 [!code-vb[VbVbalrStrings#48](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#48)]  
  
 比較の実行方法を細かく制御するには、 <xref:System.String.Compare%2A>メソッドの追加のオーバーロードを使用します。 メソッドでは、 `comparisonType`引数を使用して、使用する比較の種類を指定できます。 <xref:System.String.Compare%2A?displayProperty=nameWithType>  
  
|引数の`comparisonType`値|比較の種類|使用に適した状況|  
|---|---|---|  
|`Ordinal`|文字列のコンポーネントバイトに基づく比較。|大文字と小文字を区別する識別子、セキュリティ関連の設定、またはバイトが正確に一致する必要があるその他の非言語識別子を比較する場合は、この値を使用します。|  
|`OrdinalIgnoreCase`|文字列のコンポーネントバイトに基づく比較。<br /><br /> `OrdinalIgnoreCase`インバリアントカルチャ情報を使用して、2つの文字の大文字と小文字が区別されるかどうかを判断します。|大文字と小文字を区別しない識別子、セキュリティ関連の設定、および Windows に格納されているデータを比較する場合は、この値を使用します。|  
|`CurrentCulture` または `CurrentCultureIgnoreCase`|現在のカルチャにおける文字列の解釈に基づく比較。|ユーザーに表示されるデータ、ほとんどのユーザー入力、および言語の解釈を必要とするその他のデータを比較するときに、これらの値を使用します。|  
|`InvariantCulture` または `InvariantCultureIgnoreCase`|インバリアントカルチャにおける文字列の解釈に基づく比較。<br /><br /> これは、 `Ordinal`とと`OrdinalIgnoreCase`は異なります。インバリアントカルチャは、受け入れられた範囲外の文字を等価の不変文字として扱います。|これらの値は、持続データを比較する場合、または固定の並べ替え順序を必要とする言語関連のデータを表示する場合にのみ使用してください。|  
  
### <a name="security-considerations"></a>セキュリティの考慮事項  
 アプリケーションで、比較または大文字と小文字の変更操作の結果に基づいてセキュリティの決定を行う場合<xref:System.String.Compare%2A?displayProperty=nameWithType>は、メソッドを使用`OrdinalIgnoreCase`し、 `comparisonType`または引数にまたはを渡し`Ordinal`ます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Globalization.CultureInfo>
- [Visual Basic の文字列の概要](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)
- [データ型変換関数](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)
