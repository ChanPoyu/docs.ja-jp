---
title: 'チュートリアル: モデル ビルダーで回帰を使用して価格を予測する'
description: このチュートリアルでは、ML.NET モデル ビルダーを使用して、価格 (具体的にはニューヨーク市のタクシー運賃) を予測する回帰モデルを構築する方法を示します。
author: luisquintanilla
ms.author: luquinta
ms.date: 09/18/2019
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: bb344a7f01e8ffe0e40578c6fb2f28bebd2eb807
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117968"
---
# <a name="tutorial-predict-prices-using-regression-with-model-builder"></a>チュートリアル: モデル ビルダーで回帰を使用して価格を予測する

ML.NET モデル ビルダーを使用して、価格を予測する回帰モデル () を構築する方法について説明します。  このチュートリアルで開発する .NET コンソール アプリでは、過去のニューヨーク市のタクシー運賃データに基づいてタクシー運賃を予測します。

モデル ビルダーの価格予測テンプレートは、数値による予測値を必要とするすべてのシナリオで使用できます。 シナリオの例には、住宅価格の予測、需要予測、売上予測などがあります。

このチュートリアルでは、次の作業を行う方法について説明します。
> [!div class="checklist"]
>
> - データを準備して理解する
> - シナリオを選択する
> - データを読み込む
> - モデルをトレーニングする
> - モデルを評価する
> - モデルを使用して予測を行う

> [!NOTE]
> モデル ビルダーは現在のところ、プレビュー段階です。

## <a name="pre-requisites"></a>前提条件

前提条件の一覧とインストール手順は、[モデル ビルダーのインストール ガイド](../how-to-guides/install-model-builder.md)を参照してください。

## <a name="create-a-console-application"></a>コンソール アプリケーションを作成する

1. "TaxiFarePrediction" という名前の **.NET Core コンソール アプリケーション**を作成します。

## <a name="prepare-and-understand-the-data"></a>データを準備して理解する

1. プロジェクトに *Data* という名前のディレクトリを作成して、データ セットのファイルを保存します。

