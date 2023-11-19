# review-az-204

## refs

- https://learn.microsoft.com/ja-jp/training/modules/choose-azure-service-to-integrate-and-automate-business-processes/2-identify-technology-options
- https://learn.microsoft.com/ja-jp/training/modules/create-serverless-logic-with-azure-functions/2-decide-if-serverless-computing-is-right-for-your-business-need
- https://learn.microsoft.com/ja-jp/training/modules/create-serverless-logic-with-azure-functions/3-create-an-azure-functions-app-in-the-azure-portal?pivots=javascript

## ワークフロー

- データまたはファイルの **入力**
- データを変更するなどの **アクション** の実行
- **条件** の設定
- データまたはファイルの **出力**

ワークフローを構築して実行するために使用できるテクノロジ

- **Logic Apps**
  - ワークフローを描画できる UI がある **デザイン優先テクノロジ**
  - 200 を超える外部サービスへのインターフェイスを提供する **コネクタ**
    - Twitter コネクタ
    - Office 365 Outlook コネクタ
    - その他、独自のコネクタを作成可能 
- **Microsoft Power Automate**
  - **デザイン優先テクノロジ**
  - 4 種類のフロー
    - 自動
    - ボタン
    - スケジュール済み
    - ビジネスプロセス
  - Logic Apps が基になっており、 **Logic Apps と同じコネクタとアクションをサポート** 
- **WebJobs**
  - ビジネスプロセスの一部としてカスタムコードを記述する **コード優先テクノロジ**
  - **Azure App Servie** の一部
  - ユーザが自転車の写真をアップロードしたら、小さいサムネイル写真を生成するなどの処理を実行
  - 2 種類の WebJobs
    - **継続的** : 共有フォルダで新しい写真をチェックする場合
    - **トリガー** : イベント、スケジュール、手動で実行する場合
  - シェルスクリプト、PHP、Python、Java、Javascript、.NET フレームワーク、C# などの .NET 言語 でプログラム作成
  - SDK は C# をサポート
- **Azure Functions**
  - **コード優先テクノロジ**
  - **ホストを気にすることがない**
  - C#、Java、JavaScript、PowerShell、Python、または任意の言語で作成可能
  - 様々なテンプレート
    - HTTPTrigger: HTTP リクエストに対する応答でコードを実行
    - TimerTrigger: スケジュールでコードを実行
    - BlobTrigger: Azure ストレージアカウントに新しい BLOB が追加されたら実行
    - CosmosDBTrigger: NoSQL データベースで新規、更新されたら実行
  - 規定で 5 分のタイムアウト。最大 10 分に設定できる。10 分以上は VM 上にホストすることで可能。ただし、HTTP リクエストでトリガーされた場合に値をレスポンスに含める場合はタイムアウトは 2.5 分。Durable Functions オプションを使用するとタイムアウトなし （ **Dedicated(App Service) プラン?** ）。
  - 10 秒ごとにインスタンスを 1 つ作成でき 200 まで作成できる。
  - 動的スケーリングは **Premium プラン** 。
  - **ストレージアカウントが必要** 。従量課金プランでは、コードなどが格納される。〓他のプランでは？〓
  - `function.json` でバインドする。
  - API キーは `x-functions-key` などで渡して実行
 
**デザイン優先テクノロジの比較**

非技術スタッフが使うには Microsoft Power Automate。

<img width="867" alt="スクリーンショット 2023-11-19 16 21 01" src="https://github.com/yhor1e/review-az-204/assets/10266230/14b947a4-4f7e-4e04-9bef-520593660502">

**コード優先テクノロジの比較**

Azure Functions の方がホストを気にする必要がなかったり、自動スケーリングなど管理が簡単で対応言語が多い。
ただし、すでに App Service が動作していてその一部として管理したい場合、
コードをトリガするイベントをリッスンするオブジェクトをより細かく制御する必要がある場合は WebJobs。

<img width="868" alt="スクリーンショット 2023-11-19 16 50 21" src="https://github.com/yhor1e/review-az-204/assets/10266230/e26778d0-ff5b-49d7-94dd-97e51c20798a">
