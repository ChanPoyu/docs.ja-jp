---
title: WPF のブラウザーのホスト処理をサポートするネイティブ API
ms.date: 03/30/2017
f1_keywords:
- AutoGeneratedOrientationPage
helpviewer_keywords:
- browser hosting support [WPF]
- WPF browser hosting support APIs [WPF]
ms.assetid: 82c133a8-d760-45fb-a2b9-3a997537f1d4
ms.openlocfilehash: 29ff388685c67d06d7c5866a46954d5ade72acb1
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053357"
---
# <a name="native-wpf-browser-hosting-support-apis"></a>WPF のブラウザーのホスト処理をサポートするネイティブ API
Web ブラウザー [!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)]でのアプリケーションのホスティングは、WPF ホストから登録されたアクティブなドキュメントサーバー (DocObject とも呼ばれます) によって促進されます。 Internet Explorer は、アクティブなドキュメントを直接アクティブ化して統合できます。 Mozilla ブラウザーで xbap およびルース XAML ドキュメントをホストするため[!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)]に、には npapi プラグインが用意されています[!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)] 。これにより、Internet Explorer のように、アクティブなドキュメントサーバーに同様のホスト環境が提供されます。 ただし、他のブラウザーやスタンドアロンアプリケーションで Xbap および XAML ドキュメントをホストする最も簡単な方法は、Internet Explorer Web ブラウザーコントロールを使用することです。 Web ブラウザーコントロールは、複雑な Active ドキュメントサーバーホスティング環境を提供しますが、独自のホストがその環境をカスタマイズおよび拡張し、現在アクティブなドキュメントオブジェクトと直接通信できるようにします。  
  
 Active [!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)]ドキュメントサーバーでは、 [IOleObject](https://go.microsoft.com/fwlink/?LinkId=162049)、 [IOleDocument](https://go.microsoft.com/fwlink/?LinkId=162050)、 [IOleInPlaceActiveObject](https://go.microsoft.com/fwlink/?LinkId=162051)、 [IPersistMoniker](https://go.microsoft.com/fwlink/?LinkId=162045)、 [IOleCommandTarget](https://go.microsoft.com/fwlink/?LinkId=162047)など、いくつかの一般的なホスティングインターフェイスが実装されています。 Web ブラウザーコントロールでホストされている場合、これらのインターフェイスは、 [IWebBrowser2::D ocument](https://go.microsoft.com/fwlink/?LinkId=162048)プロパティによって返されるオブジェクトからクエリを実行できます。  
  
## <a name="iolecommandtarget"></a>IOleCommandTarget  
 WPF Active ドキュメントサーバーの[IOleCommandTarget](https://go.microsoft.com/fwlink/?LinkId=162047)の実装では、標準の OLE コマンドグループ (null コマンドグループ GUID を持つ) のナビゲーション関連およびブラウザー固有の多くのコマンドがサポートされています。 さらに、CGID_PresentationHost という名前のカスタムコマンドグループが認識されます。 現在、このグループ内に定義されているコマンドは1つだけです。  
  
```cpp  
DEFINE_GUID(CGID_PresentationHost, 0xd0288c55, 0xd6, 0x4f5e, 0xa8, 0x51, 0x79, 0xde, 0xc5, 0x1b, 0x10, 0xec);  
enum PresentationHostCommands {   
   PHCMDID_TABINTO = 1   
};  
```  
  
 PHCMDID_TABINTO は、Shift キーの状態に応じて、コンテンツ内の最初または最後にフォーカスがある要素にフォーカスを切り替えるように、プレゼンテーションホストに指示します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [IEnumRAWINPUTDEVICE](ienumrawinputdevice.md)  
 [IWpfHostSupport](iwpfhostsupport.md)
