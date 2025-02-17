---
title: Not 演算子 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Not
helpviewer_keywords:
- Boolean expressions, negating
- operators [Visual Basic], bitwise
- negation operator [Visual Basic]
- inverse bit values in variables [Visual Basic]
- bitwise operators [Visual Basic], NOT operator
- bitwise comparison [Visual Basic]
- Not operator [Visual Basic]
- logical negation
- operators [Visual Basic], negation
ms.assetid: 8f2ea83c-d2ed-480a-a474-3042a1cad9b5
ms.openlocfilehash: 29e2b159e4c6261a62e788b537102b9b457fe0c8
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69955830"
---
# <a name="not-operator-visual-basic"></a>Not 演算子 (Visual Basic)
`Boolean`式または数値式のビットごとの否定に対して論理否定を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
result = Not expression  
```  
  
## <a name="parts"></a>指定項目  
 `result`  
 必須。 `Boolean` Or 数値式。  
  
 `expression`  
 必須。 `Boolean` Or 数値式。  
  
## <a name="remarks"></a>Remarks  
 式`Boolean`の場合、次の表に`result` 、がどのように決定されるかを示します。  
  
|が`expression`の場合|の`result`値はです。|  
|------------------------|------------------------------|  
|`True`|`False`|  
|`False`|`True`|  
  
 数値式の場合、 `Not`演算子は任意の数値式のビット値を反転し、次の`result`表に従っての対応するビットを設定します。  
  
|の`expression`ビットがの場合|の`result`ビットはです。|  
|-------------------------------|----------------------------|  
|1|0|  
|0|1|  
  
> [!NOTE]
> 論理演算子とビット処理演算子は、他の算術演算子および関係演算子より優先順位が低いので、ビットごとの演算は、正確な実行を保証するためにかっこで囲む必要があります。  
  
## <a name="data-types"></a>データの種類  
 ブール否定の場合、結果のデータ型は`Boolean`になります。 ビットごとの否定の場合、結果の`expression`データ型はと同じになります。 ただし、expression が`Decimal`の場合、結果は`Long`になります。  
  
## <a name="overloading"></a>オーバーロード  
 演算子はオーバーロードできます。つまり、クラスまたは構造体がそのクラスまたは構造体の型を持つ場合に、クラスまたは構造体がその動作を再定義できます。 `Not` コードでこのようなクラスまたは構造体に対してこの演算子を使用する場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では`Not` 、演算子を使用して、 `Boolean`式に対して論理否定を実行します。 結果は、式`Boolean`の値の逆を表す値になります。  
  
 [!code-vb[VbVbalrOperators#33](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#33)]  
  
 前の例では、 `False`と`True`の結果がそれぞれ生成されます。  
  
## <a name="example"></a>例  
 次の例では`Not` 、演算子を使用して、数値式の個々のビットの論理否定を実行します。 結果パターンのビットは、オペランドパターンの対応するビットの逆順 (符号ビットを含む) に設定されます。  
  
 [!code-vb[VbVbalrOperators#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#34)]  
  
 前の例では、それぞれ–11、–9、および–7の結果が生成されます。  
  
## <a name="see-also"></a>関連項目

- [論理/ビット演算子 (Visual Basic)](../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)
- [Visual Basic における演算子の優先順位](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [機能別の演算子一覧](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [Visual Basic の論理演算子とビット処理演算子](../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)
