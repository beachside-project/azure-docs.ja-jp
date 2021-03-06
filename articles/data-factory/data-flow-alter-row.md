---
title: マッピング データ フローでの行の変更変換
description: マッピング データ フローで行の変更変換を使用してデータベースのターゲットを更新する方法
author: kromerm
ms.author: makromer
ms.reviewer: daperlov
ms.service: data-factory
ms.topic: conceptual
ms.custom: seo-lt-2019
ms.date: 04/20/2020
ms.openlocfilehash: 6b353967c9b9c7517f1a42581717c6394c0e6374
ms.sourcegitcommit: 849bb1729b89d075eed579aa36395bf4d29f3bd9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "81729133"
---
# <a name="alter-row-transformation-in-mapping-data-flow"></a>マッピング データ フローでの行の変更変換

[!INCLUDE[appliesto-adf-asa-md](includes/appliesto-adf-asa-md.md)]

行の変更変換を使用して、行の挿入、削除、更新、アップサート ポリシーを設定します。 一対多の条件を式として追加できます。 各行は一致する最初の式に対応したポリシーでマークされるので、これらの条件は優先度の順に指定する必要があります。 これらの条件によってそれぞれ、行が挿入、更新、削除、アップサートされます。 行の変更では、ご利用のデータベースに対して DDL と DML の両方を生成できます。

![行の変更の設定](media/data-flow/alter-row1.png "行の変更の設定")

行の変更変換は、自分のデータ フローのデータベース シンクまたは Cosmos DB シンクでのみ動作します。 行に割り当てるアクション (挿入、更新、削除、upsert) は、デバッグ セッション中に発生することはありません。 データ フローの実行アクティビティをパイプラインで実行し、データベース テーブルに行の変更ポリシーを適用します。

## <a name="specify-a-default-row-policy"></a>既定の行ポリシーを指定する

行の変更変換を作成し、`true()` の条件を持つ行ポリシーを指定します。 以前に定義された式のいずれにも一致しない行はそれぞれ、指定された行ポリシー用にマークされます。 既定では、どの条件式にも一致しない行はそれぞれ、`Insert` 用にマークされます。

![行の変更ポリシー](media/data-flow/alter-row4.png "行の変更ポリシー")

> [!NOTE]
> すべての行を 1 つのポリシーでマークするには、そのポリシーの条件を作成し、条件を `true()` として指定します。

## <a name="view-policies-in-data-preview"></a>データのプレビューでポリシーを表示する

[デバッグ モード](concepts-data-flow-debug-mode.md)を使用して、[データのプレビュー] ペインで行の変更ポリシーの結果を表示します。 行の変更変換のデータのプレビューでは、ターゲットに対する DDL または DML アクションは生成されません。

![行の変更を行う複数のポリシー](media/data-flow/alter-row3.png "行の変更を行う複数のポリシー")

挿入、更新、upsert、または削除アクションが発生するかどうかを示すアイコンによって、それぞれの行の変更ポリシーが表されます。 上部ヘッダーは、プレビューの各ポリシーによって影響を受ける行数を示しています。

## <a name="allow-alter-row-policies-in-sink"></a>シンクで行の変更ポリシーを許可する

行の変更ポリシーを機能させるには、データ ストリームがデータベースまたは Cosmos シンクに書き込む必要があります。 シンクの **[設定]** タブで、そのシンクで許可する行の変更ポリシーを有効にします。

![行の変更のシンク](media/data-flow/alter-row2.png "行の変更のシンク")

既定の動作では、挿入のみが許可されます。 更新、upsert、または削除を許可するには、その条件に対応する、シンクのチェックボックスをオンにします。 更新、upsert、または削除が有効になっている場合は、シンク内のどのキー列を照合するかを指定する必要があります。

> [!NOTE]
> 挿入、更新、または upsert によりシンクのターゲット テーブルのスキーマが変更される場合、データ フローは失敗します。 データベース内のターゲット スキーマを変更するには、テーブル アクションとして **[Recreate table]\(テーブルの再作成\)** を選択します。 これにより、新しいスキーマ定義でご利用のテーブルがドロップされ、再作成されます。

シンク変換では、一意の行 ID を表す 1 つのキーまたは一連のキーがターゲット データベースに必要です。 SQL シンクの場合、それらのキーの設定は、シンク設定タブで行います。CosmosDB の場合は、それらの設定にパーティション キーを設定したうえで、CosmosDB のシステム フィールド "id" をシンクのマッピングで設定します。 CosmosDB で update、upsert、delete を行う場合は、システム列である "id" を含める必要があります。

## <a name="data-flow-script"></a>データ フローのスクリプト

### <a name="syntax"></a>構文

```
<incomingStream>
    alterRow(
           insertIf(<condition>?),
           updateIf(<condition>?),
           deleteIf(<condition>?),
           upsertIf(<condition>?),
        ) ~> <alterRowTransformationName>
```

### <a name="example"></a>例

以下の例は、受信ストリーム `SpecifyUpsertConditions` を受け取り、行の変更条件を 3 つ作成する、`CleanData` という行の変更変換です。 前の変換では、データベース内で行の挿入、更新、削除を実行するかどうかを決定する `alterRowCondition` という列が計算されます。 列の値に、行の変更ルールと一致する文字列値が含まれている場合、そのポリシーが割り当てられています。

Data Factory UX では、この変換は次の図のようになります。

![行の変更の例](media/data-flow/alter-row4.png "行の変更の例")

この変換のデータ フロー スクリプトは、次のスニペットに含まれています。

```
SpecifyUpsertConditions alterRow(insertIf(alterRowCondition == 'insert'),
    updateIf(alterRowCondition == 'update'),
    deleteIf(alterRowCondition == 'delete')) ~> AlterRow
```

## <a name="next-steps"></a>次のステップ

行の変更変換の後に、[自分のデータと配布先データ ストアをシンク](data-flow-sink.md)する必要がある場合があります。
