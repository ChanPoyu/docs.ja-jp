---
title: エンティティ コンテナー
ms.date: 03/30/2017
ms.assetid: 16e80405-2c75-42fc-b0e4-b1df53b1c584
ms.openlocfilehash: 95740fb9d8b357a4fa160af6fdafb139711283cd
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795250"
---
# <a name="entity-container"></a>エンティティ コンテナー
*エンティティコンテナー*は、[エンティティセット](entity-set.md)、[アソシエーションセット](association-set.md)、および[関数インポート](model-declared-function.md)の論理的なグループです。  
  
 概念モデルで定義するエンティティ コンテナーは、次の条件を満たしている必要があります。  
  
- 1 つ以上のエンティティ コンテナーを各概念モデルに定義すること。  
  
- 各概念モデル内のエンティティ コンテナー名が一意であること。  
  
 エンティティ コンテナーは、1 つ以上の名前空間に定義されたエンティティ型またはアソシエーションを使用するエンティティ セットまたはアソシエーション セットを定義できます。 詳細については[、Entity Data Model を参照してください。名前](entity-data-model-namespaces.md)空間。  
  
## <a name="example"></a>例  
 下のダイアグラムは、`Book`、`Publisher`、および `Author` という 3 つのエンティティ型の概念モデルを示しています。  詳細については、次の例を参照してください。  
  
 ![3種類のエンティティを持つモデルの例](./media/entity-container/example-model-three-entity-types.gif)  
  
 ダイアグラムにはエンティティ コンテナー情報が示されていませんが、概念モデルにはエンティティ コンテナーを定義する必要があります。 [ADO.NET Entity Framework](./ef/index.md)は、概念スキーマ定義言語 ([CSDL](./ef/language-reference/csdl-specification.md)) と呼ばれる DSL を使用して概念モデルを定義します。 次の CSDL は、上のダイアグラムに示された概念モデルのエンティティ コンテナーを定義しています。 エンティティ コンテナー名は XML 属性に定義されています。  
  
 [!code-xml[EDM_Example_Model#EntityContainerExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entitycontainerexample)]  
  
## <a name="see-also"></a>関連項目

- [Entity Data Model キーの概念](entity-data-model-key-concepts.md)
- [Entity Data Model](entity-data-model.md)
