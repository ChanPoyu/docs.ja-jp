---
title: Docker アプリケーションの状態とデータ
description: Docker アプリケーションでの状態とデータの管理。 マイクロサービスのインスタンスは再利用できませんが、データはそうではありません。マイクロ サービスでこれを処理する方法。
ms.date: 09/20/2018
ms.openlocfilehash: bd0ac007479dcd51f2c639881273b81d1fd8b6d7
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71039580"
---
# <a name="state-and-data-in-docker-applications"></a>Docker アプリケーションの状態とデータ

ほとんどの場合、コンテナーはプロセスのインスタンスと考えることができます。 プロセスでは永続的な状態は維持されません。 コンテナーからローカル ストレージに書き込まれる可能性がありますが、インスタンスが無期限に存在すると想定することは、メモリ内の単一の場所が持続的であると想定するようなものです。 プロセスなどのコンテナー イメージには複数のインスタンスがあること、またはコンテナー イメージは最終的に強制終了されることを想定する必要があります。 コンテナー オーケストレーターを使用してコンテナー イメージを管理する場合、それらはノード間または VM 間を移動させられると想定する必要があります。

Docker アプリケーションで永続的なデータを管理するには、次のソリューションを使用します。

Docker ホストから、[Docker ボリューム](https://docs.docker.com/engine/admin/volumes/)として:

- **ボリューム**は、Docker によって管理されるホスト ファイル システムの領域に格納されます。

- **バインド マウント**はホスト ファイルシステム内の任意のフォルダーにマップすることができます。このため、Docker プロセスからアクセスを制御することができず、アクセスによってセキュリティ上のリスクが発生することがあります。これは、機密性の高い OS フォルダーがコンテナーからアクセスされる可能性があるからです。

- **tmpfs マウント**は、ホストのメモリ内にのみ存在していてファイル システムに決して書き込まれない仮想フォルダーに似ています。

リモート ストレージから:

- [Azure Storage](https://azure.microsoft.com/documentation/services/storage/)。地理的に分散可能なストレージを提供し、コンテナーに適した長期的で持続性の高いソリューションを提供します。

- [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) のようなリモート リレーショナル データベース、[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) のような NoSQL データベース、[Redis](https://redis.io/) のようなキャッシュ サービス。

Docker コンテナーから:

> Docker には、*オーバーレイ ファイル システム*という機能があります。 この機能に、コンテナーのルート ファイル システムに更新された情報を保存するコピー オン ライト タスクが実装されています。 この情報とは別に、コンテナーの基になっている元のイメージがあります。 コンテナーがシステムから削除された場合、それらの変更は失われます。 そのため、ローカル ストレージ内にコンテナーの状態を保存することはできますが、それを中心にシステムを設計することは、既定ではステートレスなコンテナー設計の前提と矛盾します。
>
> ただし、以前に紹介した Docker Volumes は、ローカル データ Docker を処理する方法として推奨されるようになりました。 コンテナー内のストレージの詳細については、[Docker ストレージ ドライバー](https://docs.docker.com/storage/storagedriver/select-storage-driver/) に関するページおよび [ストレージ ドライバー](https://docs.docker.com/storage/storagedriver/)に関するページを参照してください。

次にこれらの選択肢の詳細について説明します。

**ボリューム**は、ホスト OS からコンテナー内のディレクトリにマップされたディレクトリです。 コンテナー内のコードがディレクトリへのアクセス権を持っている場合、それは実際にはホスト OS 上のディレクトリに対するアクセス権です。 このディレクトリはコンテナー自体の有効期間に関連付けられていません。さらにディレクトリは Docker によって管理され、ホスト マシンのコア機能から分離されています。 したがって、データ ボリュームは、コンテナーの有効期間とは独立してデータを保持するように設計されます。 Docker ホストからコンテナーまたはイメージを削除した場合、データ ボリュームに保持されているデータは削除されません。

ボリュームについては、名前を付けることも匿名 (既定) とすることもできます。 名前付きボリュームは、**データ ボリューム コンテナー**が進化したものです。これにより、コンテナー間でのデータの共有が簡単になります。 ボリュームでは、いくつかのオプションの中でボリューム ドライバーもサポートされています。これを使用すると、データをリモート ホスト上に格納することができます。

**バインド マウント**はずっと前から利用できるようになっています。これを使用すると、任意のフォルダーをコンテナー内のマウント ポイントにマップすることができます。 バインド マウントにはボリュームよりも多くの制限があるほか、重要なセキュリティ上の問題もあるため、ボリュームの方をお勧めします。

**tmpfs マウント**は基本的に、ホストのメモリ内にのみ存在していてファイル システムに決して書き込まれない仮想フォルダーです。 これは、高速で安全ですがメモリを消費するため、非永続的なデータのためだけに用意されています。

図 4-5 に示すように、通常の Docker ボリュームは、コンテナー自体の外部 (ただし、ホスト サーバーまたは VM の物理的境界内) に格納できます。 ただし、Docker コンテナーは、あるホスト サーバーまたは VM から別のホスト サーバーまたは VM のボリュームにアクセスすることはできません。 つまり、このようなボリュームを使用した場合、さまざまな Docker ホスト上で実行されるコンテナーの間で共有されたデータを管理することはできません。しかし、リモート ホストをサポートするボリューム ドライバーを使用すれば、それを達成することが可能です。

![リモート ホストをサポートするリモート ドライバーを使用していない場合、コンテナー間でのボリュームの共有は同一ホスト内でのみ可能です。](./media/image5.png)

**図 4-5** コンテナーベースのアプリケーション向けのボリュームと外部データ ソース

さらに、オーケストレーターにより Docker コンテナーが管理される場合、クラスターによって実行される最適化に応じて、ホスト間でコンテナーが移動する可能性があります。 そのため、ビジネス データにデータ ボリュームを使用することはお勧めしません。 ただし、ビジネス データの一貫性に影響を与えないトレース ファイルやテンポラル ファイルなどを処理する場合には適しているメカニズムです。

Azure SQL Database、Azure Cosmos DB のような**リモート データ ソースとキャッシュ**、または Redis のようなリモート キャッシュは、コンテナーなしで開発する場合と同じ方法でコンテナー化アプリケーションで使用できます。 これは、ビジネス アプリケーション データを格納する実績のある方法です。

**Azure Storage。** ビジネス データは、通常、Azure Storage のような外部リソースやデータベースに配置する必要があります。 具体的には、Azure Storage はクラウドで次のサービスを提供します。

- BLOB ストレージには、非構造化オブジェクト データが格納されます。 BLOB は、ドキュメントやメディア ファイル (画像、オーディオ、ビデオ ファイル) など、任意の種類のテキストまたはバイナリ データの可能性があります。 BLOB ストレージは、オブジェクト ストレージとも呼ばれます。

- ファイル ストレージは、標準の SMB プロトコルを使用するレガシ アプリケーション用の共有ストレージを提供します。 Azure 仮想マシンとクラウド サービスは、マウントされた共有を介してアプリケーション コンポーネント全体でファイル データを共有できます。 オンプレミス アプリケーションは、ファイル サービス REST API を介して共有内のファイル データにアクセスできます。

- テーブル ストレージには、構造化データセットが格納されます。 テーブル ストレージは NoSQL のキー属性データ ストアであり、迅速な開発と大量のデータへの高速アクセスが可能です。

**リレーショナル データベースと NoSQL データベース。** 外部データベースには、SQL Server、PostgreSQL、Oracle のようなリレーショナル データベースや、Azure Cosmos DB、MongoDB のような NoSQL データベースなど、多くの選択肢があります。これらのデータベースについては、まったく異なる話題なので、このガイドでは説明しません。

>[!div class="step-by-step"]
>[前へ](containerize-monolithic-applications.md)
>[次へ](service-oriented-architecture.md)
