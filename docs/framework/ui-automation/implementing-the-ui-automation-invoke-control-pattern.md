---
title: UI オートメーション Invoke コントロール パターンの実装
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, Invoke control pattern
- control patterns, Invoke
- Invoke control pattern
ms.assetid: e5b1e239-49f8-468e-bfec-1fba02ec9ac4
ms.openlocfilehash: e9815e4c2c0740f213632681200e48c8e4786657
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71043393"
---
# <a name="implementing-the-ui-automation-invoke-control-pattern"></a>UI オートメーション Invoke コントロール パターンの実装

> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 の最新情報[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]については[、「Windows Automation API:UI オートメーション](https://go.microsoft.com/fwlink/?LinkID=156746)。

このトピックでは、イベントおよびプロパティに関する情報など、 <xref:System.Windows.Automation.Provider.IInvokeProvider>の実装のためのガイドラインと規則について説明します。 その他のリファレンスへのリンクは、トピックの最後に記載します。

<xref:System.Windows.Automation.InvokePattern> コントロール パターンは、アクティブになったときに状態を保持せずに単一の明確なアクションを開始または実行するコントロールをサポートするために使用されます。 チェック ボックスやオプション ボタンなどの状態を保持するコントロールは、代わりに <xref:System.Windows.Automation.Provider.IToggleProvider> と <xref:System.Windows.Automation.Provider.ISelectionItemProvider> をそれぞれ実装する必要があります。 Invoke コントロール パターンを実装するコントロールの例については、「 [Control Pattern Mapping for UI Automation Clients](control-pattern-mapping-for-ui-automation-clients.md)」を参照してください。

<a name="Implementation_Guidelines_and_Conventions"></a>

## <a name="implementation-guidelines-and-conventions"></a>実装のガイドラインと規則

Invoke コントロール パターンを実装する場合は、次のガイドラインと規則に注意してください。

- 別のコントロール パターン プロバイダーを通じて同じ動作が公開されていない場合、コントロールは <xref:System.Windows.Automation.Provider.IInvokeProvider> を実装します。 たとえば、コントロールの <xref:System.Windows.Automation.InvokePattern.Invoke%2A> メソッドが <xref:System.Windows.Automation.ExpandCollapsePattern.Expand%2A> メソッドまたは <xref:System.Windows.Automation.ExpandCollapsePattern.Collapse%2A> メソッドと同じ処理を実行する場合、コントロールに <xref:System.Windows.Automation.Provider.IInvokeProvider>を実装しないようにします。

- 通常、コントロールの呼び出しは、クリックまたはダブルクリックするか、Enter キー、定義済みのキーボード ショートカット、または何らかの代替的なキーの組み合わせを押すことによって実行されます。

- (関連付けられたアクションを実行したコントロールへの応答として) アクティブ化されたコントロールで<xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent> が生成されます。 可能な場合は、コントロールがアクションを完了し、ブロックせずに戻った後に、イベントを生成する必要があります。 次のシナリオでは、Invoke 要求を処理する前に Invoked イベントを生成する必要があります。

  - 処理が完了するまで待機することが不可能または非現実的である。

  - 処理にユーザー操作が必要になる。

  - アクションに時間がかかり、呼び出し側のクライアントを長時間ブロックする。

- コントロールの呼び出しに大きな副作用が伴う場合は、その副作用を、 <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.HelpText%2A> プロパティを介して公開する必要があります。 たとえば、 <xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A> が選択に関連付けられていない場合でも、 <xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A> によって別のコントロールが選択された状態になることがあります。

- ホバー (マウス オーバー) 効果は、一般に Invoked イベントを発生させません。 ただし、ホバー状態に基づいて (視覚効果を発生させることなく) アクションを実行するコントロールは、 <xref:System.Windows.Automation.InvokePattern> コントロール パターンをサポートする必要があります。

> [!NOTE]
> マウス関連の副作用の結果として呼び出す以外にコントロールを呼び出す方法がない場合、そのような実装はユーザー補助に問題があるものと見なされます。

- コントロールの呼び出しは、項目の選択とは異なります。 ただし、コントロールによっては、その呼び出しの副作用として、項目が選択された状態になることがあります。 たとえば、My Documents フォルダー内にある [!INCLUDE[TLA#tla_word](../../../includes/tlasharptla-word-md.md)] ドキュメントのリスト項目を呼び出すと、その項目が選択され、ドキュメントが開きます。

- 要素は、呼び出されるとすぐに [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーから消える場合があります。 そのため、イベント コールバックで提供された要素に情報を要求すると失敗することがあります。 推奨される回避策は、キャッシュされた情報をプリフェッチすることです。

- コントロールは、複数のコントロール パターンを実装できます。 たとえば、 [!INCLUDE[TLA#tla_xl](../../../includes/tlasharptla-xl-md.md)] ツール バーの [塗りつぶしの色] コントロールは、 <xref:System.Windows.Automation.InvokePattern> コントロール パターンと <xref:System.Windows.Automation.ExpandCollapsePattern> コントロール パターンを実装しています。 <xref:System.Windows.Automation.ExpandCollapsePattern> はメニューを公開し、 <xref:System.Windows.Automation.InvokePattern> は選択された色でアクティブな選択内容を塗りつぶします。

<a name="Required_Members_for_the_IValueProvider_Interface"></a>

## <a name="required-members-for-iinvokeprovider"></a>IInvokeProvider の必須メンバー

<xref:System.Windows.Automation.Provider.IInvokeProvider>の実装には、次のプロパティとメソッドが必要です。

|必須メンバー|メンバーの型|メモ|
|----------------------|-----------------|-----------|
|<xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A>|メソッド|<xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A> は非同期呼び出しであるため、クライアントをブロックせずに即座に戻る必要があります。<br /><br /> 呼び出されたときにモーダル ダイアログを直接的または間接的に表示するコントロールでは、この動作は特に重要です。 イベントを発生させたすべての UI オートメーション クライアントは、モーダル ダイアログが閉じられるまで、ブロックされたままになります。|

<a name="Exceptions"></a>

## <a name="exceptions"></a>例外

プロバイダーは、次の例外をスローする必要があります。

|例外の種類|条件|
|--------------------|---------------|
|<xref:System.Windows.Automation.ElementNotEnabledException>|コントロールが有効ではない。|

## <a name="see-also"></a>関連項目

- [UI Automation コントロール パターンの概要](ui-automation-control-patterns-overview.md)
- [UI オートメーション プロバイダーでのコントロール パターンのサポート](support-control-patterns-in-a-ui-automation-provider.md)
- [クライアントの UI オートメーション コントロール パターン](ui-automation-control-patterns-for-clients.md)
- [UI オートメーションを使用したコントロールの呼び出し](invoke-a-control-using-ui-automation.md)
- [UI Automation ツリーの概要](ui-automation-tree-overview.md)
- [UI オートメーションにおけるキャッシュの使用](use-caching-in-ui-automation.md)
