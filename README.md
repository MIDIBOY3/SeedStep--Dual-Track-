# SeedStep -Dual Track-

ブラウザで動く、**“1音から育てる” 16ステップ・デュアルトラック・シーケンサー**。  
シンプルなパラメータだけで、**確率（CHANCE）×ランダム（RANGE）**を軸にフレーズを発展させていけます。

> シングルHTML（`index.html`）のみ。WebAudio + 純JS + CSS。ビルド不要。

---

## 主要機能

- **16-Step × 2トラック**
  - クリックで **ON/OFF**（ON=ソリッド、OFF=ストライプで視認性UP）
  - 再生中ステップはハイライト
- **グローバル Key / Scale**
  - 上部で **Key と Scale を共通管理**（両トラックに同時適用）
- **“育つ”ための確率とランダム**
  - **Global Chance（全体）**
  - **T-Chance（各トラックの全体確率）**
  - **Step Chance（各ステップ確率）**
  - **Range**（各トラックの音程ばらけ幅）
  - **Auto RND /16**：16ステップごとに音程を自動ランダム化（トグル）
  - **Rnd Notes Now**：即時ランダム化
  - ※グリッドの水色の強さ＝ **Global × Track × Step** の最終発音確率をリアルタイム可視化
- **“One-Note” から育てる**
  - **One-Note (both)**：両トラックを1音×ベタ打ちに初期化（チャンス類も100%に）
  - **One-Note A / B**：各トラックのみを初期化
- **演奏系**
  - **Tempo / Swing / Gate**
  - **Track Volume（各トラック）**、**Crossfader A⇄B**
  - **Waveform per track**（sine/triangle/saw/square）
  - **Filter per track**（Cutoff / Resonance(Q)）※リアルタイム反映
- **FX**
  - **Delay**（Mix / Time / Feedback）※Mixを上げると自動で配線＆有効化
  - **Reverb**（Mixのみ）※インパルスは簡易ノイズIRを動的生成
- **共有 / 保存**
  - **Permalink**（現在状態をURLハッシュに保存してコピー）
  - **Share to X**（Xに共有／クリックで新規タブ）
  - **Export MIDI**（Type-1、2トラック）
- **アクセシビリティ**
  - ステップのON/OFFを **色＋パターン（ソリッド/ストライプ）**で区別（色覚配慮）

---

## クイックスタート

### 1) ローカルで開く
1. このリポジトリをダウンロード（`index.html` だけでもOK）
2. ブラウザで `index.html` を開く
3. ページどこかをクリック → **Start**（自動再生制限の解除のため）

### 2) GitHub Pages で公開
1. GitHub のリポジトリに `index.html` を置く（ルートでOK）
2. **Settings → Pages**  
   - Source: `Deploy from a branch`  
   - Branch: `main` / `/ (root)` → **Save**
3. 数十秒〜数分後に公開URLが発行されます
4. 変更を反映したいときは `index.html` を上書き commit →  
   **キャッシュ回避**のため、URL に `?v=2025-08-08` のようなクエリを付けてリロード

---

## 操作メモ

- **テンポ / スウィング / ゲート**：上部グローバルセクション
- **Key / Scale**：グローバル（両トラック共通）
- **Range**：各トラックの音程ランダム幅（±半音段階、スケール度数にマップ）
- **Auto RND /16**：ループ境界（16ステップ）で毎回ランダム化
- **Rnd Notes Now**：今すぐランダム化
- **T-Chance**：トラック全体の発音確率（0–200%）
- **Step Chance**：選択ステップ個別の発音確率（0–100%）
- **Crossfader**：AとBをブレンド（コンスタントパワー）
- **Vol**：各トラックの出力レベル
- **Filter**：Cutoff / Q をリアルタイムで適用
- **Delay / Reverb**：Mixを上げると自動でノード生成＆配線（初期はオフ）
- **Permalink**：現状態をURLにエンコードしてクリップボードへ
- **Export MIDI**：現在のパターンをType-1でダウンロード

---

## 仕様メモ（テクニカル）

- **音源**：WebAudio の `OscillatorNode` ×2（軽いデチューン）→ `Gain` → `BiquadFilter` → TrackGain → Master
- **Swing**：偶数ステップを遅延（0–75%）
- **Gate**：各ステップ長の割合（Tie/Slideで時間延長／スライドは線形）
- **確率適用**：`Global × Track × Step` の積を**最終確率**として `seed` ベースの擬似乱数と比較
- **ランダムノート**：`Range` を±幅としてスケール度数をオフセット（`deg2semi` → MIDI）
- **MIDI**：PPQ=480、1ステップ=PPQ/4 の扱い。テンポ/拍子のメタ含む

---

## よくあるトラブルと対処

### 「音が出ない」
- ページを一度**クリック**してから **Start**（自動再生制限）
- **Crossfader=0（中央）**、**Vol(A/B)>0**、**Gate>5%**、**Chance類>0%**を確認
- ブラウザのタブが **ミュート** になっていないか
- **iOS/Safari** では省電力設定やサイレントスイッチに影響されることがあります
- まだダメなら **DevTools → Console のエラー**を確認

### 「ステップが表示されない / ボタンが効かない」
- キャッシュをクリア or URLに `?v=xxxx` を付与してハードリロード
- Console にエラーが出ていないか確認（JSが途中で止まるとUIが出ません）

### 「FXが効かない」
- **Mix** を上げると自動でノード生成＆配線されます（0%のままだとオフ）

---

## ディレクトリ構成

```
.
├── index.html   # 単体で動作。ここにすべて含まれています
└── README.md    # このファイル
```

---

## ライセンス

MIT License。自由にフォーク／改変OK。クレジット表記は任意です。

---

## 変更履歴（要点）

- 2025-08-08: グローバル Key/Scale、トラックAuto-RND、Rnd Now、T-Chance可視化、Filterリアルタイム、アクセシビリティ配慮、MIDI/共有まわり整理、数件の初期化タイミングバグを修正。
