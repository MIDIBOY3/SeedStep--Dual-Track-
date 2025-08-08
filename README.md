# Mini Sequencer — Dual Track (Browser)

**2トラック**・**16ステップ**のブラウザシーケンサー／ミニシンセ。  
**Chance / Range / Velocity / Accent / Tie / Slide / Filter / Delay / Reverb / Waveform / Crossfader / Per-Track Volume / MIDI書き出し / Permalink / Xシェア**。  
Chrome/macOSでも鳴る「安全設計（ドライ常時直結／FX遅延生成）」です。

## 追加点（この版）
- 各トラックの**音量**（Vol）＋**クロスフェーダー**（A⇄B）
- 各トラックの**波形**選択（sine / triangle / sawtooth / square）
- 各トラックの**トラックChance**（T-Chance）…Global×Track×Stepの乗算で最終確率を決定
- 各トラックの**One-Noteボタン**（One-Note A / B）：そのトラックだけを1音ベタ打ちに初期化（Range=0, Step Chance=100, Track Chance=100）
- グリッドの**高コントラスト化**：ON＝明るい塗り＋●、OFF＝暗色ストライプ＋○
- FX配線の安定化：ミックスを上げた時にノード生成＆**トラックからFXへ明示的に接続**

## 使い方（要点）
- どこかをクリック → **Start**。右上 `Audio: running` を確認。
- **One-Note (both)** で両トラック、**One-Note A/B** で片方だけを初期化できます。
- **T-Chance**：各トラックの確率ゲイン。**Global Chance × T-Chance × Step Chance** が最終確率。

## デプロイ（GitHub Pages）
1. この `index.html` をリポジトリ直下にアップロードしてコミット（置き換えOK）。
2. Settings → Pages → Source: Deploy from a branch（Branch: `main`, Folder: `/ (root)`） → Save
3. 数十秒後、表示されたURL（`https://<user>.github.io/<repo>/`）で確認。反映されない場合はハードリロード。

---

© 2025 — Built for quick musical sketching.
