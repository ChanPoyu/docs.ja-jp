---
title: project.json からの .NET Core の移行
description: project.json を使って以前の .NET Core プロジェクトを移行する方法について説明します
ms.date: 07/19/2017
ms.custom: seodec18
ms.openlocfilehash: 6334f06a998054cfaf766654dda59d87f5d23ed8
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2019
ms.locfileid: "70105305"
---
# <a name="migrating-net-core-projects-from-projectjson"></a>project.json からの .NET Core プロジェクトの移行

このドキュメントでは、.NET Core プロジェクトの移行シナリオについて説明します。次の 3 つの移行シナリオを取り上げます。

1. [有効な最新スキーマの *project.json* から *csproj* への移行](#migration-from-projectjson-to-csproj)
2. [DNX から csproj への移行](#migration-from-dnx-to-csproj)
3. [RC3 と以前の .NET Core csproj プロジェクトから最終形式への移行](#migration-from-earlier-net-core-csproj-formats-to-rtm-csproj)

このドキュメントを使用できるのは、project.json を引き続き使っている、以前の .NET Core プロジェクトのみです。 これを .NET Framework から .NET Core への移行に適用することはできません。

## <a name="migration-from-projectjson-to-csproj"></a>project.json から csproj への移行

*project.json* から *.csproj* への移行は、次のいずれかの方法で実行できます。

- [Visual Studio 2017](#visual-studio-2017)
- [dotnet 移行コマンドライン ツール](#dotnet-migrate)

いずれの方法も、同じ基本エンジンを使用してプロジェクトを移行するので、両方の結果は同じです。 ほとんどの場合、2 つの方法のいずれかを使用して *project.json* を *csproj* に移行するだけで完了します。プロジェクト ファイルをさらに手動で編集する必要はありません。 結果の *.csproj* ファイルには、格納しているディレクトリ名と同じ名前が付けられます。

### <a name="visual-studio-2017"></a>Visual Studio 2017

*.xproj* ファイルまたは *.xproj* ファイルを参照するソリューションを開くと、 **[一方向のアップグレード]** ダイアログが表示されます。 このダイアログには、移行されるプロジェクトが表示されます。
ソリューション ファイルを開くと、ソリューション ファイルに指定されているすべてのプロジェクトが表示されます。 移行されるプロジェクトの一覧を確認し、 **[OK]** を選択します。

![移行されるプロジェクトの一覧が表示された [一方向のアップグレード] ダイアログ](media/one-way-upgrade.jpg)

Visual Studio では、選択したプロジェクトが自動的に移行されます。 すべてのプロジェクトを選択していない状態でソリューションを移行すると、同じダイアログが開き、そのソリューションの残りのプロジェクトをアップグレードすることを確認するメッセージが表示されます。 プロジェクトが移行されたら、**ソリューション エクスプローラー** ウィンドウでプロジェクトを右クリックして、 **[編集 \<プロジェクト名.csproj]** を選択し、そのコンテンツを表示して変更することができます。

移行されたファイル (*project.json*、*global.json*、 *.xproj*、およびソリューション ファイル) は *Backup* フォルダーに移動されます。 移行されるソリューション ファイルは Visual Studio 2017 にアップグレードされ、以前のバージョンの Visual Studio ではそのソリューション ファイルを開くことができなくなります。
移行レポートを含む *UpgradeLog.htm* というファイルも保存され、自動的に開かれます。

> [!IMPORTANT]
> 新しいツールは Visual Studio 2015 で使用できないので、Visual Studio 2015 を使用してプロジェクトを移行できません。

### <a name="dotnet-migrate"></a>dotnet の移行

コマンドラインのシナリオでは、[`dotnet migrate`](../tools/dotnet-migrate.md) コマンドを使用できます。 検出されたものに応じて、プロジェクト、ソリューション、または一連のフォルダーの順に移行されます。
プロジェクトを移行すると、プロジェクトとそのすべての依存ファイルが移行されます。

移行されたファイル (*project.json*、*global.json*、および *.xproj*) は *Backup* フォルダーに移動されます。

> [!NOTE]
> Visual Studio コードを使用している場合、`dotnet migrate` コマンドを実行しても、`tasks.json` などの Visual Studio コード固有のファイルは変更されません。 これらのファイルは手動で変更する必要があります。
> これは、Project Ryder などのエディターや、Visual Studio ではない統合開発環境 (IDE) を使用している場合にも該当します。

project.json および csproj 形式の比較については、「[project.json プロパティと csproj プロパティの間のマッピング](../tools/project-json-to-csproj.md)」を参照してください。

### <a name="common-issues"></a>一般的な問題

- 次のエラーが発生する場合:"No executable found matching command dotnet-migrate" (コマンド dotnet-migrate と一致する実行ファイルが見つかりません):

`dotnet --version` を実行して使用しているバージョンを確認します。 [`dotnet migrate`](../tools/dotnet-migrate.md) には、.NET Core CLI RC3 以降が必要です。
カレント ディレクトリまたは親ディレクトリに *global.json* ファイルがあり、`sdk` バージョンが古いバージョンに設定されている場合にこのエラーが発生します。

## <a name="migration-from-dnx-to-csproj"></a>DNX から csproj への移行

.NET Core 開発にまだ DNX を使用している場合、移行プロセスは次の 2 段階で実行する必要があります。

1. [既存の DNX 移行ガイダンス](from-dnx.md)を使用して DNX から project-json 対応の CLI に移行します。
2. 前のセクションの手順に従って、*project.json* から *.csproj* に移行します。  

> [!NOTE]
> Preview 1 リリースの .NET Core CLI で、DNX は公式に非推奨になりました。

## <a name="migration-from-earlier-net-core-csproj-formats-to-rtm-csproj"></a>以前の .NET Core csproj 形式から RTM csproj への移行

.NET Core csproj 形式は、ツールの新しいプレリリース バージョンごとに変化し、進化しています。 以前のバージョンの csproj から最新バージョンにプロジェクト ファイルを移行するツールはないため、プロジェクト ファイルを手動で編集する必要があります。 実際の手順は、移行するプロジェクト ファイルのバージョンによって異なります。 バージョン間で加えられた変更内容に基づいて、考慮する必要があるガイダンスの一部を次に示します。

- `<Project>` 要素からツールのバージョン プロパティを削除します (存在する場合)。
- `<Project>` 要素から XML 名前空間 (`xmlns`) を削除します。
- 存在しない場合は、`<Project>` 要素に `Sdk` 属性を追加し、`Microsoft.NET.Sdk` または `Microsoft.NET.Sdk.Web` に設定します。 この属性は、プロジェクトが SDK を使用することを指定するために使用します。 `Microsoft.NET.Sdk.Web` は Web アプリに使用されます。
- プロジェクトの一番上と一番下から `<Import Project="$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props" />` および `<Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />` ステートメントを削除します。 これらの import ステートメントは SDK で暗黙的に指定されているので、プロジェクトに含める必要はありません。
- プロジェクトに `Microsoft.NETCore.App` または `NETStandard.Library` `<PackageReference>` アイテムがある場合は削除することをお勧めします。 これらのパッケージ参照は、[SDK で暗黙的に指定されています](https://aka.ms/sdkimplicitrefs)。
- `Microsoft.NET.Sdk` `<PackageReference>` 要素がある場合は削除します。 SDK の参照は、`<Project>` 要素の `Sdk` 属性によって行われます。
- [SDK で暗黙的に指定](../tools/csproj.md#default-compilation-includes-in-net-core-projects)されている [glob](https://en.wikipedia.org/wiki/Glob_(programming)) を削除します。 プロジェクトにこれらの glob を残すと、コンパイル アイテムが重複するため、ビルド時にエラーが発生します。

これらの手順を実行すると、RTM .NET Core csproj 形式と完全に互換性のあるプロジェクトになります。

古い csproj 形式から新しい形式に移行する前と後の例については、.NET ブログの記事「[Updating Visual Studio 2017 RC – .NET Core Tooling improvements](https://devblogs.microsoft.com/dotnet/updating-visual-studio-2017-rc-net-core-tooling-improvements/)」 (Visual Studio 2017 RC の更新 - .NET Core ツールの改善) を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio プロジェクトのポート、移行、アップグレード](/visualstudio/porting/port-migrate-and-upgrade-visual-studio-projects)
