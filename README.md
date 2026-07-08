# Rice Leaf Disease Detection

📌 **Problem Statement**
Rice crops are commonly affected by three major diseases — Bacterial Leaf Blight, Brown Spot, and Leaf Smut — which are difficult for farmers to distinguish visually and manually. This project builds an image classification model to automatically identify the disease from a photo of a rice leaf, enabling faster, more consistent diagnosis.

📊 **Dataset**
* **Source:** [Rice Leaf Diseases Dataset](https://www.kaggle.com/)
* **Size:** 120 JPG images total, evenly split across 3 classes (40 images each):
    * Bacterial Leaf Blight
    * Brown Spot
    * Leaf Smut

🛠️ **Approach**
* **Exploratory Data Analysis (EDA):** Inspected image dimensions, class balance, and sample visualizations across the three disease categories.
* **Data Augmentation:** Since the dataset is very small (only 40 images/class), applied rotation, flipping, zoom, and brightness augmentation to artificially expand the training set and reduce overfitting.
* **Modeling:** Built and compared Convolutional Neural Network (CNN) architectures, including transfer learning with a pretrained backbone, for multi-class image classification.
* **Evaluation:** Compared models using accuracy, precision, recall, and confusion matrix to identify the best-performing approach for a small-data image classification setting.

📈 **Results**

| Model | Validation Accuracy | Notes |
| :--- | :--- | :--- |
| CNN (from scratch) + Augmentation | ~34.8% | Underfit — insufficient data |
| MobileNetV2 (Transfer Learning, frozen base) | ~87–91% | Strong generalization jump |
| MobileNetV2 (Fine-Tuned) | ~87% | Best performing / final model |

**Best model:** Fine-Tuned MobileNetV2 — selected as the final model. It reached ~87% validation accuracy with 91% weighted precision, showing 1.00 precision for Bacterial Leaf Blight and Brown Spot, and 1.00 recall for Leaf Smut. Its lightweight architecture also makes it practical for real-world deployment on mobile devices for field diagnostics.

⚠️ **Challenges Faced**
* **Very small dataset:** A CNN trained from scratch overfit almost immediately and plateaued near random-guess accuracy (~35%). Solved by switching to transfer learning with a pretrained MobileNetV2 backbone.
* **Visually similar symptoms:** Some diseases share overlapping visual patterns. Addressed by fine-tuning the last layers of MobileNetV2 (controlled unfreezing + a very low learning rate).
* **Fine-tuning instability:** Mitigated by unfreezing only the last 10 layers and using a very small learning rate (1e-6) to avoid catastrophic forgetting.

🧰 **Tech Stack**
Python · TensorFlow/Keras · NumPy · Pandas · Matplotlib · Google Colab

📁 **Files**
* `PRCP_1001_RiceLeaf_Disease_Detection.ipynb` — Full analysis, model building, and evaluation.

🚀 **How to Run**
1.  Open the notebook in [Google Colab](https://colab.research.google.com/).
2.  Upload the dataset zip files to your Colab environment.
3.  Run all cells sequentially.
