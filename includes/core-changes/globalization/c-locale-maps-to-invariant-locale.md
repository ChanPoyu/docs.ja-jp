---
ms.openlocfilehash: 9e9e443be9ea51d214e95c676fc28f0d8790af8b
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117175"
---
### <a name="c-locale-maps-to-the-invariant-locale"></a>"C" ロケールは、インバリアント ロケールにマップされます

.NET Core 2.2 以前のバージョンでは、"C" ロケールを en_US_POSIX ロケールにマップする既定の ICU 動作に依存しています。 en_US_POSIX ロケールでは、大文字と小文字を区別しない文字列比較がサポートされていないため、望ましくない照合順序の動作があります。 一部の Linux ディストリビューションでは、"C" ロケールが既定のロケールとして設定されているため、ユーザーが予期しない動作が発生していました。 

#### <a name="details"></a>説明

.NET Core 3.0 以降では、"C" ロケール マッピングが en_US_POSIX ではなくインバリアント ロケールを使用するように変更されました。 一貫性を確保するため、インバリアントへの "C" ロケールのマッピングは、Windows にも適用されます。

en_US_POSIX では大文字と小文字を区別しない並べ替え/検索文字列操作がサポートされないため、"C" を en_US_POSIX カルチャにマッピングすると、お客様の混乱を招いていました。 "C" ロケールは一部の Linux ディストリビューションでは既定のロケールとして使用されているため、これらのオペレーティング システムでお客様にこのような望ましくない動作が発生していました。 

#### <a name="version-introduced"></a>導入されたバージョン

.NET Core 3.0

### <a name="recommended-action"></a>推奨される操作

この変更を認識する以外には特にありません。 この変更は、"C" ロケール マッピングを使用するアプリケーションにのみ影響します。

### <a name="category"></a>カテゴリ

グローバリゼーション 

### <a name="affected-apis"></a>影響を受ける API

すべての照合順序 API とカルチャ API は、この変更の影響を受けます。

<!--

-->
