---
title: < < 演算子 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.<<
helpviewer_keywords:
- bit shift operators [Visual Basic]
- << operator [Visual Basic]
- operator <<, Visual Basic left shift operator
ms.assetid: fdb93d25-81ba-417f-b808-41207bfb8440
ms.openlocfilehash: d6b186ad519bcd7cf82cce12523f2d75e09317cc
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69966886"
---
# <a name="-operator-visual-basic"></a>\<\<演算子 (Visual Basic)
ビットパターンに対して算術左シフトを実行します。  
  
## <a name="syntax"></a>構文  
  
```  
result = pattern << amount  
```  
  
## <a name="parts"></a>指定項目  
 `result`  
 必須。 整数の数値。 ビットパターンをシフトした結果。 データ型は、の`pattern`データ型と同じです。  
  
 `pattern`  
 必須。 整数の数値式。 シフトされるビットパターン。 データ`SByte`型は、整数型 ( `UShort` `Short`、 `Byte`、、 `Integer` `UInteger` `ULong`、、、、または) である必要があります。 `Long`  
  
 `amount`  
 必須。 数値式。 ビットパターンをシフトするビット数。 データ型は、 `Integer`またはに`Integer`拡大変換する必要があります。  
  
## <a name="remarks"></a>Remarks  
 算術シフトは循環していません。つまり、結果の一方の端からシフトされたビットはもう一方の端には再入されません。 算術左シフトでは、結果のデータ型の範囲を超えてシフトされたビットは破棄され、右側に空いているビット位置は0に設定されます。  
  
 結果よりも多くのビットでシフトを防止するために、Visual Basic はのデータ`amount` `pattern`型に対応するサイズマスクを使用しての値をマスクします。 これらの値のバイナリとは、シフトの量に使用されます。 サイズマスクは次のとおりです。  
  
|のデータ型`pattern`|サイズマスク (10 進数)|サイズマスク (16 進数)|  
|----------------------------|---------------------------|-------------------------------|  
|`SByte`, `Byte`|7|& H00000007|  
|`Short`, `UShort`|16|& H0000000F|  
|`Integer`, `UInteger`|31|& H0000001F|  
|`Long`, `ULong`|63|& H0000003F|  
  
 が`amount` 0 の場合、の`result`値はの`pattern`値と同じです。 が`amount`負の場合は、符号なしの値として取得され、適切なサイズマスクでマスクされます。  
  
 算術シフトではオーバーフロー例外は生成されません。  
  
> [!NOTE]
> 演算子はオーバーロードできます。つまり、クラスまたは構造体がそのクラスまたは構造体の型を持つ場合に、クラスまたは構造体がその動作を再定義できます。 `<<` コードでこのようなクラスまたは構造体に対してこの演算子を使用する場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では`<<` 、演算子を使用して、整数値に対する算術左シフトを実行します。 結果は、シフトする式と同じデータ型になります。  
  
 [!code-vb[VbVbalrOperators#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#12)]  
  
 前の例の結果は次のようになります。  
  
- `result1`は 192 (0000 0000 1100 0000) です。  
  
- `result2`は 3072 (0000 1100 0000 0000) です。  
  
- `result3`は-32768 (1000 0000 0000 0000) です。  
  
- `result4`は 384 (0000 0001 1000 0000) です。  
  
- `result5`が 0 (左に15桁に移動) です。  
  
 の`result4`シフト量は、1に等しい17と15として計算されます。  
  
## <a name="see-also"></a>関連項目

- [ビット シフト演算子](../../../visual-basic/language-reference/operators/bit-shift-operators.md)
- [代入演算子](../../../visual-basic/language-reference/operators/assignment-operators.md)
- [<<= 演算子](../../../visual-basic/language-reference/operators/left-shift-assignment-operator.md)
- [Visual Basic における演算子の優先順位](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [機能別の演算子一覧](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [Visual Basic の算術演算子](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
