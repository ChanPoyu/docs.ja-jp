---
title: DataSet への XSLT 変換の適用
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 09f2e4ee-1d08-4ba8-8936-83394fee319d
ms.openlocfilehash: d9767844400d67e81c7065148b22c62352af0428
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784788"
---
# <a name="applying-an-xslt-transform-to-a-dataset"></a>DataSet への XSLT 変換の適用
の**WriteXml**メソッド<xref:System.Data.DataSet>を使用すると、データ**セット**の内容を XML データとして書き込むことができます。 一般的なタスクは、XSLT (XSL Transformation) を使用してこの XML を別の形式へ変換する操作です。 <xref:System.Xml.XmlDataDocument>ただし、を使用して**データセット**を同期すると、最初に**WriteXml**を使用してデータ**セット**の内容を XML データとして書き込むことなく、データセットのコンテンツに XSLT スタイルシートを適用できます。  
  
 次の例では、**データセット**にテーブルとリレーションシップを設定し、 **dataset**を**XmlDataDocument**と同期して、XSLT スタイルシートを使用してデータセットの一部を HTML ファイル**として**書き込みます。 次のコードは、XSLT スタイルシートの内容です。  
  
```xml  
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">  
  
<xsl:template match="CustomerOrders">  
  <HTML>  
  <STYLE>  
  BODY {font-family:verdana;font-size:9pt}  
  TD   {font-size:8pt}  
  </STYLE>  
    <BODY>  
    <TABLE BORDER="1">  
      <xsl:apply-templates select="Customers"/>  
    </TABLE>  
    </BODY>  
  </HTML>  
</xsl:template>  
  
<xsl:template match="Customers">  
    <TR><TD>  
      <xsl:value-of select="ContactName"/>, <xsl:value-of select="Phone"/><BR/>  
    </TD></TR>  
      <xsl:apply-templates select="Orders"/>  
</xsl:template>  
  
<xsl:template match="Orders">  
  <TABLE BORDER="1">  
    <TR><TD valign="top"><B>Order:</B></TD><TD valign="top"><xsl:value-of select="OrderID"/></TD></TR>  
    <TR><TD valign="top"><B>Date:</B></TD><TD valign="top"><xsl:value-of select="OrderDate"/></TD></TR>  
    <TR><TD valign="top"><B>Ship To:</B></TD>  
        <TD valign="top"><xsl:value-of select="ShipName"/><BR/>  
        <xsl:value-of select="ShipAddress"/><BR/>  
        <xsl:value-of select="ShipCity"/>, <xsl:value-of select="ShipRegion"/>  <xsl:value-of select="ShipPostalCode"/><BR/>  
        <xsl:value-of select="ShipCountry"/></TD></TR>  
  </TABLE>  
</xsl:template>  
  
</xsl:stylesheet>  
```  
  
 次のコードでは、**データセットにデータ**を読み込み、XSLT スタイルシートを適用します。  
  
> [!NOTE]
> リレーションシップを含む**データセット**に XSLT スタイルシートを適用する場合は、入れ子になった各関係に対して、 <xref:System.Data.DataRelation>の nested プロパティを**true**に設定すると、最適なパフォーマンスが得られます。 これにより、階層を自然な順番で上から下へと進みながらデータを変換する XSLT スタイル シートを利用できるようになります。パフォーマンスに大きく影響する XPath ロケーション軸 (たとえば、スタイル シートのノード テスト式での preceding-sibling や following-sibling) を使用して階層をたどる必要はなくなります。 入れ子になったリレーションの詳細については、「 [datarelation の入れ子](nesting-datarelations.md)」を参照してください。  
  
```vb  
' Assumes connection is a valid SqlConnection.  
Dim dataSet As DataSet = New DataSet("CustomerOrders")  
  
Dim customerAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM Customers", connection)  
customerAdapter.Fill(dataSet, "Customers")  
  
Dim orderAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM Orders", connection)  
orderAdapter.Fill(dataSet, "Orders")  
  
connection.Close()  
  
dataSet.Relations.Add("CustOrders", _  
dataSet.Tables("Customers").Columns("CustomerID"), _  
dataSet.Tables("Orders").Columns("CustomerID")).Nested = true  
  
Dim xmlDoc As XmlDataDocument = New XmlDataDocument(dataSet)   
  
Dim xslTran As XslTransform = New XslTransform  
xslTran.Load("transform.xsl")  
  
Dim writer As XmlTextWriter = New XmlTextWriter( _  
  "xslt_output.html", System.Text.Encoding.UTF8)  
  
xslTran.Transform(xmlDoc, Nothing, writer)  
writer.Close()  
```  
  
```csharp  
// Assumes connection is a valid SqlConnection.  
connection.Open();  
  
DataSet custDS = new DataSet("CustomerDataSet");  
  
SqlDataAdapter customerAdapter = new SqlDataAdapter(  
  "SELECT * FROM Customers", connection);  
customerAdapter.Fill(custDS, "Customers");  
  
SqlDataAdapter orderAdapter = new SqlDataAdapter(  
  "SELECT * FROM Orders", connection);  
orderAdapter.Fill(custDS, "Orders");  
  
connection.Close();  
  
custDS.Relations.Add("CustOrders",  
  custDS.Tables["Customers"].Columns["CustomerID"],  
                     custDS.Tables["Orders"].Columns["CustomerID"]).Nested = true;  
  
XmlDataDocument xmlDoc = new XmlDataDocument(custDS);   
  
XslTransform xslTran = new XslTransform();  
xslTran.Load("transform.xsl");  
  
XmlTextWriter writer = new XmlTextWriter("xslt_output.html",   
  System.Text.Encoding.UTF8);  
  
xslTran.Transform(xmlDoc, null, writer);  
writer.Close();  
```  
  
## <a name="see-also"></a>関連項目

- [DataSet と XmlDataDocument の同期](dataset-and-xmldatadocument-synchronization.md)
- [ADO.NET の概要](../ado-net-overview.md)
