---
title: アセンブリと side-by-side 実行
ms.date: 08/20/2019
helpviewer_keywords:
- side-by-side execution [.NET Framework]
- assemblies [.NET Framework], side-by-side execution
ms.assetid: e42036ee-7590-47d1-b884-cc856e39bd5d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d4f246108768dcebf51348f67c4523cb83df4f9d
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053976"
---
# <a name="assemblies-and-side-by-side-execution"></a>アセンブリと side-by-side 実行

side-by-side 実行は、アプリケーションやコンポーネントの複数のバージョンを同じコンピューターに格納して実行する機能です。 つまり、ランタイムの複数のバージョンと、特定のバージョンのランタイムを使用するアプリケーションおよびコンポーネントの複数のバージョンを、同一コンピューター上に共存させることができます。 side-by-side 実行によって、アプリケーションをバインドするコンポーネントのバージョンや、アプリケーションが使用するランタイムのバージョンを細かく制御できます。  
  
同じアセンブリの異なるバージョンの side-by-side ストレージにおける side-by-side 実行のサポートは、厳密な名前には不可欠の要素であり、ランタイムのインフラストラクチャに組み込まれています。 厳密な名前を持つアセンブリのバージョン番号がその識別子の一部に含まれているため、ランタイムは同じアセンブリの複数のバージョンをグローバル アセンブリ キャッシュに格納し、実行時にこれらのアセンブリを読み込むことができます。  
  
ランタイムは、side-by-side 実行できるアプリケーションの作成機能を提供しますが、side-by-side 実行は自動的にサポートされるわけではありません。 side-by-side 実行できるアプリケーションの作成に関する詳細については、「[side-by-side 実行用のコンポーネントを作成するためのガイドライン](../../framework/deployment/guidelines-for-creating-components-for-side-by-side-execution.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [ランタイムがアセンブリを検索する方法](../../framework/deployment/how-the-runtime-locates-assemblies.md)
- [.NET のアセンブリ](index.md)
