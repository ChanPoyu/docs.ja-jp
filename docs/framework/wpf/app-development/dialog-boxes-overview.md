---
title: ダイアログ ボックスの概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- modeless dialog boxes [WPF]
- dialog boxes [WPF]
- message boxes [WPF]
- modal dialog boxes [WPF]
ms.assetid: 0d23d544-a393-4a02-a3aa-d8cd5d3d6511
ms.openlocfilehash: bf4617d838ba7f02523d7bbdbb57932c033f4a9e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69958673"
---
# <a name="dialog-boxes-overview"></a>ダイアログボックスの概要
スタンドアロンアプリケーションには、通常、アプリケーションが動作するメインデータを表示し、メニューバー、ツールバー、ステータスバーなど[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]のメカニズムを使用してデータを処理する機能を公開するメインウィンドウがあります。 重要なアプリケーションは、次のようなことをするための追加のウィンドウを表示することもあります。  
  
- 固有の情報をユーザーに表示する。  
  
- ユーザーから情報を収集する。  
  
- 情報の表示と収集の両方を行う。  
  
 これらの種類のウィンドウと呼ばれる *ダイアログ ボックス*、し、2 種類があります: モーダルとモードレスです。  
  
 関数でユーザーに追加のデータが必要な場合は、関数によって*モーダル*ダイアログボックスが表示されます。 機能は、モーダル ダイアログ ボックスに依存してデータを収集するため、モーダル ダイアログ ボックスが開いている間、ユーザーはアプリケーション内の他のウィンドウをアクティブ化することはできません。 ほとんどの場合、モーダルダイアログボックスを使用すると、 **[OK** ] または **[キャンセル**] をクリックしてモーダルダイアログボックスが終了したときにユーザーに通知できます。 **[OK** ] ボタンを押すと、ユーザーがデータを入力し、そのデータでの処理を続行するように求められます。 **[キャンセル**] ボタンを押すと、ユーザーが関数の実行を完全に停止することを指定します。 モーダル ダイアログ ボックスの最も一般的な例は、データを開く、保存する、および印刷するために表示されます。  
  
 一方、*モードレス*ダイアログボックスでは、ユーザーが開いている間に他のウィンドウをアクティブ化することはできません。 たとえば、ユーザーがドキュメント内の特定の単語の出現箇所を検索する場合、メイン ウィンドウは、多くの場合、ダイアログ ボックスを開いて、検索する単語をユーザーに尋ねます。 しかし、単語の検索中もユーザーはドキュメントを編集できるため、ダイアログ ボックスがモーダルである必要はありません。 モードレスダイアログボックスには、ダイアログボックスを閉じるための **[閉じる]** ボタンが用意されています。また、次を **[検索]** ボタンをクリックして、単語検索の検索条件に一致する次の単語を検索するなど、特定の機能を実行するためのボタンを追加することもできます。  
  
 Windows Presentation Foundation (WPF) を使用すると、メッセージボックス、コモンダイアログボックス、カスタムダイアログボックスなど、いくつかの種類のダイアログボックスを作成できます。 このトピックでは、それぞれについて説明し、[ダイアログボックスのサンプル](https://go.microsoft.com/fwlink/?LinkID=159984)で一致例を示します。  

<a name="Message_Boxes"></a>   
## <a name="message-boxes"></a>メッセージボックス  
 *メッセージボックス*は、テキスト情報を表示したり、ユーザーがボタンを使用して判断したりできるようにするためのダイアログボックスです。 次の図は、テキスト情報と質問を表示して、ユーザーが質問に回答するための 3 つのボタンを表示するメッセージ ボックスを示しています。  
  
 ![アプリケーションを閉じる前にドキュメントに変更を保存するかどうかを確認する [ワードプロセッサ] ダイアログボックス。](./media/dialog-boxes-overview/word-processor-dialog.png)  
  
 メッセージボックスを作成するには<xref:System.Windows.MessageBox> 、クラスを使用します。 <xref:System.Windows.MessageBox>では、次のようなコードを使用して、メッセージボックスのテキスト、タイトル、アイコン、およびボタンを構成できます。  
  
 [!code-csharp[DialogBoxesOverviewSnippets#MsgBoxConfigureCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/CSharp/Window1.xaml.cs#msgboxconfigurecodebehind)]
 [!code-vb[DialogBoxesOverviewSnippets#MsgBoxConfigureCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/VisualBasic/window1.xaml.vb#msgboxconfigurecodebehind)]  
  
 メッセージボックスを表示するには、次`static`のコードに示すように、 <xref:System.Windows.MessageBox.Show%2A>メソッドを呼び出します。  
  
 [!code-csharp[DialogBoxesOverviewSnippets#MsgBoxShowCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/CSharp/Window1.xaml.cs#msgboxshowcodebehind)]
 [!code-vb[DialogBoxesOverviewSnippets#MsgBoxShowCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/VisualBasic/window1.xaml.vb#msgboxshowcodebehind)]  
  
 メッセージ ボックスを表示するコードで、ユーザーの決定 (どのボタンが押されたか) を検出して処理する必要があるときには、コードは、次のコードに示されているように、メッセージ ボックスの結果を検査できます。  
  
 [!code-csharp[DialogBoxesOverviewSnippets#MsgBoxShowAndResultCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/CSharp/Window1.xaml.cs#msgboxshowandresultcodebehind1)]
 [!code-vb[DialogBoxesOverviewSnippets#MsgBoxShowAndResultCODEBEHIND1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/VisualBasic/window1.xaml.vb#msgboxshowandresultcodebehind1)]  
  
 メッセージボックスの使用方法の詳細につい<xref:System.Windows.MessageBox>ては、「」、「 [MessageBox サンプル](https://go.microsoft.com/fwlink/?LinkID=160023)」、および「[ダイアログボックスのサンプル](https://go.microsoft.com/fwlink/?LinkID=159984)」を参照してください。  
  
 では、簡単なダイアログボックスのユーザーエクスペリエンスが提供される<xref:System.Windows.MessageBox> 場合がありますが、を使用する利点は、部分信頼セキュリティサンドボックス内で実行されるアプリケーションで表示できる唯一の種類のウィンドウです(「[セキュリティ](../security-wpf.md)」を参照してください<xref:System.Windows.MessageBox>)。 [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)].  
  
 ほとんどのダイアログ ボックスは、テキスト、選択 (チェック ボックス)、相互に排他的な選択 (オプション ボタン)、リスト選択 (リスト ボックス、コンボ ボックス、ドロップダウン リスト ボックス) など、メッセージ ボックスの結果よりも複雑なデータを表示し、収集します。 これらの場合、Windows Presentation Foundation (WPF) にはいくつかの一般的なダイアログボックスが用意されており、独自のダイアログボックスを作成することができます。ただし、どちらの方法も、完全信頼で実行されるアプリケーションに限定されます。  
  
<a name="Common_Dialogs"></a>   
## <a name="common-dialog-boxes"></a>コモンダイアログボックス  
 Windows には、ファイルを開く、ファイルを保存する、印刷するためのダイアログボックスなど、すべてのアプリケーションに共通の再利用可能なダイアログボックスが実装されています。 これらのダイアログ ボックスはオペレーティング システムによって実装されるため、そのオペレーティング システム上で実行するすべてのアプリケーション間で共有でき、ユーザー エクスペリエンスの一貫性を保つことができます。ユーザーが 1 つのアプリケーションで、オペレーティング システムによって提供されるダイアログ ボックスの使用に慣れると、他のアプリケーションでも、そのダイアログ ボックスの使用法を学ぶ必要はありません。 これらのダイアログボックスはすべてのアプリケーションで使用でき、一貫性のあるユーザーエクスペリエンスを提供するのに役立つため、*コモンダイアログボックス*と呼ばれています。  
  
 Windows Presentation Foundation (WPF) は、[ファイルを開く]、[ファイルの保存]、および [印刷] コモンダイアログボックスをカプセル化し、スタンドアロンアプリケーションで使用するためのマネージクラスとして公開します。 このトピックでは、それぞれの概要を簡単に説明します。  
  
<a name="Open_File_Dialog"></a>   
### <a name="open-file-dialog"></a>ファイルを開くダイアログ  
 [ファイルを開く] ダイアログ ボックスは、次の図に示されているように、開くファイルの名前を取得するために、ファイルを開く機能によって使用されます。  
  
 ![ファイルを取得する場所を示す、開いているダイアログボックス。](./media/dialog-boxes-overview/open-file-dialog-box.png)  
  
 共通の [ファイルを開く] ダイアログボックスは<xref:Microsoft.Win32.OpenFileDialog> 、クラスとして実装<xref:Microsoft.Win32>され、名前空間に配置されます。 次のコードは、[ファイルを開く] ダイアログ ボックスの作成、構成、および表示の方法と、結果を処理する方法を示しています。  
  
 [!code-csharp[DialogBoxesOverviewSnippets#OpenFileDialogBoxCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/CSharp/Window1.xaml.cs#openfiledialogboxcodebehind)]
 [!code-vb[DialogBoxesOverviewSnippets#OpenFileDialogBoxCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/VisualBasic/window1.xaml.vb#openfiledialogboxcodebehind)]  
  
 [ファイルを開く] ダイアログボックスの詳細につい<xref:Microsoft.Win32.OpenFileDialog?displayProperty=nameWithType>ては、「」を参照してください。  
  
> [!NOTE]
> <xref:Microsoft.Win32.OpenFileDialog>部分信頼で実行されているアプリケーションによってファイル名を安全に取得するために使用できます (「[セキュリティ](../security-wpf.md)」を参照してください)。  
  
<a name="Save_File_Dialog"></a>   
### <a name="save-file-dialog-box"></a>[ファイルの保存] ダイアログ ボックス  
 [ファイルの保存] ダイアログ ボックスは、次の図に示されているように、保存するファイルの名前を取得するために、ファイルを保存する機能によって使用されます。  
  
 ![ファイルを保存する場所を示す [名前を付けて保存] ダイアログボックス。](./media/dialog-boxes-overview/save-file-dialog-box.png)  
  
 共通の [ファイルの保存] ダイアログボックスは<xref:Microsoft.Win32.SaveFileDialog>クラスとして実装され<xref:Microsoft.Win32> 、名前空間にあります。 次のコードは、[ファイルを開く] ダイアログ ボックスの作成、構成、および表示の方法と、結果を処理する方法を示しています。  
  
 [!code-csharp[DialogBoxesOverviewSnippets#SaveFileDialogBoxCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/CSharp/Window1.xaml.cs#savefiledialogboxcodebehind)]
 [!code-vb[DialogBoxesOverviewSnippets#SaveFileDialogBoxCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/VisualBasic/window1.xaml.vb#savefiledialogboxcodebehind)]  
  
 [ファイルの保存] ダイアログボックスの詳細につい<xref:Microsoft.Win32.SaveFileDialog?displayProperty=nameWithType>ては、「」を参照してください。  
  
<a name="Print_Dialog"></a>   
### <a name="print-dialog-box"></a>[印刷] ダイアログ ボックス

次の図に示されているように、[印刷] ダイアログ ボックスは、ユーザーがデータを印刷するプリンターを選択し、構成するために、印刷機能によって使用されます。  
  
![[印刷] ダイアログボックスを表示するスクリーンショット。](./media/dialog-boxes-overview/print-data-dialog-box.png)  
  
共通の [印刷] ダイアログボックスは<xref:System.Windows.Controls.PrintDialog>クラスとして実装され、 <xref:System.Windows.Controls>名前空間にあります。 次のコードは、[印刷] ダイアログ ボックスの作成、構成、および表示の方法を示しています。  
  
 [!code-csharp[DialogBoxesOverviewSnippets#PrintDialogBoxCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/CSharp/Window1.xaml.cs#printdialogboxcodebehind)]
 [!code-vb[DialogBoxesOverviewSnippets#PrintDialogBoxCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/VisualBasic/window1.xaml.vb#printdialogboxcodebehind)]  
  
 [印刷] ダイアログボックスの詳細について<xref:System.Windows.Controls.PrintDialog?displayProperty=nameWithType>は、「」を参照してください。 WPF での印刷の詳細については、「[印刷の概要](../advanced/printing-overview.md)」を参照してください。  
  
<a name="Custom_Dialog_Boxes"></a>   
## <a name="custom-dialog-boxes"></a>カスタムダイアログボックス

コモン ダイアログ ボックスは便利であり、可能なときにはコモン ダイアログ ボックスを使用する必要がありますが、ドメイン固有のダイアログ ボックスの要件はサポートしていません。 このような場合は、独自のダイアログ ボックスを作成する必要があります。 これから説明するように、ダイアログ ボックスは、特殊な動作を持つウィンドウです。 <xref:System.Windows.Window>これらの動作を実装します。したがっ<xref:System.Windows.Window>て、を使用して、カスタムモーダルダイアログボックスとモードレスダイアログボックスを作成します。  
  
<a name="Creating_a_Modal_Custom_Dialog_Box"></a>   
### <a name="creating-a-modal-custom-dialog-box"></a>モーダルカスタムダイアログボックスの作成

このトピックでは、を<xref:System.Windows.Window>使用して、ダイアログボックスを例として`Margins`使用し、一般的なモーダルダイアログボックスの実装を作成する方法について説明します (「[ダイアログボックスのサンプル](https://go.microsoft.com/fwlink/?LinkID=159984)」を参照してください)。 `Margins`ダイアログボックスを次の図に示します。  
  
 ![左余白、上余白、右余白、および下余白を定義するフィールドを含む [余白] ダイアログボックス。](./media/dialog-boxes-overview/margin-size-dialog-box.png)  
  
#### <a name="configuring-a-modal-dialog-box"></a>モーダルダイアログボックスの構成

一般的なダイアログ ボックスのユーザー インターフェイスには、次の項目が含まれます。  
  
- 必要なデータを収集するために必要なさまざまなコントロール。  
  
- **[OK]** ボタンをクリックすると、ダイアログボックスが閉じられ、関数に戻り、処理が続行されます。  
  
- **[キャンセル]** ボタン。このボタンをクリックすると、ダイアログボックスが閉じ、関数をさらに処理できなくなります。  
  
- タイトルバーの **[閉じる]** ボタン。  
  
- アイコン。  
  
- **[最小化]** 、 **[最大化]** 、 **[元に戻す]** ボタン。  
  
- ダイアログボックスを最小化、最大化、復元、および閉じるための**システム**メニュー。  
  
- ダイアログボックスを開いたウィンドウの中央にあるおよびの上の位置。  
  
- 可能な場合は、ダイアログボックスが小さすぎないようにサイズを変更できるようにし、ユーザーに便利な既定サイズを提供します。 そのためには、既定のディメンションと最小ディメンションの両方を設定する必要があります。  
  
- ESC キーをキーボードショートカットとして使用すると、 **[キャンセル**] ボタンが押されます。 これを行うには、 <xref:System.Windows.Controls.Button.IsCancel%2A> **[キャンセル**] ボタンのプロパティ`true`をに設定します。  
  
- ENTER (または RETURN) キーをキーボードショートカットとして押すと、 **[OK** ] ボタンが押されます。 これを行うには、 <xref:System.Windows.Controls.Button.IsDefault%2A> **[OK** ] ボタン`true`のプロパティを設定します。  
  
次のコードは、この構成の例を示しています。  
  
[!code-xaml[MarginsDialogBox XAML file](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginsDialogBox.xaml?range=1-16,106-112)]  

[!code-csharp[MarginsDialogBox C# code-behind](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginsDialogBox.xaml.cs?range=1-12,67-68)]
[!code-vb[MarginsDialogBox VB code-behind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MarginsDialogBox.xaml.vb?range=1-11,61-62)]  
  
ダイアログ ボックスのユーザー エクスペリエンスは、ダイアログ ボックスを開くウィンドウのメニュー バーにも及びます。 メニュー項目が、機能の続行には、ダイアログ ボックスでのユーザーの操作を必要とする機能を実行するときには、次に示されているように、その機能のメニュー項目の見出しに省略記号を付けます。  
  
[!code-xaml[Menu bar of MainWindow.Xaml file](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MainWindow.xaml#L26-L27)]  
  
メニュー項目が、[バージョン情報] ダイアログ ボックスなど、ユーザーの操作を必要としないダイアログ ボックスを表示する機能を実行するときには、省略記号は必要ありません。  
  
#### <a name="opening-a-modal-dialog-box"></a>モーダルダイアログボックスを開く

ダイアログ ボックスは、通常、ワード プロセッサでドキュメントの余白を設定するなど、ドメイン固有の機能を実行するためにユーザーがメニュー項目を選択した結果として表示されます。 ウィンドウをダイアログ ボックスとして表示するのは、通常のウィンドウを表示するのと同様ですが、ダイアログ ボックス固有の追加の構成が必要です。 ダイアログ ボックスのインスタンス化、構成、および開くプロセスの全体を、次のコードに示します。  
  
[!code-csharp[Opening a modal dialog box](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MainWindow.xaml.cs?range=1-11,78-88,193-195)]
[!code-vb[Opening a modal dialog box](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MainWindow.xaml.vb?range=1-9,58-67,130-132)]  

ここでは、このコードによって、既定の情報 (現在の余白) がダイアログボックスに渡されます。 また、ダイアログボックス<xref:System.Windows.Window.Owner%2A?displayProperty=nameWithType>を表示しているウィンドウへの参照をプロパティに設定します。 一般に、すべてのダイアログ ボックスに共通するウィンドウの状態関連動作を提供するために、ダイアログ ボックスの所有者を必ず設定する必要があります (詳細については、「[WPF ウィンドウの概要](wpf-windows-overview.md)」を参照してください)。

> [!NOTE]
> ダイアログボックスのユーザーインターフェイス (UI) オートメーションをサポートするには、所有者を指定する必要があります (「 [Ui オートメーションの概要](../../ui-automation/ui-automation-overview.md)」を参照してください)。

ダイアログボックスが構成された後は、 <xref:System.Windows.Window.ShowDialog%2A>メソッドを呼び出すことによってモーダルとして表示されます。  
  
#### <a name="validating-user-provided-data"></a>ユーザー指定のデータの検証

ダイアログ ボックスが開かれ、ユーザーが必要なデータを指定すると、ダイアログ ボックスは、指定されたデータが有効であることを確認する必要があります。これは、次のような理由からです。  
  
- セキュリティの観点から、すべての入力を検証する必要があります。  
  
- ドメイン固有の観点から、データの検証は、誤ったデータがコードによって処理されて、例外がスローされるのを防ぎます。  
  
- ユーザー エクスペリエンスの観点から、ダイアログ ボックスは、入力したデータが無効であることを示すことによって、ユーザーを支援できます。  
  
- パフォーマンスの観点から、多層アプリケーションでのデータの検証は、特に、アプリケーションが Web サービスまたはサーバーベースのデータベースで構成される場合、クライアント層とアプリケーション層の間のラウンド トリップの回数を減らすことができます。  

WPF でバインドされたコントロールを検証するには、検証規則を定義し、バインディングに関連付ける必要があります。 検証規則は、から<xref:System.Windows.Controls.ValidationRule>派生するカスタムクラスです。 次の例は、バインドされ`MarginValidationRule`た値<xref:System.Double>がで、指定した範囲内にあることを確認する検証規則を示しています。  

[!code-csharp[Margin validation rules](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginValidationRule.cs)]
[!code-vb[Margin validation rules](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MarginValidationRule.vb)]  

このコードでは、検証規則の検証ロジックは、データを検証し<xref:System.Windows.Controls.ValidationRule.Validate%2A>て適切<xref:System.Windows.Controls.ValidationResult>なを返すメソッドをオーバーライドすることによって実装されます。  

検証規則をバインド コントロールに関連付けるには、次のマークアップを使用します。  
  
[!code-xaml[Associating a validation rule with a control](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginsDialogBox.xaml?range=1-16,57-68,111-112)]

検証規則が関連付けられると、バインドされたコントロールにデータが入力されると、WPF は自動的にそれを適用します。 コントロールに無効なデータが含まれている場合、WPF では、次の図に示すように、無効なコントロールの周囲に赤い枠線が表示されます。  
  
![[余白] ダイアログボックス。無効な左余白の値の周囲に赤い枠線が付きます。](./media/dialog-boxes-overview/invalid-left-margin-dialog.png)  

WPF では、有効なデータを入力しない限り、ユーザーは無効なコントロールに制限されません。 これは、ダイアログ ボックスとして適切な動作です。データが有効かどうかにかかわらず、ユーザーはダイアログ ボックス内のコントロールを自由に移動できる必要があります。 ただし、これは、ユーザーが無効なデータを入力して **[OK** ] ボタンを押すことができることを意味します。 このため、 <xref:System.Windows.Controls.Primitives.ButtonBase.Click>イベントを処理して **[OK** ] ボタンが押されたときに、コードでダイアログボックス内のすべてのコントロールを検証する必要もあります。  
  
[!code-csharp[Validating all controls in a dialog box](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginsDialogBox.xaml.cs?range=1-8,26-29,33-68)]
[!code-vb[Validating all controls in a dialog box](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MarginsDialogBox.xaml.vb?range=1-8,27-29,33-62)]  

このコードは、ウィンドウ上のすべての依存関係オブジェクトを列挙します。が無効<xref:System.Windows.Controls.Validation.GetHasError%2A>な場合 (から返された場合) `IsValid` 、無効`false`なコントロールはフォーカスを取得し、メソッドはを返し、ウィンドウは無効と見なされます。  
  
ダイアログ ボックスが有効な場合は、安全に閉じて、戻ることができます。 復帰プロセスの一環として、呼び出し元の機能に結果を返す必要があります。  
  
#### <a name="setting-the-modal-dialog-result"></a>モーダルダイアログの結果の設定

を使用して<xref:System.Windows.Window.ShowDialog%2A>ダイアログボックスを開くことは、基本的にメソッドの呼び出しと似ています。を使用して<xref:System.Windows.Window.ShowDialog%2A>ダイアログボックスを開いたコードは、が戻るまで<xref:System.Windows.Window.ShowDialog%2A>待機します。 が<xref:System.Windows.Window.ShowDialog%2A>を返した場合、それを呼び出したコードは、ユーザーが **[OK** ] ボタンまたは **[キャンセル**] ボタンを押したかどうかに基づいて、処理を継続するか、処理を停止するかを決定する必要があります。 この判断を容易にするために、ダイアログボックスは、 <xref:System.Boolean> <xref:System.Windows.Window.ShowDialog%2A>メソッドから返される値としてユーザーの選択を返す必要があります。  

**[OK** ] ボタンがクリックさ<xref:System.Windows.Window.ShowDialog%2A>れると`true`、はを返します。 これを実現するには<xref:System.Windows.Window.DialogResult%2A> 、 **[OK** ] ボタンをクリックしたときにダイアログボックスのプロパティを設定します。  

[!code-csharp[Responding to the OK button](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginsDialogBox.xaml.cs?range=1-8,25-27,32-33,67-68)]
[!code-vb[Responding to the OK button](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MarginsDialogBox.xaml.vb?range=1-8,27,31-33,61-62)]  

また、プロパティを<xref:System.Windows.Window.DialogResult%2A>設定すると、ウィンドウが自動的に閉じられるため、明示的に<xref:System.Windows.Window.Close%2A>呼び出す必要がなくなります。  
  
**[キャンセル**] ボタンがクリックさ<xref:System.Windows.Window.ShowDialog%2A>れると`false`、はを返す必要が<xref:System.Windows.Window.DialogResult%2A>あります。これには、プロパティの設定も必要です。  
  
[!code-csharp[Responding to the Cancel button](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginsDialogBox.xaml.cs?range=1-8,19-24,67-68)]
[!code-vb[Responding to the Cancel button](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MarginsDialogBox.xaml.vb?range=1-8,22-25,61-62)]  

ボタンの<xref:System.Windows.Controls.Button.IsCancel%2A> `true`プロパティがに設定され、ユーザーが **[キャンセル**] ボタンまたは ESC キーを押す<xref:System.Windows.Window.DialogResult%2A>と、は自動的`false`にに設定されます。 次のマークアップは、 <xref:System.Windows.Controls.Primitives.ButtonBase.Click>イベントを処理することなく、前のコードと同じ効果があります。  
  
[!code-xaml[Markup instead of handling the Click event](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginsDialogBox.xaml#L109-L109)]  

ユーザーがタイトルバーの`false` **[閉じる]** ボタンを押すか、 **[システム]** メニューの **[閉じる]** メニュー項目を選択すると、ダイアログボックスが自動的にを返します。  

#### <a name="processing-data-returned-from-a-modal-dialog-box"></a>モーダルダイアログボックスから返されたデータの処理  

がダイアログボックスによって設定されている場合は、が返されたとき<xref:System.Windows.Window.ShowDialog%2A>に<xref:System.Windows.Window.DialogResult%2A>プロパティを調べることによって、ダイアログボックスを開いた関数がダイアログボックスの結果を取得できます。 <xref:System.Windows.Window.DialogResult%2A>  
  
[!code-csharp[Processing data returned from the modal dialog box](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MainWindow.xaml.cs?range=1-10,77-79,89-96,194-195)]
[!code-vb[Processing data returned from the modal dialog box](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MainWindow.xaml.vb?range=1-9,58,69-73,131-132)]

ダイアログの結果が`true`の場合、関数は、ユーザーが指定したデータを取得して処理するためのキューとしてそれを使用します。  
  
> [!NOTE]
> が<xref:System.Windows.Window.ShowDialog%2A>返された後、ダイアログボックスを再び開くことはできません。 代わりに、新しいインスタンスを作成する必要があります。

ダイアログの結果が`false`の場合、関数は適切に処理を終了する必要があります。  
  
<a name="Creating_a_Modeless_Custom_Dialog_Box"></a>   
### <a name="creating-a-modeless-custom-dialog-box"></a>モードレスカスタムダイアログボックスの作成

次の図に示されている [検索] ダイアログ ボックスなどのモードレス ダイアログ ボックスは、基本的な外観はモーダル ダイアログ ボックスと同じです。  

![[検索] ダイアログボックスを表示するスクリーンショット。](./media/dialog-boxes-overview/find-modeless-dialog-box.png)  

しかし、次のセクションで説明するように、動作は少し異なります。  
  
#### <a name="opening-a-modeless-dialog-box"></a>モードレスダイアログボックスを開く

モードレスダイアログボックスは、 <xref:System.Windows.Window.Show%2A>メソッドを呼び出すことによって開かれます。  

[!code-xaml[XAML to define a modeless dialog box](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MainWindow.xaml#L21-L22)]  
 
[!code-csharp[Opening a modeless dialog box](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MainWindow.xaml.cs?range=1-10,65-76,194-195)]
[!code-vb[Openng a modeless dialog box](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MainWindow.xaml.vb?range=1-9,18-23,131,132)]  

と<xref:System.Windows.Window.ShowDialog%2A>は<xref:System.Windows.Window.Show%2A>異なり、はすぐにを返します。 その結果、呼び出し元のウィンドウは、モードレス ダイアログ ボックスが閉じられたことを知ることができず、したがって、ダイアログ ボックスの結果を確認するタイミングを判断したり、ダイアログ ボックスからデータを取得して、さらに処理したりすることができません。 代わりに、ダイアログ ボックスは、別の方法を作成して、呼び出し元のウィンドウに処理用のデータを返す必要があります。  
  
#### <a name="processing-data-returned-from-a-modeless-dialog-box"></a>モードレスダイアログボックスから返されたデータの処理  

この例では、 `FindDialogBox`は、特定の頻度を指定せずに検索するテキストに応じて、メインウィンドウに1つ以上の検索結果を返すことがあります。 モーダル ダイアログ ボックスと同様、モードレス ダイアログ ボックスは、プロパティを使用して結果を返すことができます。 ただし、ダイアログ ボックスを所有しているウィンドウは、それらのプロパティを確認するタイミングを知る必要があります。 これを可能にする方法の 1 つは、ダイアログ ボックスで、テキストが見つかったときに発生するイベントを実装することです。 `FindDialogBox``TextFoundEvent`この目的でを実装します。最初にデリゲートが必要です。  

[!code-csharp[The TextFoundEventHandler delegate](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/TextFoundEventHandler.cs)]
[!code-vb[The TextFoundEventHandler delegate](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/TextFoundEventHandler.vb)]  

デリゲートを使用し`FindDialogBox`て、 `TextFoundEvent`を実装します。 `TextFoundEventHandler`
  
[!code-csharp[The TextFound event](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/FindDialogBox.xaml.cs?range=1-17,125-126)]
[!code-vb[The TextFound event](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/FindDialogBox.xaml.vb?range=1-15,102-103)]

その結果`Find` 、は、検索結果が見つかったときにイベントを発生させることができます。  
  
[!code-csharp[Raising the TextFound event](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/FindDialogBox.xaml.cs?range=1-9,50-52,91-94,124-127)]
[!code-vb[Raising the TextFound event](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/FindDialogBox.xaml.vb?range=1-9,15,60-64,102-103)]  

そのとき、所有者ウィンドウは、このイベントを登録し、処理する必要があります。

[!code-csharp[Registering and handling the event](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MainWindow.xaml.cs?range=1-10,184-195)]
[!code-vb[Registering and handling the event](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MainWindow.xaml.vb?range=1-9,126-132)]  

#### <a name="closing-a-modeless-dialog-box"></a>モードレスダイアログボックスを閉じる

は<xref:System.Windows.Window.DialogResult%2A>設定する必要がないため、次のようなシステム提供機構を使用して、モードレスダイアログを閉じることができます。  
  
- タイトルバーの **[閉じる]** ボタンをクリックします。  
  
- Alt キーを押しながら F4 キーを押す。  
  
- **[システム]** メニューの **[閉じる]** をクリックします。  
  
または、 **[閉じる]** <xref:System.Windows.Window.Close%2A>ボタンがクリックされたときにコードからを呼び出すこともできます。  

[!code-csharp[Calling the Close method](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/FindDialogBox.xaml.cs?range=1-9,119-126)]
[!code-vb[Calling the Close method](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/FindDialogBox.xaml.vb?range=1-9,99-103)]  

## <a name="see-also"></a>関連項目

- [ポップアップの概要](../controls/popup-overview.md)
- [ダイアログボックスのサンプル](https://go.microsoft.com/fwlink/?LinkID=159984)
