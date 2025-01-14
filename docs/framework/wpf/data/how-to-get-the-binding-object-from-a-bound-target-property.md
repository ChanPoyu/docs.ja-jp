---
title: '方法: バインドされているターゲット プロパティからのバインディング オブジェクトの取得'
ms.date: 03/30/2017
helpviewer_keywords:
- data binding [WPF], getting binding objects from bound target properties
- properties [WPF], getting binding objects from
ms.assetid: 87974c5f-136b-4de7-b07d-9285b62ab123
ms.openlocfilehash: c7aacc2145ffe98ec7b58afb3b2e3dca151ef0ad
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69965432"
---
# <a name="how-to-get-the-binding-object-from-a-bound-target-property"></a>方法: バインドされているターゲット プロパティからのバインディング オブジェクトの取得
この例では、データにバインドされているターゲット プロパティからバインディング オブジェクトを取得する方法を示します。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Data.Binding>オブジェクトを取得するには、次の操作を実行します。  
  
 [!code-csharp[BindValidation#GetBinding](~/samples/snippets/csharp/VS_Snippets_Wpf/BindValidation/CSharp/Window1.xaml.cs#getbinding)]  
  
> [!NOTE]
> ターゲット オブジェクトの複数のプロパティがデータ バインディングを使用している可能性があるため、バインディングの依存関係プロパティを指定する必要があります。  
  
 または、を取得<xref:System.Windows.Data.BindingExpression>し、 <xref:System.Windows.Data.BindingExpression.ParentBinding%2A>プロパティの値を取得することもできます。  
  
 コード例全体については、「[バインディングの検証のサンプル](https://go.microsoft.com/fwlink/?LinkID=159972)」をご覧ください。  
  
> [!NOTE]
> バインディングがの<xref:System.Windows.Data.MultiBinding>場合は、. <xref:System.Windows.Data.BindingOperations><xref:System.Windows.Data.BindingOperations.GetMultiBinding%2A>を使用します。 がの<xref:System.Windows.Data.PriorityBinding>場合は、. <xref:System.Windows.Data.BindingOperations><xref:System.Windows.Data.BindingOperations.GetPriorityBinding%2A>を使用します。 <xref:System.Windows.Data.Binding>ターゲットプロパティが<xref:System.Windows.Data.BindingOperations.GetBindingBase%2A> <xref:System.Windows.Data.BindingOperations>、、または<xref:System.Windows.Data.PriorityBinding>を使用してバインドされているかどうかが不明な場合は、. を使用できます。 <xref:System.Windows.Data.MultiBinding>  
  
## <a name="see-also"></a>関連項目

- [コードでバインディングを作成する](how-to-create-a-binding-in-code.md)
- [方法トピック](data-binding-how-to-topics.md)
