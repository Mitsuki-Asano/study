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
