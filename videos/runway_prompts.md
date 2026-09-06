# Runway生成プロンプト

サイトの2つの動画枠に対応。生成後、同じファイル名で `videos/` フォルダに保存すれば自動で反映されます。

## 1. hero-bg.mp4（トップのヒーロー背景・ループ用）

- 用途: ページ最上部、テキストの背景でずっとループ再生
- 推奨: 16:9、5〜10秒、音声なし、ループしても違和感のない始点/終点
- 生成方法: Image to Video（`images/lp.pic1.jpg` を開始フレームにすると内装トーンが揃いやすい）

```
Slow, cinematic dolly-in shot through an upscale Japanese hostess lounge (kyabakura)
in Shibuya at night. Warm gold and deep crimson ambient lighting, soft bokeh from
chandeliers, plush velvet booths, subtle lens flare. Elegant, luxurious, calm mood.
Camera drifts forward very slowly, shallow depth of field, no visible people's faces,
no text, no logos. Seamless loopable motion.
```

- ネガティブ/避けたい要素: テキスト、ロゴ、顔のクローズアップ、激しいカメラ揺れ

## 2. venue-highlight.mp4（MOVIEセクション・店内紹介ムービー）

- 用途: 「お店の雰囲気をムービーで」セクションの再生ボタン付き動画
- 推奨: 16:9、15〜30秒程度（複数クリップを繋ぐ場合は各5〜10秒を数本生成して編集で結合）
- 生成方法: Image to Video（`images/lp.pic2.jpg` や `lp.pic3.jpg` を開始フレームに）

```
A sequence of elegant, cinematic shots inside a high-end Shibuya hostess lounge at
night: glasses of champagne catching gold light, a softly lit bar counter, warm
ambient lighting reflecting off velvet interiors, gentle camera pans and slow zooms.
Sophisticated, inviting, slightly moody atmosphere. No visible faces, no text overlays.
```

- 複数カット生成する場合の分割案:
  1. 入口〜内装の全体感（ゆっくりパン）
  2. カウンター・グラスのクローズアップ（スローズーム）
  3. 照明・空間の雰囲気カット（静かなドリー）
- 編集時: 各カットをフェードで繋ぎ、最後にロゴ/店名テロップを軽く重ねると仕上がりが良くなります。

## 共通の注意点

- Runwayの生成物は著作権・利用規約上、商用LP掲載前に規約を確認してください。
- 出力後は `.mp4`（H.264）でエクスポートし、可能なら圧縮（HandBrake等）してから配置するとページの表示速度が保てます。
- ファイルを置く場所: `C:\Users\kimuk\projects\taka_test\videos\`
  - `hero-bg.mp4`
  - `venue-highlight.mp4`
