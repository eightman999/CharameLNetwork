# CharameLNetwork（Ourin 対応版）

macOS 向け伺かベースウェア [Ourin](https://github.com/eightman999/Ourin) で動かすための変更だけを `ourin` ブランチに置いています。
本体（辞書・スクリプト・ドキュメント）は upstream のままです。

- upstream: https://github.com/nikolat/CharameLNetwork.git
- 本体 DLL: `yaya.dll`（x86 の Windows コード。macOS では実行しない）
- 実行方法: Ourin 内蔵の YAYA エンジンが同梱辞書を動かす

## 変更内容

| ファイル | 内容 |
|---|---|
| `yaya.plugin/Contents/Info.plist` | Ourin が読み込む `.plugin`。`OurinPluginEngine=yaya` で内蔵エンジンを指定する。実行体は持たない |
| `ourin/build_nar.sh` | Ourin へインストールする NAR を作る |

Ourin は `descript.txt` の `filename` が `yaya.dll` のプラグインを読み込むときに同じ `.plugin` を自動生成するため、
この `.plugin` が無い upstream 版をそのまま入れても動きます。

## インストール

```bash
ourin/build_nar.sh
```

できた `build/yaya-ourin.nar` を Ourin のゴーストへドラッグ＆ドロップします。

## 動作確認

Ourin の yaya_core に、Ourin が送るのと同じ PLUGIN/2.0 要求を流した結果です（`version` / `installedghostname` / `OnGhostBoot` / `OnSecondChange` / `OnMenuExec`）。

```
== CharameLNetwork (dics=2, charset=UTF-8)
  load: ok=True loaded=2 err=None
  version: PLUGIN/2.0 200 OK | Sender: AYA | Charset: UTF-8 | Value: CharameLNetwork/0.5 |  | 
  installedghostname: PLUGIN/2.0 204 No Content | Charset: UTF-8 |  | 
  OnGhostBoot: PLUGIN/2.0 204 No Content | Charset: UTF-8 |  | 
  OnSecondChange: PLUGIN/2.0 204 No Content | Charset: UTF-8 |  | 
  OnMenuExec: PLUGIN/2.0 200 OK | Sender: AYA | Charset: UTF-8 | Event: OnCharameLNetwork | ScriptOption: nobreak,notranslate | Script: \![open,browser,file:////private/tmp/claude-501/-Users-eightman-dev-apps-Ourin/9f10ead0-e76c-4144-
```

Ourin 本体上での表示・操作の確認はまだです。

## ライセンス

upstream のライセンスに従います（upstream にライセンス表記はありません。再配布の前に作者へ確認してください）。
