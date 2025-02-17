---
title: アセンブリの場所
ms.date: 08/20/2019
helpviewer_keywords:
- locating assemblies
- assemblies [.NET Framework], location
ms.assetid: 9f1f41a7-2954-49d3-a2c0-62b6ef4d40ab
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6427f7d005c43ef9e83387e865f71009b683a7c4
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972655"
---
# <a name="assembly-location"></a>アセンブリの場所
アセンブリの場所は、参照時に共通言語ランタイムがそれを見つけることができるかどうかを決定します。また、アセンブリをその他のアセンブリと共有できるかどうかも決定できます。 次の場所にアセンブリを展開することができます。  
  
- アプリケーションのディレクトリまたはサブディレクトリ  
  
     これは、アセンブリを展開する最も一般的な場所です。 アプリケーションのルート ディレクトリのサブディレクトリは、言語またはカルチャを基にすることができます。 アセンブリにカルチャ属性の情報がある場合は、アプリケーション ディレクトリの下のサブディレクトリに、そのカルチャの名前で存在する必要があります。  
  
- グローバル アセンブリ キャッシュ  
  
     これは、共通言語ランタイムをインストールしている場所にインストールされている、コンピューター全体で使用できるコード キャッシュです。 ほとんどの場合、あるアセンブリを複数のアプリケーションで共有する場合は、そのアセンブリをグローバル アセンブリ キャッシュ内に展開する必要があります。  
  
- HTTP サーバー上  
  
     HTTP サーバーに展開されているアセンブリは、厳密な名前を持つ必要があります。アプリケーションの構成ファイルのコードベース セクションにあるアセンブリをポイントします。  
  
## <a name="see-also"></a>関連項目

- [アセンブリを作成する](create.md)
- [グローバル アセンブリ キャッシュ](../../framework/app-domains/gac.md)
- [ランタイムがアセンブリを検索する方法](../../framework/deployment/how-the-runtime-locates-assemblies.md)
- [アセンブリを使用したプログラム](program.md)
