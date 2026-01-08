# Succulent Binary Classifier (Prototype)

iPhoneで撮影した植物画像を入力として、  
**多肉植物（succulent） / それ以外（other）** の2クラスに分類する  
深層学習（Deep Learning）プロトタイプです。

PyTorch を用い、ImageNetで事前学習された **MobileNetV3** を  
転移学習（Transfer Learning）して分類を行います。

---

## 使用技術
- Python 3.10 / 3.11
- PyTorch
- timm（事前学習モデル）
- MobileNetV3（軽量CNN）

---

## 環境構築
```bash
pip install torch torchvision timm pillow


データセット構成

学習用画像は以下の構造で配置します。
フォルダ名がクラスラベルとして使用されます。

dataset/
 ├─ succulent/   # 多肉植物の画像
 └─ other/       # それ以外の植物の画像


※ iPhoneで撮影した高解像度画像（3024×4032）でも問題ありません
（内部で224×224にリサイズして学習します）

学習（Training）

以下を実行すると学習が開始されます。

python train.py


学習後、以下のファイルが生成されます。

succulent_binary.pt
→ 学習済みモデルの重み

succulent_binary_meta.json
→ クラス名などのメタ情報

推論（Prediction）

predict.py 内の IMAGE_PATH を判定したい画像に変更し、実行します。

python predict.py


出力例：

pred_class: succulent
probabilities:
  succulent: 0.88
  other: 0.12
