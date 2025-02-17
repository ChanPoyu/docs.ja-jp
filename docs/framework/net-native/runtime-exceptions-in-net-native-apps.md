---
title: .NET ネイティブ アプリでのランタイム例外
ms.date: 03/30/2017
ms.assetid: 5f050181-8fdd-4a4e-9d16-f84c22a88a97
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 27a2e0906343d115c47230c726efb74cd51d4c93
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049161"
---
# <a name="runtime-exceptions-in-net-native-apps"></a>.NET ネイティブ アプリでのランタイム例外
デバッグ構成とリリース構成は完全に異なるため、ターゲット プラットフォームでユニバーサル Windows プラットフォーム アプリのリリース ビルドをテストすることは重要です。 既定では、デバッグ構成は .NET Core ランタイムを使用してアプリをコンパイルしますが、リリース構成は .NET ネイティブを使用してアプリをネイティブ コードにコンパイルします。  
  
> [!IMPORTANT]
> アプリのリリースバージョンをテストするときに発生する可能性のある[MissingMetadataException](missingmetadataexception-class-net-native.md)、 [MissingInteropDataException](missinginteropdataexception-class-net-native.md)、および[誤 Singruntimeartifactexception](missingruntimeartifactexception-class-net-native.md)例外の処理については、「手順 4:例外の処理については、「[.NET ネイティブの概要](getting-started-with-net-native.md)」の「手順 4: メタデータの欠落を手動で解決」、さらに「[リフレクションおよび .NET ネイティブ](reflection-and-net-native.md)」と「[ランタイム ディレクティブ (rd.xml) 構成ファイル リファレンス](runtime-directives-rd-xml-configuration-file-reference.md)」を参照してください。  
  
## <a name="debug-and-release-builds"></a>デバッグ ビルドとリリース ビルド  
 .NET Core ランタイムに対してデバッグ ビルドを実行した場合は、ネイティブ コードにコンパイルされません。 このため、一般にランタイムによって提供されるすべてのサービスをアプリで使用することができます。  
  
 一方、リリース ビルドの場合は、パフォーマンスを最大化するために、ターゲット プラットフォーム用のネイティブ コードにコンパイルされ、外部のランタイムおよびライブラリに対する依存関係のほとんどが削除され、コードが大幅に最適化されます。  
  
 .NET ネイティブを使用してコンパイルされたリリース ビルドをデバッグする場合:  
  
- 通常の .NET デバッグ ツールとは異なる、.NET ネイティブのデバッグ エンジンを使用します。  
  
- 実行可能ファイルのサイズは、最大限削減されます。 .NET ネイティブが実行可能ファイルのサイズを削減する方法の 1 つは、ランタイムの例外メッセージを大幅にトリミングする方法です。これについては、「 [Runtime exception messages](#Messages) 」セクションでトピックとして詳細に説明しています。  
  
- コードは大幅に最適化されます。 つまり、できる限りインライン展開が使用されます。 (インライン展開により、コードは外部ルーチンから呼び出し元のルーチンに移動されます。) .NET ネイティブは特殊なランタイムを備えていて、積極的なインライン展開を実装するため、デバッグするときに表示される呼び出し履歴が影響を受けます。  詳細については、「 [Runtime call stack](#CallStack) 」を参照してください。  
  
> [!NOTE]
> **[.NET ネイティブ ツール チェーンを使用してコンパイルする]** ボックスをオンまたはオフにすることによって、デバッグ ビルドとリリース ビルドを .NET ネイティブ ツール チェーンでコンパイルするかどうかを制御できます。   ただし、Windows ストアは常に .NET ネイティブ ツールのチェーンを使用してアプリの製品バージョンをコンパイルすることに注意してください。  
  
<a name="Messages"></a>   
## <a name="runtime-exception-messages"></a>Runtime exception messages  
 アプリケーションの実行可能ファイルのサイズを最小限に抑えるために、.NET ネイティブは例外メッセージの全文を組み込みません。 そのため、リリース ビルドでスローされるランタイム例外では、例外メッセージの全文が表示されない場合があります。 代わりに、部分的な文字列を含むテキストが、詳細を示すリンクと共に表示される可能性があります。 たとえば、以下のような例外情報が表示されます。  
  
```output
Exception thrown: '$16_System.AggregateException' in Unknown Module.  
  
Additional information: AggregateException_ctor_DefaultMessage  
  
If there is a handler for this exception, the program may be safely continued.  
```  
  
 完全な例外メッセージが必要な場合は、代わりにデバッグ ビルドを実行します。 たとえば、リリース ビルドからの上記の例外情報は、デバッグ ビルドでは以下のように表示されます。  
  
```output
Exception thrown: 'System.AggregateException' in NativeApp.exe.  
  
Additional information: Value does not fall within the expected range.  
```  
  
<a name="CallStack"></a>   
## <a name="runtime-call-stack"></a>Runtime call stack  
 インライン展開および他の最適化のために、.NET ネイティブ ツール チェーンでコンパイルされたアプリで表示される呼び出し履歴では、ランタイム例外へのパスを明確に識別できない場合があります。  
  
 完全なスタックを取得するには、代わりにデバッグ ビルドを実行します。  
  
## <a name="see-also"></a>関連項目

- [Windows ユニバーサルアプリのデバッグ .NET ネイティブ](https://devblogs.microsoft.com/devops/debugging-net-native-windows-universal-apps/)
- [はじめに](getting-started-with-net-native.md)
