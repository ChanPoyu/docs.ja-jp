---
title: プロパティ条件に基づく UI オートメーション要素の検索
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- elements, finding by property conditions
- UI Automation, finding elements by property conditions
ms.assetid: 3acaee5a-6ce8-4c3e-81c8-67e59eb74477
ms.openlocfilehash: 536a71532f02782f9e84bb2bd086af212a77c0da
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71043663"
---
# <a name="find-a-ui-automation-element-based-on-a-property-condition"></a>プロパティ条件に基づく UI オートメーション要素の検索
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 の最新情報[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]については[、「Windows Automation API:UI オートメーション](https://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 このトピックには、特定のプロパティまたはプロパティに基づいて[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]ツリー内の要素を検索する方法を示すコード例が含まれています。  
  
## <a name="example"></a>例  
 次の例では、 <xref:System.Windows.Automation.AutomationElement>ツリー内の関心のある要素 (または要素) を識別する一連のプロパティ条件を指定しています。 次に、一致するすべての要素の検索が<xref:System.Windows.Automation.AutomationElement.FindAll%2A> 、一致する要素の数<xref:System.Windows.Automation.AndCondition>を制限する一連のブール演算を組み込むメソッドを使用して実行されます。  
  
> [!NOTE]
> から検索する場合<xref:System.Windows.Automation.AutomationElement.RootElement%2A>は、直接の子のみを取得するようにしてください。 子孫の検索では、数百または数千の要素を反復処理することがあります。その結果、スタックオーバーフローが発生する可能性があります。 下位レベルの特定の要素を取得しようとする場合、アプリケーション ウィンドウから、または下位レベルのコンテナーから検索を開始する必要があります。  
  
 [!code-csharp[InvokePatternApp#1100](../../../samples/snippets/csharp/VS_Snippets_Wpf/InvokePatternApp/CSharp/InvokePatternApp.cs#1100)]
 [!code-vb[InvokePatternApp#1100](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InvokePatternApp/VisualBasic/Client.vb#1100)]  
  
## <a name="see-also"></a>関連項目

- [InvokePattern と ExpandCollapsePattern のメニュー項目のサンプル](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms771636(v=vs.90))
- [UI オートメーション要素の取得](obtaining-ui-automation-elements.md)
- [AutomationID プロパティの使用](use-the-automationid-property.md)
