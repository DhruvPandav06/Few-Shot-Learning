# 🐾 Learning from Less: Few-Shot Image Classification Using Transfer Learning

## 📌 Overview
This project investigates how image classification accuracy changes when models are trained with **limited labeled data**.  
We compare three **ImageNet-pretrained models** (ResNet18, MobileNetV3-Large, EfficientNet-B0) against a **CNN trained from scratch** on five pet breeds from the Oxford-IIIT Pet dataset.

---

## 🎯 Objective
- Research Question: *How does image-classification performance change when models are trained with few labeled images?*  
- Approach: Compare pretrained transfer-learning models vs. scratch CNN across multiple few-shot settings (5, 10, 25, 50, 100 images per class) and a full-data baseline.

---

## 📂 Dataset
- **Source**: Oxford-IIIT Pet dataset  
- **Classes**: Abyssinian, Bengal, Persian, Pug, Siamese  
- **Custom Split**: 70% training (697), 15% validation (150), 15% test (150)  
- Few-shot subsets sampled from training set.

---

## ⚙️ Methodology
### Models
- **ResNet18** – residual connections, deep CNN backbone  
- **MobileNetV3-Large** – efficient, lightweight, depthwise separable convolutions  
- **EfficientNet-B0** – compound scaling, MBConv blocks  
- **Custom CNN (scratch)** – 4 conv blocks + FC layer, 26M trainable parameters  

### Training Setup
- Input size: 224×224  
- Batch size: 16  
- Optimizer: Adam (lr=0.001)  
- Epochs: 10  
- Loss: Cross-entropy  
- Hardware: Tesla T4 GPU  

---

## 📊 Results
### Few-Shot Accuracy
| Images/Class | ResNet18 | MobileNetV3-Large | EfficientNet-B0 | CNN (scratch) |
|--------------|----------|-------------------|-----------------|---------------|
| 5            | 78.67%   | **97.33%**        | 96.00%          | 22.00%        |
| 10           | 88.00%   | **99.33%**        | 97.33%          | 24.00%        |
| 25           | **98.00%** | 96.67%          | 96.67%          | 36.00%        |
| 50           | 98.00%   | 97.33%            | **98.67%**      | 39.33%        |
| 100          | 96.67%   | **98.67%**        | **98.67%**      | 43.33%        |

### Full Dataset (697 images)
- **MobileNetV3-Large**: 98.67% (fastest, 31.22s)  
- **EfficientNet-B0**: 98.67% (lowest loss, 0.0448)  
- **ResNet18**: 97.33%  
- **CNN (scratch)**: 62.67%  

---

## 💡 Key Insights
- **Pretraining is crucial**: pretrained models >96% accuracy even with 5–25 images/class.  
- **Scratch CNN struggles**: <45% few-shot, only 62.67% full-data.  
- **Best trade-off**: MobileNetV3-Large (accuracy + speed).  
- **Results fluctuate**: small dataset size means minor accuracy changes may be noise.  

---

## ⚠️ Limitations
- Single run per setting → results not statistically conclusive.  
- Small test set (150 images).  
- Only frozen-backbone transfer learning tested (no fine-tuning).  
- Fixed hyperparameters (no tuning).  

---

## 🔮 Future Work
- Multiple runs with random subsets → mean & std reporting.  
- Data augmentation + hyperparameter tuning.  
- Fine-tuning pretrained layers.  
- Larger, more diverse datasets.  
- Report inference latency & model size.  

---

## ✅ Conclusion
Pretrained ImageNet models achieve **>96% accuracy with very few labeled examples**, while a CNN trained from scratch lags far behind.  
**MobileNetV3-Large** provides the best balance of speed and accuracy, making it ideal for few-shot image classification tasks.

---

## 📖 References
- Oxford-IIIT Pet Dataset  
- ResNet, MobileNetV3, EfficientNet papers  
- PyTorch documentation
