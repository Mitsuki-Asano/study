# Succulent Binary Classifier (Prototype)

## 目的
本プロジェクトは、撮影した植物画像を入力として、  
**多肉植物（succulent）/それ以外の植物（other）** の2クラスに自動分類する  
深層学習モデルを構築することを目的とする。

少量のデータでも学習が可能な **転移学習（Transfer Learning）** を用い、  
将来的なスマートフォンアプリへの展開を見据えた軽量モデルを採用している。

---

## 使用技術
- Python
- PyTorch
- torchvision
- timm
- MobileNetV3
- Pillow

---

## 環境構築
以下のコマンドで必要なライブラリをインストールする。

```bash
pip install torch torchvision timm pillow
```

---

## データセット構成
学習用画像は以下のフォルダ構造で配置する。
フォルダ名がそのままクラスラベルとして使用される。

```
dataset/
 ├─ succulent/   # 多肉植物の画像
 │   ├─ img_001.jpg
 │   ├─ img_002.jpg
 │   └─ ...
 └─ other/       # それ以外の植物の画像
     ├─ img_101.jpg
     ├─ img_102.jpg
     └─ ...
```
画像は高解像度画像でも問題ない

学習時に自動的にリサイズされ、モデル入力サイズ（224×224）に変換される

---

## 学習（Training）
以下のコマンドを実行すると、モデルの学習が開始される。

```bash
python train.py
```
### 学習の流れ
1.データセットを読み込む

2.学習用データと検証用データに分割

3.画像前処理およびデータ拡張を適用

4.事前学習済み MobileNetV3 を用いた転移学習を実施

5.検証精度が最も高いモデルを保存

出力ファイル
学習完了後、以下のファイルが生成される。
```
succulent_binary.pt(学習済みモデルの重み)
```

```
succulent_binary_meta.json(クラス名・画像サイズなどのメタ情報)
```

---

## 推論（Prediction）
学習済みモデルを用いて、画像1枚を分類する。

実行方法
predict.py 内の IMAGE_PATH を判定したい画像のパスに変更し、以下を実行する。

```bash
python predict.py
```

### 推論の流れ
1.学習済みモデルおよびメタ情報を読み込み

2.入力画像を学習時と同じ前処理で変換

3.モデルに画像を入力して推論

4.各クラスの確率を算出し、最も高いものを出力

出力例
```
pred_class: succulent
probabilities:
  {'succulent': 0.88,'other': 0.12}
```





