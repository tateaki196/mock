# マレビト（仮）紙芝居 — 公開と停止の手順

URL：https://tateaki196.github.io/mock/ （検索避けの設定済み。URL を知っている人は誰でも開けるので、伝える相手を限る）

## 公開する・止める（GitHub の画面だけで済む）

1. https://github.com/tateaki196/mock/actions を開く
2. 左の「mock の公開・停止」→ 右の「Run workflow」
3. 「公開」か「停止」を選ぶ
   - 公開のときだけ、止める日（例 `2026-11-30`）を入れられる。入れるとその日の 0:10（日本時間）に自動で止まる。空なら止めない
4. 緑の「Run workflow」を押す。1〜2分で切り替わる（URL は変わらない）

いまの状態は、このリポジトリの `state.json`（`mode`＝公開／停止、`stop_date`＝止める日）で分かる。

## 資料を直したあと、紙芝居を新しくする（手元の PC で）

```
python scripts/publish_mock.py
```

ikusei リポジトリのルートで実行する。`docs/ikusei_mvp_dev.html` から組み立て直してここへ送る。
公開中なら新しい紙芝居で出し直され、停止中なら停止のまま。組み立ての結果は `logs/mock_kamishibai_report.md`。

## 最初に一度だけ（済んでいれば不要）

- GitHub で `tateaki196/mock` を Public で作る（中身は空でよい）
- Settings → Pages → Build and deployment の Source を「GitHub Actions」にする
- 手元で `python scripts/publish_mock.py` を1回実行（初回は「停止」の状態で始まる）→ 上の手順で「公開」

## 注意

- 自動で止める見回りは、リポジトリに60日動きが無いと GitHub が止めることがある。Actions の画面に黄色い帯が出たら「Enable workflow」を押す
- このリポジトリのファイルは手元の `scripts/mock_pages_repo/` と `out/mock/` から写したもの。ここで直接直さない
