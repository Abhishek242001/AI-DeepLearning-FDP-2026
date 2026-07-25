# 💻 Code — Hands-on Notebooks

Two fully hands-on Jupyter notebooks used in the live workshop sessions. Both are self-contained — run top to bottom on Google Colab (GPU runtime recommended) or any local environment with a CUDA GPU.

---

## 📁 `ai_model_development/`

**[`AI_Model_Development_Workshop_LandCover_CNN.ipynb`](ai_model_development/AI_Model_Development_Workshop_LandCover_CNN.ipynb)** · 50 cells

Builds and trains a **CNN** and a **Vision Transformer (ViT)** from scratch on the EuroSAT satellite land-cover dataset, then compares them head-to-head on accuracy, parameter count, and confusion-matrix behavior.

**Covers:** dataset loading & class balance, `tf.data` pipelines, CNN architecture (Conv2D/BatchNorm/MaxPool + Global Average Pooling), ViT architecture (patch embedding + multi-head self-attention), training with reproducibility safeguards, evaluation, and math deep-dives (convolution, pooling, parameter counting, self-attention).

**Stack:** TensorFlow/Keras, NumPy, Matplotlib

📖 Full topic-by-topic notes: [`notes/README.md` → Session 2](<../notes/README.md#-session-2-ai-model-development-using-python>)

---

## 📁 `deep_learning_resource_optimization/`

**[`Deep_Learning_Resource_Optimization_Workshop.ipynb`](deep_learning_resource_optimization/Deep_Learning_Resource_Optimization_Workshop.ipynb)** · 45 cells

Demonstrates the full model-efficiency stack live on GPT-2: **LoRA** fine-tuning, **quantization**, and **ONNX** export — with real measured before/after numbers for size, speed, and trainable-parameter count.

**Covers:** training a tiny character-level Transformer from scratch, loading and fine-tuning GPT-2 with LoRA (`peft`), precision formats (FP32/FP16/BF16/INT8), post-training quantization, exporting to ONNX and benchmarking against native PyTorch inference.

**Stack:** PyTorch, Hugging Face `transformers`, `peft`, `optimum-onnx`, `onnxruntime`

📖 Full topic-by-topic notes: [`notes/README.md` → Session 3](<../notes/README.md#-session-3-deep-learning-applications-for-resource-optimization>)

---

## ⚙️ Setup

```bash
# ai_model_development
pip install tensorflow numpy matplotlib datasets

# deep_learning_resource_optimization
pip install torch transformers peft accelerate optimum onnxruntime
```

**Recommended:** run both notebooks on [Google Colab](https://colab.research.google.com) with a **T4 GPU runtime** (Runtime → Change runtime type → T4 GPU) — this matches the hardware used during the live workshop sessions, so your results should closely match the numbers reported in the notes.

---
*Part of the FDP on Integrating AI and IoT for Sustainable Resource Management — IIT Guwahati (EICT Academy) × NIT Nagaland, 27–31 July 2026.*
