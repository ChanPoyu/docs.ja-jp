---
title: Visual Basic における LINQ to XML の概要
ms.date: 07/20/2015
helpviewer_keywords:
- LINQ to XML [Visual Basic], about LINQ to XML
- LINQ [Visual Basic], LINQ to XML
ms.assetid: 01c62a79-6d58-468e-84fb-039c05947701
ms.openlocfilehash: 5080efdf10a8e3b1f6815e836f9fffe968a8e4e0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69939257"
---
# <a name="overview-of-linq-to-xml-in-visual-basic"></a>Visual Basic における LINQ to XML の概要
Visual Basic は、xml [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]リテラルおよび xml 軸プロパティを使用したのサポートを提供します。 これにより、Visual Basic コードで XML を操作するための使い慣れた便利な構文を使用できます。 *Xml リテラル*を使用すると、コードに直接 xml を含めることができます。 *Xml 軸プロパティ*を使用すると、xml リテラルの子ノード、子孫ノード、および属性にアクセスできます。 詳細については、「 [Xml リテラルの概要](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-overview.md)」および「 [VISUAL BASIC での Xml へのアクセス](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)」を参照してください。  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]は、を利用[!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)]するために特に設計された、メモリ内の XML プログラミング API です。 Api は[!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]直接呼び出すことができますが、xml リテラルを宣言し、xml 軸プロパティに直接アクセスできるのは、Visual Basic だけです。  
  
> [!NOTE]
> XML リテラルおよび XML 軸のプロパティは、ASP.NET ページの宣言型コードではサポートされていません。 Visual Basic の XML 機能を使用するには、ASP.NET アプリケーションの分離コードページにコードを配置します。  
  
 [再生ボタン](./media/overview-of-linq-to-xml/play-video-icon-example.gif)関連するビデオデモについては、「 [LINQ to XML の使用を開始する方法](/aspnet/web-forms/videos/data-access/linq-videos-from-the-vb-team/how-do-i-get-started-with-linq-to-xml)」および「 [LINQ to XML を使用して Excel スプレッドシートを作成する方法](/aspnet/web-forms/videos/data-access/linq-videos-from-the-vb-team/how-do-i-create-excel-spreadsheets-using-linq-to-xml)」を参照してください。   
  
## <a name="creating-xml"></a>XML の作成  
 Visual Basic で XML ツリーを作成するには、2つの方法があります。 XML リテラルは、コード内で直接宣言することも、 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] api を使用してツリーを作成することもできます。 どちらのプロセスでも、コードは XML ツリーの最終構造を反映することができます。 たとえば、次のコード例では、XML 要素が作成されます。  
  
 [!code-vb[VbXmlSamples#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples2.vb#5)]  
  
 詳細については、「 [Visual Basic での XML の作成](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)」を参照してください。  
  
## <a name="accessing-and-navigating-xml"></a>アクセスと XML への移動  
 Visual Basic は、XML 構造にアクセスしたり、XML 構造を移動したりするための XML 軸プロパティを提供します。 これらのプロパティを使用すると、xml の子要素名を指定することによって、XML の要素と属性にアクセスできます。 または、 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]メソッドを明示的に呼び出して、要素と属性の移動と検索を行うこともできます。 たとえば、次のコード例では、xml 要素の属性と子要素を参照するために XML 軸プロパティを使用しています。 このコード例では[!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 、クエリを使用して子要素を取得し、XML 要素として出力し、変換を効果的に実行します。  
  
 [!code-vb[VbXmlSamples#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples3.vb#8)]  
  
 詳細については、「 [Visual Basic での XML へのアクセス](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)」を参照してください。  
  
## <a name="xml-namespaces"></a>XML 名前空間  
 Visual Basic では、 `Imports`ステートメントを使用して、グローバル XML 名前空間の別名を指定できます。 次の例では、ステートメントを`Imports`使用して XML 名前空間をインポートする方法を示します。  
  
 [!code-vb[VbXMLSamples#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples1.vb#1)]  
  
 Xml 軸プロパティにアクセスし、xml ドキュメントおよび xml 要素の xml リテラルを宣言するときに、XML 名前空間エイリアスを使用できます。  
  
 [Getxmlnamespace 演算子](../../../../visual-basic/language-reference/operators/getxmlnamespace-operator.md)を<xref:System.Xml.Linq.XNamespace>使用すると、特定の名前空間プレフィックスのオブジェクトを取得できます。  
  
 詳細については、「 [Imports ステートメント (XML 名前空間)](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)」を参照してください。  
  
### <a name="using-xml-namespaces-in-xml-literals"></a>Xml リテラルでの XML 名前空間の使用  
 次の例は、グローバル名前空間<xref:System.Xml.Linq.XElement> `ns`を使用するオブジェクトを作成する方法を示しています。  
  
 [!code-vb[VbXMLSamples#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples1.vb#2)]  
  
 Visual Basic コンパイラは、xml 名前空間エイリアスを含む xml リテラルを、 `xmlns`属性と共に xml 名前空間を使用するための xml 表記法を使用する同等のコードに変換します。 コンパイル時に、前のセクションの例のコードでは、次の例と同じ実行可能コードが生成されます。  
  
 [!code-vb[VbXMLSamples#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples1.vb#3)]  
  
### <a name="using-xml-namespaces-in-xml-axis-properties"></a>Xml 軸プロパティでの XML 名前空間の使用  
 Xml リテラルで宣言された XML 名前空間は、XML 軸プロパティでは使用できません。 ただし、XML 軸のプロパティではグローバル名前空間を使用できます。 XML 名前空間プレフィックスをローカル要素名から区切るには、コロンを使用します。 例を次に示します。  
  
 [!code-vb[VbXMLSamples#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples1.vb#4)]  
  
## <a name="see-also"></a>関連項目

- [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)
- [Visual Basic での XML の作成](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
- [Visual Basic での XML へのアクセス](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)
- [Visual Basic での XML の操作](../../../../visual-basic/programming-guide/language-features/xml/manipulating-xml.md)
