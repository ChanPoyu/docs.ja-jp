---
title: 相互運用性 - C# プログラミング ガイド
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- COM interop
- interoperability
- platform invoke, accessing APIs with C#
- C# language, interoperability
ms.assetid: 238bb95a-e962-4026-bbd5-197055bdb8ee
ms.openlocfilehash: 896f89304289fd90c10da9aaa7ea15ada35ef8f7
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2019
ms.locfileid: "69589095"
---
# <a name="interoperability-c-programming-guide"></a>相互運用性 (C# プログラミング ガイド)
相互運用性は、アンマネージ コードへの既存の投資を保持して活用できるようにします。 共通言語ランタイム (CLR) の制御下で実行されるコードは*マネージド コード*と呼ばれ、CLR の外部で実行されるコードは*アンマネージド コード*と呼ばれます。 アンマネージ コードの例は、COM、COM +、C++ コンポーネント、ActiveX コンポーネント、および Microsoft Windows API です。  
  
 .NET Framework では、プラットフォーム呼び出しサービス、<xref:System.Runtime.InteropServices> 名前空間、C++ 相互運用性、および COM 相互運用性 (COM 相互運用機能) を通して、アンマネージ コードの相互運用を可能にしています。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [相互運用性の概要](./interoperability-overview.md)  
 C# のマネージド コードとアンマネージド コードの間で相互運用する方法について説明します。  
  
 [方法: Visual C# の機能を使用して Office 相互運用オブジェクトにアクセスする](./how-to-access-office-onterop-objects.md)  
 Office のプログラミングを容易にするために Visual C# に導入されている機能について説明します。  
  
 [方法: COM 相互運用機能を使用したプログラミングでインデックス付きプロパティを使用する](./how-to-use-indexed-properties-in-com-interop-rogramming.md)  
 インデックス付きプロパティを使用して、パラメーターを持つ COM プロパティにアクセスする方法について説明します。  
  
 [方法: プラットフォーム呼び出しを使用して Wave ファイルを再生する](./how-to-use-platform-invoke-to-play-a-wave-file.md)  
 プラットフォーム呼び出しサービスを使用して、Windows オペレーティング システム上の .wav サウンド ファイルを再生する方法について説明します。  
  
 [チュートリアル:Office プログラミング](./walkthrough-office-programming.md)  
 Excel ブックと、ブックへのリンクを含む Word 文書を作成する方法を示します。  
  
 [COM クラスの例](./example-com-class.md)  
 C# クラスを COM オブジェクトとして公開する方法を示します。  
  
## <a name="c-language-specification"></a>C# 言語仕様  

詳細については、「[C# 言語の仕様](../../language-reference/language-specification/index.md)」の「[基本概念](~/_csharplang/spec/unsafe-code.md)」を参照してください。 言語仕様は、C# の構文と使用法に関する信頼性のある情報源です。
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A?displayProperty=nameWithType>
- [C# プログラミング ガイド](../index.md)
- [アンマネージ コードとの相互運用](../../../framework/interop/index.md)
- [チュートリアル:Office プログラミング](./walkthrough-office-programming.md)
