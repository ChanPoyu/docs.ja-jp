---
title: 'アセンブリ マニフェストを作成中にエラーが発生しました : <error message>'
ms.date: 07/20/2015
f1_keywords:
- bc30140
- vbc30140
helpviewer_keywords:
- BC30140
ms.assetid: 1beb5aa0-7b79-4c85-946b-5c2d0a41d1d2
ms.openlocfilehash: 560635718a931cc9cdb687154a1d23970136de97
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972287"
---
# <a name="error-creating-assembly-manifest-error-message"></a>アセンブリマニフェスト作成時の\<エラー: エラーメッセージ >
Visual Basic コンパイラは、アセンブリリンカー (Al.exe、Alink とも呼ばれます) を呼び出して、マニフェストを持つアセンブリを生成します。 リンカーが、アセンブリの生成前の段階でのエラーを報告しています。  
  
 指定したキー ファイルまたはキー コンテナーに原因がある場合があります。 アセンブリに完全署名するには、公開キーと秘密キーに関する情報を含む有効なキー ファイルを提供する必要があります。 アセンブリに遅延署名するには、 **[遅延署名のみ]** チェック ボックスをオンにし、公開キー情報を含む有効なキー ファイルを提供する必要があります。 アセンブリに遅延署名する場合、秘密キーは必要ありません。 詳細については、「[方法 :厳密な名前でアセンブリに署名する](../../../standard/assembly/sign-strong-name.md)」を参照してください。  
  
 **エラー ID:** BC30140  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. 引用符で囲まれたエラーメッセージを調べ、「 [al.exe](../../../framework/tools/al-exe-assembly-linker.md)」を参照してください。 エラー AL1019 の詳細な説明とアドバイス  
  
2. エラーが続く場合は、状況に関する情報を収集し、マイクロソフト プロダクト サポート サービスに通知してください。  
  
## <a name="see-also"></a>関連項目

- [方法: 厳密な名前でアセンブリに署名する](../../../standard/assembly/sign-strong-name.md)
- [[署名] ページ (プロジェクト デザイナー)](/visualstudio/ide/reference/signing-page-project-designer)
- [Al.exe](../../../framework/tools/al-exe-assembly-linker.md)
- [ご意見](/visualstudio/ide/talk-to-us)
