---
title: 軽減策:ポインター ベースのタッチおよびスタイラスのサポート
ms.date: 04/07/2017
helpviewer_keywords:
- retargeting changes
- .NET Framework 4.7 retargeting changes
- WPF retargeting changes
- WPF pointer-based touch and stylus stack
ms.assetid: f99126b5-c396-48f9-8233-8f36b4c9e717
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 67e41450ed69d73a4b27b0aa37974ae01be69687
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70779240"
---
# <a name="mitigation-pointer-based-touch-and-stylus-support"></a>軽減策:ポインター ベースのタッチおよびスタイラスのサポート

.NET Framework 4.7 を対象とし、Windows 10 Creators Update 以降の Windows システムで実行されている WPF アプリケーションは、オプションの `WM_POINTER` ベースの WPF タッチ/スタイラス スタックを有効にすることができます。

## <a name="impact"></a>影響

ポインター ベースのタッチ/スタイラス サポートを明示的に有効にしていない開発者は、WPF タッチ/スタイラス動作の変更を確認できません。

オプションの `WM_POINTER` ベースのタッチ/スタイラス スタックに関する現在の既知の問題を以下に示します。

- リアルタイム インクがサポートされない。

   インクとスタイラス プラグインがまだ機能している間は、UI スレッドで処理されますが、パフォーマンスの低下につながる可能性があります。

- プロモーションの変更により、タッチ/スタイラス イベントからマウス イベントに動作が変更される。

  - 操作の動作が異なる場合があります。

  - ドラッグ/ドロップでは、タッチ入力の適切なフィードバックが表示されません (これはスタイラス入力には影響しません)。

  - ドラッグ/ドロップは、タッチ/スタイラス イベントで開始できなくなりました。

      そのため、マウス入力が検出されるまで、アプリケーションが応答しなくなる可能性があります。 代わりに、開発者はマウス イベントからドラッグ アンド ドロップを開始する必要があります。

## <a name="opting-in-to-wm_pointer-based-touchstylus-support"></a>WM_POINTER ベースのタッチ/スタイラス サポートの有効化

このスタックを有効にする開発者は、アプリケーションの app.config ファイルに次の行を追加できます。

```xml
<configuration>
    <runtime>
        <AppContextSwitchOverrides value="Switch.System.Windows.Input.Stylus.EnablePointerSupport=true"/>
    </runtime>
</configuration>
```

このエントリを削除するか、その値を `false` に設定すると、このオプションのスタックがオフになります。

## <a name="see-also"></a>関連項目

- [.NET Framework 4.7 における再ターゲットの変更点](retargeting-changes-in-the-net-framework-4-7.md)
