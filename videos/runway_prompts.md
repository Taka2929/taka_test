# 動画 再生成ガイド（Runway / DeeVid AI 共通）

サイトの2つの動画枠に対応。生成後、**同じファイル名**で `videos/` フォルダに保存すれば
コード側の変更なしでそのまま反映されます。

## ⚠️ 前回の出力で直すべき2点（最優先）

1. **透かし（ウォーターマーク）を消す**
   - DeeVid AIは無料/一部プランだと右上にロゴが焼き込まれます。有料プランの
     "No watermark" / "透かしなし" 出力オプションを有効にしてください。
   - Runwayを使う場合はロゴは基本入りませんが、プラン・出力設定を一応確認してください。

2. **アスペクト比を16:9（横長）に固定する**
   - 前回は640×640（正方形）と544×736（縦長）で出力されており、サイト側で
     `object-fit: cover` により上下・左右が大きくトリミングされてしまいます。
   - 生成画面で **Aspect Ratio / 画面比率を「16:9」または「Landscape」に明示的に選択**してから
     生成してください（デフォルトのままだと縦型SNS用の9:16になっていることが多いです）。

3. **（venue-highlight.mp4のみ）ポートレート写真からのモーフィングは避ける**
   - 前回は「女性の顔写真」→「シャンパングラス」に変形する演出になっており、
     途中に白い帯状のノイズ（グリッチ）が映り込んでいました。
   - 人物写真を起点にせず、**店内の1シーンだけを撮る/動かす**プロンプトにしてください
     （下記プロンプト参照）。複数カットが欲しい場合は、シーンごとに別々に生成してあとで繋ぐ
     （＝1回の生成で変形させない）のがコツです。

---

## 1. hero-bg.mp4（トップのヒーロー背景・ループ用）

- 用途: ページ最上部、テキストの背景でずっとループ再生
- 設定: **16:9 / Landscape**、5〜10秒、音声なし、ループしても違和感のない始点/終点
- 生成方法: Text to Video、またはImage to Video（人物ではなく内装・什器の写真を起点に）

```
Slow, cinematic dolly-in shot through an upscale Japanese hostess lounge (kyabakura)
in Shibuya at night. Warm gold and deep crimson ambient lighting, soft bokeh from
chandeliers, plush velvet booths, subtle lens flare. Elegant, luxurious, calm mood.
Camera drifts forward very slowly, shallow depth of field, no visible people's faces,
no text, no logos, no watermark. Seamless loopable motion. Landscape 16:9 framing.
```

- ネガティブ/避けたい要素: テキスト、ロゴ、透かし、顔のクローズアップ、激しいカメラ揺れ、縦型構図

## 2. venue-highlight.mp4（MOVIEセクション・店内紹介ムービー）

- 用途: 「お店の雰囲気をムービーで」セクションの再生ボタン付き動画
- 設定: **16:9 / Landscape**、1カット5〜10秒（複数カット欲しい場合は下記のように分けて別々に生成）
- 生成方法: Image to Video（内装・グラス・カウンターなど「モノ」の写真を起点に。人物写真は起点にしない）

```
A single continuous cinematic shot inside a high-end Shibuya hostess lounge at night:
champagne glasses catching warm gold light on a softly lit bar counter, ambient
lighting reflecting off velvet interiors, a gentle slow camera pan or slow zoom.
Sophisticated, inviting, slightly moody atmosphere. No people, no faces, no text
overlays, no watermark, no morphing or scene transition. Landscape 16:9 framing.
```

- 複数カットが欲しい場合は、上のプロンプトの被写体部分（グラス→内装全体→照明）だけを変えて
  **1シーン1生成**で3本作り、編集ソフト（CapCut / Premiere等）でフェード編集して1本のmp4に
  書き出してから `venue-highlight.mp4` として配置してください。

---

## 共通の注意点

- 生成AIの利用規約・商用利用条件を確認してから公開してください（DeeVid AI / Runwayとも規約は要確認）。
- 出力後は `.mp4`（H.264）でエクスポート。可能なら圧縮（HandBrake等）してから配置すると表示速度が保てます。
- ファイルを置く場所: `C:\Users\kimuk\projects\taka_test\videos\`
  - `hero-bg.mp4`
  - `venue-highlight.mp4`
- 配置後、私に一声かけていただければ、解像度・透かし・アスペクト比を確認した上でpush・公開まで対応します。