1. 機械学習モデルのトレーニングと評価に使用するデータ セットは、NYC TLC Taxi Trip データ セットから取得したものです。

    このデータ セットをダウンロードするには、[taxi-fare-train.csv のダウンロード リンク](https://raw.githubusercontent.com/dotnet/machinelearning/master/test/data/taxi-fare-train.csv)に移動します。

    ページが読み込まれたら、ページ上の任意の場所を右クリックして、 **[名前を付けて保存]** を選択します。

    **[名前を付けて保存] ダイアログ**を使って、前の手順で作成した *Data* フォルダーにファイルを保存します。

1. **ソリューション エクスプローラー**で、 *[taxi-fare-train.csv]* ファイルを右クリックし、 **[プロパティ]** を選択します。 **[詳細設定]** で、 **[出力ディレクトリにコピー]** の値を **[新しい場合はコピーする]** に変更します。

`taxi-fare-train.csv` データ セットの各行に、タクシーの移動の詳細が含まれています。

1. **taxi-fare-train.csv** データ セットを開きます

    提供されているデータ セットには、次の列が含まれます。

    - **vendor_id:** タクシー会社の ID は特徴です。
    - **rate_code:** タクシー旅行のレートの種類は特徴です。
    - **passenger_count:** 旅行の乗客数は特徴です。
    - **trip_time_in_secs:** 旅行の所要時間です。
    - **trip_distance:** 旅行距離は特徴です。
    - **payment_type:** 支払い方法 (現金またはクレジット カード) は特徴です。
    - **fare_amount:** 支払った合計タクシー運賃はラベルです。

`label` は予測する列です。 回帰タスクを実行する場合の目標は、数値を予測することです。 この価格予測シナリオでは、タクシーの乗車のコストが予測されています。 したがって、**fare_amount** がラベルです。 識別された `features` は、`label` を予測するためにモデルを指定する入力です。 この場合、残りの列は、運賃の金額を予測するための機能または入力として使用されます。

## <a name="choose-a-scenario"></a>シナリオを選択する

モデルをトレーニングするには、モデル ビルダーによって提供される機械学習シナリオの一覧から選択する必要があります。 この場合、シナリオは `Price Prediction` です。

1. **ソリューション エクスプローラー**で、 *[TaxiFarePrediction]* プロジェクトを右クリックし、 **[追加]**  >  **[機械学習]** を選択します。
1. モデル ビルダー ツールのシナリオの手順で、*価格の予測*のシナリオを選択します。

## <a name="load-the-data"></a>データを読み込む

モデル ビルダーは、SQL Server データベースか、csv または tsv 形式のローカル ファイルという 2 つのソースからデータを受け取ることができます。

1. モデル ビルダー ツールのデータの手順で、データ ソースのドロップダウンから *[ファイル]* を選択します。
1. *[ファイルの選択]* テキスト ボックスの横にあるボタンを選択し、ファイル エクスプローラーを使用して *Data* ディレクトリにある *[taxi-fare-test.csv]* を参照し、選択します
1. *[Label or Column to Predict]\(予測するラベルまたは列\)* ドロップダウンにある *[fare_amount]* を選択して、モデル ビルダー ツールのトレーニングの手順に移動します。

## <a name="train-the-model"></a>モデルをトレーニングする

このチュートリアルで、価格予測モデルのトレーニングに使用する機械学習のタスクは、回帰です。 モデルのトレーニング プロセス中、モデル ビルダーは、さまざまな回帰アルゴリズムと設定を使用して、データセットで最も良いパフォーマンスのモデルを見つける個別のモデルをトレーニングします。

モデルのトレーニングに必要な時間は、データの量に比例します。 モデル ビルダーにより、 **[Time to train (seconds)]\(トレーニング時間 (秒)\)** の既定値が、データ ソースのサイズに基づいて自動的に選択されます。

1. より長い時間トレーニングする場合を除き、 *[Time to train (seconds)]\(トレーニング時間 (秒)\)* は既定値のままとします。
2. *[Start Training]\(トレーニング開始\)* を選択します。

トレーニング プロセスを通して、進捗データがトレーニングの手順の `Progress` セクションに表示されます。

- 状態には、トレーニング プロセスの完了ステータスが表示されます。
- [Best accuracy]\(最良の精度\) には、これまでにモデル ビルダーで見つかった最良のパフォーマンスのモデルの精度が表示されます。 精度が高くなるほど、テスト データでモデルが正確に予測されたことになります。
- [Best algorithm]\(最良のアルゴリズム\) には、これまでにモデル ビルダーで見つかった最良のパフォーマンスのアルゴリズムの名前が表示されます。
- [Last algorithm]\(最後のアルゴリズム\) には、モデル ビルダーがモデルのトレーニングに最近使用したアルゴリズムの名前が表示されます。

トレーニングが完了したら、評価の手順に移動します。

## <a name="evaluate-the-model"></a>モデルを評価する

トレーニングの手順の結果が、最良のパフォーマンスだった 1 つのモデルになります。 モデル ビルダー ツールの評価の手順の出力セクションには、 *[Best Model]\(最良のモデル\)* エントリの最良のパフォーマンスのモデルで使用されたアルゴリズムと、 *[Best Model Quality (RSquared)]\(最良のモデル品質 (RSquared)\)* のメトリックが含まれます。 また、概要テーブルには上位 5 つのモデルとそのメトリックが含まれています。

精度のメトリックに不満がある場合、モデルのトレーニング時間を増やすか、さらに多くのデータを使用すると、モデルの精度を簡単に高めることができます。 そうでない場合は、コードの手順に移動します。

## <a name="add-the-code-to-make-predictions"></a>予測を行うコードを追加する

トレーニング プロセスの結果として 2 つのプロジェクトが作成されます。

- TaxiFarePredictionML.ConsoleApp: モデルのトレーニングと使用に関するコードが含まれる .NET Core コンソール アプリケーション。
- TaxiFarePredictionML.Model: 入出力モデル データのスキーマを定義するデータ モデルと、トレーニング中にパフォーマンスが最も良かったモデルの永続化バージョンが含まれる .NET Standard クラス ライブラリ。

1. モデル ビルダー ツールのコードの手順で、 **[プロジェクトの追加]** を選択して、自動生成されたプロジェクトをソリューションに追加します。
1. *[TaxiFarePrediction]* プロジェクトを右クリックします。 それから、 **[追加]、[参照]** の順に選択します。 **[プロジェクト]、[ソリューション]** ノードを選択し、一覧で *[TaxiFarePredictionML.Model]* プロジェクトを選択して [OK] を選択します。
1. *[TaxiFarePrediction]* プロジェクトの *[Program.cs]* ファイルを開きます。
1. *Microsoft.ML* NuGet パッケージと *TaxiFarePredictionML.Model* プロジェクトを参照するために、次の using ステートメントを追加します。

    ```csharp
    using System;
    using Microsoft.ML;
    using TaxiFarePredictionML.Model.DataModels;
    ```

1. `ConsumeModel` メソッドを `Program` クラスに追加します。

    ```csharp
    static ModelOutput ConsumeModel(ModelInput input)
    {
        // 1. Load the model
        MLContext mlContext = new MLContext();
        ITransformer mlModel = mlContext.Model.Load("MLModel.zip", out var modelInputSchema);

        // 2. Create PredictionEngine
        var predictionEngine = mlContext.Model.CreatePredictionEngine<ModelInput, ModelOutput>(mlModel);

        // 3. Use PredictionEngine to use model on input data
        ModelOutput result = predictionEngine.Predict(input);

        // 4. Return prediction result
        return result;
    }
    ```

    `ConsumeModel` によって、トレーニング済みのモデルが読み込まれ、モデル用の [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) が作成され、それを使った予測が新しいデータで実行されます。

1. 新しいデータに対してモデルを使った予測を行うには、`ModelInput` クラスの新しいインスタンスを作成し、`ConsumeModel` メソッドを使用します。 運賃額が入力に含まれていないことがわかります。 これは、モデルによってその予測が生成されるためです。 `Main` メソッドに次のコードを追加して、アプリケーションを実行します

    ```csharp
    // Create sample data
    ModelInput input = new ModelInput()
    {
        Vendor_id = "CMT",
        Rate_code = 1,
        Passenger_count = 1,
        Trip_time_in_secs = 1271,
        Trip_distance = 3.8f,
        Payment_type = "CRD"
    };

    // Make prediction
    ModelOutput prediction = ConsumeModel(input);

    // Print Prediction
    Console.WriteLine($"Predicted Fare: {prediction.Score}");
    Console.ReadKey();
    ```

    プログラムによって生成される出力は次のスニペットのようになります。

    ```bash
    Predicted Fare: 16.82245
    ```

別のソリューション内で後で生成されたプロジェクトを参照する必要がある場合は、`C:\Users\%USERNAME%\AppData\Local\Temp\MLVSTools` ディレクトリを検索することができます。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、次の作業を行う方法を学びました。
> [!div class="checklist"]
>
> - データを準備して理解する
> - シナリオを選択する
> - データを読み込む
> - モデルをトレーニングする
> - モデルを評価する
> - モデルを使用して予測を行う

### <a name="additional-resources"></a>その他のリソース

このチュートリアルで説明しているトピックについて詳しくは、次のリソースを参照してください。

- [モデル ビルダーのシナリオ](../automate-training-with-model-builder.md#scenarios)
- [回帰](../resources/glossary.md#regression)
- [回帰モデルのメトリック](../resources/metrics.md#metrics-for-regression)
- [NYC TLC Taxi Trip データ セット](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml)
