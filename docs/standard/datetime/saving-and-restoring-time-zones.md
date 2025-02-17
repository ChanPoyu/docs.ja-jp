---
title: タイム ゾーンの保存と復元
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- restoring time zones
- deserialization [.NET Framework], time zones
- serialization [.NET Framework], time zones
- time zone objects [.NET Framework], restoring
- saving time zones
- time zone objects [.NET Framework], deserializing
- time zones [.NET Framework], saving
- time zones [.NET Framework], restoring
- time zone objects [.NET Framework], serializing
- time zone objects [.NET Framework], saving
ms.assetid: 4028b310-e7ce-49d4-a646-1e83bfaf6f9d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ea44b29eaa0273baadbf02093108bc4da912a3e5
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2019
ms.locfileid: "70106744"
---
# <a name="saving-and-restoring-time-zones"></a>タイム ゾーンの保存と復元

クラス<xref:System.TimeZoneInfo>は、定義済みのタイムゾーンデータを取得するためにレジストリに依存しています。 ただし、レジストリは動的な構造です。 また、レジストリに格納されているタイムゾーン情報は、主に現在の年の時間調整と変換を処理するためにオペレーティングシステムによって使用されます。 正確なタイムゾーンデータに依存するアプリケーションには、次の2つの大きな影響があります。

- アプリケーションで必要なタイムゾーンがレジストリで定義されていないか、名前が変更されたか、レジストリから削除された可能性があります。

- レジストリに定義されているタイムゾーンには、履歴のタイムゾーンの変換に必要な特定の調整規則に関する情報が含まれていない場合があります。

クラス<xref:System.TimeZoneInfo>は、タイムゾーンデータのシリアル化 (保存) と逆シリアル化 (復元) をサポートすることで、これらの制限に対処します。

## <a name="time-zone-serialization-and-deserialization"></a>タイムゾーンのシリアル化と逆シリアル化

タイムゾーンデータをシリアル化および逆シリアル化してタイムゾーンを保存および復元するには、次の2つのメソッド呼び出しのみが必要です。

- オブジェクトの<xref:System.TimeZoneInfo> <xref:System.TimeZoneInfo.ToSerializedString%2A>メソッドを呼び出すことによって、オブジェクトをシリアル化できます。 メソッドはパラメーターを取らず、タイムゾーン情報を含む文字列を返します。

- `static` ( <xref:System.TimeZoneInfo> VisualBasic)<xref:System.TimeZoneInfo.FromSerializedString%2A?displayProperty=nameWithType>メソッドにその文字列を渡すことによって、シリアル化された文字列からオブジェクトを逆シリアル化できます。`Shared`

## <a name="serialization-and-deserialization-scenarios"></a>シリアル化と逆シリアル化のシナリオ

<xref:System.TimeZoneInfo>オブジェクトを文字列に保存 (シリアル化) し、後で使用できるように復元 (または逆シリアル化) する機能により、ユーティリティと<xref:System.TimeZoneInfo>クラスの柔軟性が向上します。 ここでは、シリアル化と逆シリアル化が最も役立つ状況について説明します。

### <a name="serializing-and-deserializing-time-zone-data-in-an-application"></a>アプリケーション内のタイムゾーンデータのシリアル化と逆シリアル化

シリアル化されたタイムゾーンは、必要に応じて文字列から復元できます。 アプリケーションは、レジストリから取得したタイムゾーンが特定の日付範囲内の日付と時刻を正しく変換できない場合に、このような処理を実行する可能性があります。 たとえば、Windows XP レジストリのタイムゾーンデータは1つの調整規則をサポートしますが、Windows Vista レジストリで定義されているタイムゾーンは通常、2つの調整規則に関する情報を提供します。 これは、過去の時刻の変換が不正確になる可能性があることを意味します。 タイムゾーンデータのシリアル化と逆シリアル化では、この制限を処理できます。

次の例では、調整<xref:System.TimeZoneInfo>規則が適用されていないカスタムクラスが、米国の米国に夏時間を導入する前の、1883から1917までの東部標準時のタイムゾーン。 カスタムタイムゾーンは、グローバルスコープを持つ変数でシリアル化されます。 タイムゾーンの変換メソッド`ConvertUtcTime`は、協定世界時 (UTC) の時刻に変換されます。 日付と時刻が1917以前である場合は、カスタム東部標準時のタイムゾーンがシリアル化された文字列から復元され、レジストリから取得したタイムゾーンが置き換えられます。

[!code-csharp[System.TimeZone2.Serialization.1#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Serialization.1/cs/Serialization.cs#1)]
[!code-vb[System.TimeZone2.Serialization.1#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Serialization.1/vb/Serialization.vb#1)]

### <a name="handling-time-zone-exceptions"></a>タイムゾーンの例外の処理

レジストリは動的な構造であるため、その内容は偶発的または意図的に変更される可能性があります。 これは、レジストリで定義され、アプリケーションを正常に実行するために必要なタイムゾーンが存在しない可能性があることを意味します。 タイムゾーンのシリアル化と逆シリアル化をサポートしていない場合は、 <xref:System.TimeZoneNotFoundException>アプリケーションを終了することによって、その結果を処理することはほとんどありません。 ただし、タイムゾーンのシリアル化と逆シリアル化を使用すると<xref:System.TimeZoneNotFoundException> 、シリアル化された文字列から必要なタイムゾーンを復元することで、予期しないを処理できます。この場合、アプリケーションは実行を続行します。

次の例では、カスタムの中部標準タイムゾーンを作成してシリアル化します。 次に、レジストリから中部標準時ゾーンを取得しようとします。 取得操作によって<xref:System.TimeZoneNotFoundException>またはが<xref:System.InvalidTimeZoneException>スローされた場合、例外ハンドラーはタイムゾーンを逆シリアル化します。

[!code-csharp[System.TimeZone2.Serialization.2#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Serialization.2/cs/Serialization2.cs#1)]
[!code-vb[System.TimeZone2.Serialization.2#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Serialization.2/vb/Serialization2.vb#1)]

### <a name="storing-a-serialized-string-and-restoring-it-when-needed"></a>シリアル化された文字列を格納し、必要に応じて復元する

前の例では、タイムゾーン情報が文字列変数に格納され、必要に応じて復元されています。 ただし、シリアル化されたタイムゾーン情報を含む文字列は、外部ファイル、アプリケーションに埋め込まれているリソースファイル、レジストリなど、一部のストレージメディアに格納することができます。 (カスタムタイムゾーンに関する情報は、レジストリ内のシステムのタイムゾーンキーとは別に保存する必要があることに注意してください)。

この方法でシリアル化されたタイムゾーン文字列を格納すると、タイムゾーン作成ルーチンもアプリケーション自体から分離されます。 たとえば、タイムゾーン作成ルーチンを実行して、アプリケーションが使用できる履歴タイムゾーン情報を含むデータファイルを作成できます。 その後、データファイルをアプリケーションと共にインストールすることができます。これを開くと、アプリケーションで必要になったときに1つ以上のタイムゾーンを逆シリアル化できます。

埋め込みリソースを使用してシリアル化されたタイムゾーンデータを[格納する例については、「方法:埋め込みリソース](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md)にタイムゾーンを保存[し、次の操作を行います。埋め込みリソース](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md)からタイムゾーンを復元します。

## <a name="see-also"></a>関連項目

- [日付、時刻、およびタイム ゾーン](../../../docs/standard/datetime/index.md)
