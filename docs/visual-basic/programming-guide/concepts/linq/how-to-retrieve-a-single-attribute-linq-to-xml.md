---
title: '方法: 単一の属性を取得する (LINQ to XML) (Visual Basic)'
ms.date: 07/20/2015
ms.assetid: 11b938d7-c011-4048-900e-8b9183c41c94
ms.openlocfilehash: 635644783153765d61aff3c00fe16860642c29f1
ms.sourcegitcommit: eb9ff6f364cde6f11322e03800d8f5ce302f3c73
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/01/2019
ms.locfileid: "68710520"
---
# <a name="how-to-retrieve-a-single-attribute-linq-to-xml-visual-basic"></a>方法: 単一の属性を取得する (LINQ to XML) (Visual Basic)
このトピックでは、属性名を指定して要素の単一の属性を取得する方法について説明します。 これは、特定の属性を持つ要素を検索するクエリ式を記述する場合に便利です。  
  
 <xref:System.Xml.Linq.XElement.Attribute%2A> クラスの <xref:System.Xml.Linq.XElement> メソッドは、指定された名前を持つ <xref:System.Xml.Linq.XAttribute> を返します。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Xml.Linq.XElement.Attribute%2A> メソッドを使用します。  
  
```vb  
Dim cust As XElement = <PhoneNumbers>  
                           <Phone type="home">555-555-5555</Phone>  
                           <Phone type="work">555-555-6666</Phone>  
                       </PhoneNumbers>  
Dim elList = From el In cust...<Phone>  
For Each e As XElement In elList  
    Console.WriteLine(e.@type)  
Next  
```  
  
 この例では、`Phone` という名前のツリー内のすべての子孫を検索し、次に `type` という名前の属性を検索します。  
  
 このコードを実行すると、次の出力が生成されます。  
  
```  
home  
work  
```  
  
## <a name="example"></a>例  
 属性の値を取得する場合は、<xref:System.Xml.Linq.XElement> オブジェクトを使用して行う場合と同じように、その属性をキャストできます。 次に例を示します。  
  
```vb  
Dim cust As XElement = <PhoneNumbers>  
                           <Phone type="home">555-555-5555</Phone>  
                           <Phone type="work">555-555-6666</Phone>  
                       </PhoneNumbers>  
Dim elList As IEnumerable(Of XElement) = _  
    From el In cust...<Phone> _  
    Select el  
For Each el As XElement In elList  
    Console.WriteLine(el.@type)  
Next  
```  
  
 このコードを実行すると、次の出力が生成されます。  
  
```  
home  
work  
```  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] では、`string`、`bool`、`bool?`、`int`、`int?`、`uint`、`uint?`、`long`、`long?`、`ulong`、`ulong?`、`float`、`float?`、`double`、`double?`、`decimal`、`decimal?`、`DateTime`、`DateTime?`、`TimeSpan`、`TimeSpan?`、`GUID`、および `GUID?` に対する <xref:System.Xml.Linq.XAttribute> クラスのための明示的なキャスト演算子が用意されています。  
  
## <a name="example"></a>例  
 上記と同じコードを使用して、名前空間内の属性を取得する例を次に示します。 詳細については、「[名前空間の概要」 (LINQ to XML) (Visual Basic)](namespaces-overview-linq-to-xml.md)を参照してください。  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim cust As XElement = _  
            <aw:PhoneNumbers>  
                <aw:Phone aw:type="home">555-555-5555</aw:Phone>  
                <aw:Phone aw:type="work">555-555-6666</aw:Phone>  
            </aw:PhoneNumbers>  
        Dim elList As IEnumerable(Of XElement) = _  
            From el In cust...<aw:Phone> _  
            Select el  
        For Each el As XElement In elList  
            Console.WriteLine(el.@aw:type)  
        Next  
    End Sub  
End Module  
```  
  
 このコードを実行すると、次の出力が生成されます。  
  
```  
home  
work  
```  
  
## <a name="see-also"></a>関連項目

- [LINQ to XML 軸 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-axes.md)
