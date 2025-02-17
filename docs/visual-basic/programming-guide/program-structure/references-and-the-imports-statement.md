---
title: 参照と Imports ステートメント (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- assemblies [Visual Basic], namespaces
- references [Visual Basic], assembly
- namespaces [Visual Basic], assemblies
- referencing assemblies
- Imports statement [Visual Basic], referencing assemblies
- assemblies [Visual Basic], references
ms.assetid: 38149bd4-0a6f-4b31-b5f8-94a8c33f1600
ms.openlocfilehash: 5b810af86f8659ffbe27d23d36aece408516a9bd
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972059"
---
# <a name="references-and-the-imports-statement-visual-basic"></a>参照と Imports ステートメント (Visual Basic)
**[プロジェクト]** メニューの **[参照の追加]** をクリックして、プロジェクトで外部オブジェクトを使用できるようにすることができます。 Visual Basic の参照は、タイプライブラリのようなアセンブリを指すことができますが、さらに多くの情報が含まれています。  
  
## <a name="the-imports-statement"></a>Imports ステートメント  
 アセンブリには、1つまたは複数の名前空間が含まれます。 アセンブリへの参照を追加するときに、モジュール内のアセンブリ`Imports`の名前空間の表示を制御するステートメントをモジュールに追加することもできます。 ステートメント`Imports`は、一意の参照を提供するために必要な名前空間の部分のみを使用できるようにするスコープコンテキストを提供します。  
  
 `Imports`ステートメントには、次の構文があります。  
  
 `Imports [Aliasname =] Namespace`  
  
 `Aliasname`は、インポートされた名前空間を参照するためにコード内で使用できる短い名前を参照します。 `Namespace`は、プロジェクト参照、プロジェクト内の定義、または前`Imports`のステートメントを通じて使用できる名前空間です。  
  
 モジュールには、任意の数`Imports`のステートメントを含めることができます。 これらは、 `Option`ステートメントが存在する場合は、他のコードよりも前に記述する必要があります。  
  
> [!NOTE]
> プロジェクト参照を`Imports`ステートメント`Declare`またはステートメントと混同しないようにしてください。 プロジェクト参照は、アセンブリ内のオブジェクトなどの外部オブジェクトを、Visual Basic プロジェクトで使用できるようにします。 `Imports`ステートメントは、プロジェクト参照へのアクセスを簡略化するために使用されますが、これらのオブジェクトへのアクセスは提供されません。 ステートメント`Declare`は、ダイナミックリンクライブラリ (DLL) 内の外部プロシージャへの参照を宣言するために使用されます。  
  
## <a name="using-aliases-with-the-imports-statement"></a>Imports ステートメントでの別名の使用  
 ステートメント`Imports`を使用すると、参照の完全修飾名を明示的に入力する必要がなくなるため、クラスのメソッドに簡単にアクセスできるようになります。 エイリアスを使用すると、名前空間の1つの部分のみにわかりやすい名前を割り当てることができます。 たとえば、1つのテキストが複数行に表示されるキャリッジリターン/ラインフィードシーケンスは、 <xref:Microsoft.VisualBasic.ControlChars> <xref:Microsoft.VisualBasic?displayProperty=nameWithType>名前空間のモジュールの一部になります。 エイリアスのないプログラムでこの定数を使用するには、次のコードを入力する必要があります。  
  
 [!code-vb[VbVbalrApplication#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/Class1.vb#3)]  
  
 `Imports`ステートメントは、常に、モジュール内の`Option`ステートメントの直後の最初の行である必要があります。 次のコードフラグメントは、エイリアスをインポートして<xref:Microsoft.VisualBasic.ControlChars?displayProperty=nameWithType>モジュールに割り当てる方法を示しています。  
  
 [!code-vb[VbVbalrApplication#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/Class1.vb#4)]  
  
 この名前空間への今後の参照は、大幅に短縮される可能性があります。  
  
 [!code-vb[VbVbalrApplication#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/Class1.vb#5)]  
  
 ステートメントに`Imports`エイリアス名が含まれていない場合、インポートされた名前空間内で定義された要素は、修飾なしでモジュールで使用できます。 エイリアス名を指定する場合は、その名前空間内に含まれる名前の修飾子として使用する必要があります。  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.ControlChars>
- <xref:Microsoft.VisualBasic>
- [Visual Basic 内の名前空間](namespaces.md)
- [.NET のアセンブリ](../../../standard/assembly/index.md)
- [Imports ステートメント (.NET 名前空間および型)](../../language-reference/statements/imports-statement-net-namespace-and-type.md)
