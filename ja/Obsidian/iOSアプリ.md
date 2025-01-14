iOS版アプリは現在一般に公開されており、 https://obsidian.md/mobile からAppストアのリンクにアクセスできます。

## 保管庫はどこに保存されますか？

iCloudで保管庫の保存を行う場合には、保管庫のデータは"Obsidian"という名前のアプリケーションフォルダの直下にあるiCloud Driveアカウント内フォルダに保存されることになります。アプリケーションフォルダはObsidianのロゴアイコンで表示されています。

iCloudでの同期を行わない場合には、保管庫はObsidianアプリのサンドボックスファイルシステムに保存されます。ローカル保管庫はファイルシステムを介したフォルダ選択をサポートしている他のアプリからアクセスできます。例えば、Working CopyのようなアプリはObsidianのローカル保管庫の同期に使用できます。

==保管庫をローカルに保存することを選択した場合には、Obsidianのアプリをアンインストールする際にiOSによって保管庫は自動的に削除されてしまうことに注意してください。==

## 同期

### クイックスタート

すでにデスクトップに保管庫を所有している場合には、モバイル版に保管庫を同期してアクセスするのに2つの方法があります。

- [[#iCloud Driveによる同期]]
- [[#Obsidian Syncによる同期]]

公式で現在サポートされている2つの同期方法はiCloudとObsidian Syncです。
Working Copy(git)はiOS版Obsidianでテスト済みの代替的な同期方法です。

現在、iOSでは次の同期サービスについてサポート情報が**ありません**。
- Dropbox
- Google Drive
- OneDrive
- Syncthing

iOSでのObsidianについて上記のサービスを利用して同期する方法を見つけた場合には、Discordサーバーに参加していただきセットアップのやり方を教えていただけるとありがたいです。

理論上はデバイス上の特定フォルダをバックグラウンドで同期が可能なサードパーティの同期サービスプロバイダーであれば、2つの同期方法と同様に上手く機能するはずですが、Working Copyを除いてあらゆるサービスが実際に機能するかどうかについては認識していません。これはiOSアプリ間でのファイル共有が高度に複雑な仕組みとなっており、その制約があるためです。すべてのアプリがアクセス可能なパブリックフォルダを提供しているAndroidの場合とは異なります。このため、多くのサードパーティの同期サービスプロバイダーはiOSでのバックグラウンド同期に関する適切な実装を行っていません。

現在、ObsidianはFileProviderを介して仮想ファイルシステムを提供するサードパーティの同期サービスプロバイダーに対しての直接的なサポートは行っていませんが、将来的には機能向上としてこの問題の解決を試みる予定です。

### Obsidian Syncによる同期

下に示したように、Androidでの同期と同様のステップに従うことで同期できます。現在、Obsidian Syncによる同期とiCloudによる同期の両方を同時に使用することは推奨していません。同時使用によって[[Obsidian Sync#サードパーティの同期サービス|競合状態]]によるデータ損失の発生が報告されています。

![[Androidアプリ#Obsidian Syncによる同期]]

### iCloud Driveによる同期

iCloud Driveを介した**新規**保管庫の同期セットアップ

1. アプリを起動して、｢Create a new vault｣を選択する
2. デスクトップで、｢別の保管庫を開く｣コマンドを使用してiCloud内の新規保管庫のロケーションを指定する

iCloud Driveを介した**すでに存在している**保管庫の同期セットアップ

1. アプリを起動して、｢Create a new vault｣を選択する
2. [[Obsidian URIの利用|保管庫間URI]]が機能するように保管庫にデスクトップの保管庫と同じ名前を付ける
3. iCloudから空のフォルダがデスクトップに同期されるのを待つ
4. この空のフォルダに保管庫に存在するすべてをコピー＆ペーストする
5. デスクトップで、｢別の保管庫を開く｣コマンドを使用してiCloud内の新規保管庫のロケーションを指定する
6. iCloudからモバイルデバイスにすべてが同期されるのを待つ

### Working Copy

iOSでの代替手段として、保管庫の同期を行うためにWorking CopyをセットアップしてGitを利用することも可能です。これを行うためには、まず最初にデバイス上に空のローカル保管庫を作成し、｢フォルダー同期のセットアップ｣を行った後にObsidianのアプリ内部でローカル保管庫を選択してください。これによって、手動でのコミットとプッシュが可能になります。

# サードパーティの同期サービスのサポート

モバイル版Obsidianではなぜ他の同期方法をサポートしていないのかと多くのユーザーから質問されますが、現在のモバイル同期サポートの状況に対する簡単な説明をここに記載しておきます。

Obsidianが1WriterやiA Writerといった他のアプリと異なる部分の一つとしては、単一のノートというよりはむしろ保管庫のトップで機能するということが挙げられます。オートコンプリートや画像埋め込み、タグペイン、バックリンク、そしてすべてのノート間機能などのObsidianが有するコア機能の多くは、保管庫全体とその内部に存在するすべてのファイルに依存しているからです。

対照的に、多くのマークダウン編集アプリは単純に単一のノートを**開き**、ユーザーに編集させ、ノートをバックグラウンドで保存するような仕組みになっています。これによって、OSとサードパーティの同期サービスプロバイダーは通常、保管庫(サブフォルダを持ちうるフォルダやファイル群)を扱うというよりはむしろ、単一ファイルに対してのアクセスや作業のためのAPIを提供するのみとなっています。

標準的なマークダウンエディタのアプリでは、同期のために**選択したファイルを開いた際にファイルをダウンロード**と**保存を行った際にファイルをアップロードして戻す**という基本機能を実装しているのみとなっています。Obsidianでは利便性と共に、変更があった全ファイル(例えば、ファイルのリネームを実行した際には、他のファイルに存在するリンク名が変更されるためにそれら一連のファイルを更新するなどの可能性があります)に対しての追跡を維持するため、保管庫全体をダウンロードする必要があります。その上で、同期ソリューションを介して変更を監視し、ファイル変更の際には内部キャッシュを更新して正確なリンクを提供する方法が必要となってきます。

それらすべてをサードパーティの同期サービスプロバイダーが維持するというのは、かなり大変です。これが、多くの同期サービスプロバイダーがモバイル用に適切な同期クライアントを開発せず、ユーザーがサードパーティのアプリ(DropSyncやFolderSyncなど)を使用しているという事の理由の一つとなっています。残念ながら、iOSではそのようなアプリはサンドボックスがあるために存在しえないのです。

## 既知の問題

### macOSにおけるiCloudフォルダでの問題

macOSのFinderを使用してiCloud上のフォルダへファイルをドラッグ＆ドロップできない場合には、 https://obsidian.md からこの問題を修正したデスクトップ版Obsidianの最新リリースをダウンロードしてください。インストールが完了するとアプリの実行によって自動的にiCloudのフォルダパーミッションを更新します。この方法がうまくいかない場合にはマシンを再起動する必要があるかもしれません。

### ペーストメニューが表示されないことがある

一部のユーザーからカーソルをタップしてもペーストメニューが表示されないという問題が報告されています。その問題が起こる場合の回避策としては、三本指のタップジェスチャを使用してグローバル編集メニューを開き、そこからテキストへのペーストを行うことができます。