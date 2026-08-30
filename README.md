# P.A.W Runtime Metadata

P.A.WがComfyUIとの互換性を確認するための公開メタデータです。
P.A.W本体のソースコード、生成内容、ユーザー設定は含まれていません。

## リリース時の確認

新しいP.A.W versionを配布する場合は、次の確認を完了してから公開してください。通常の無関係なコミットで毎回メタデータを変更する必要はありません。

- `comfyCompatibilityManifest.json` の `verified`／`pawVersions` には、実機で確認済みの組合せだけを登録する。未検証の最新版は `verified` にしない。
- 同じ検証済み組合せを、P.A.W本体の同梱マニフェストにも登録する。
- P.A.W本体リポジトリとこの公開リポジトリの両方でリリースコミットとpushを完了し、公開ファイルの配信反映を確認する。公開側の反映が未確認ならリリース完了としない。
- 配布前に、認証なしで [公開rawマニフェスト](https://raw.githubusercontent.com/fumipon-studio-dev/paw-runtime-metadata/main/comfyCompatibilityManifest.json) を取得してHTTP 200とJSON妥当性を確認する。P.A.W本体の現行 `package.json` の `version` を使って `findLatestVerifiedComfyCompatibility` が期待する検証済み版を選べることも確認する。
- 互換性情報はプロセス内で最大1時間キャッシュされるため、公開反映確認後にP.A.Wを完全終了して再起動し、再取得する（1時間待つ必要はない）。その後、クリーンな初回セットアップを実機で確認する。これは公開反映確認とは別の必須確認である。

今回は自動hookを追加せず、この手順でリリースを確認します。アプリは公開マニフェストの取得に成功すると同梱マニフェストから公開版へ切り替えるため、公開側の登録漏れを同梱版で補うことはできません。
