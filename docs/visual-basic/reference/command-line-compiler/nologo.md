---
title: -nologo (Visual Basic)
ms.date: 03/13/2018
helpviewer_keywords:
- -nologo compiler option [Visual Basic]
- banners [Visual Basic], suppressing startup
- nologo compiler option [Visual Basic]
- /nologo compiler option [Visual Basic]
ms.assetid: 25ef54b6-d676-4639-a2d2-a747a158bc07
ms.openlocfilehash: 07e1718554b158635b9d8b04958834e804e1fe9f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964377"
---
# <a name="-nologo-visual-basic"></a>-nologo (Visual Basic)
コンパイル中に著作権情報のバナーおよび情報メッセージを表示しません。  
  
## <a name="syntax"></a>構文  
  
```  
-nologo  
```  
  
## <a name="remarks"></a>Remarks  
 を指定`-nologo`した場合、コンパイラは著作権情報のバナーを表示しません。 既定では、`-nologo` は無効です。  
  
> [!NOTE]
> この`-nologo`オプションは、Visual Studio 開発環境内からは使用できません。コマンドラインからコンパイルする場合にのみ使用できます。  
  
## <a name="example"></a>例  
 次のコードは`T2.vb`コンパイルされ、著作権バナーは表示されません。  
  
```console
vbc -nologo t2.vb  
```  
  
## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](../../../visual-basic/reference/command-line-compiler/index.md)
- [コンパイル コマンド ラインのサンプル](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
