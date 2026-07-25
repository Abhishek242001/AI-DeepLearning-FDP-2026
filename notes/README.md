# 🗒️ Session Notes

> Detailed notes for all sessions delivered by **Er. Abhishek Kumar Shukla** (Senior AI Developer, UniConverge Technologies Pvt. Ltd.) at the One-Week FDP on **"Integrating AI and IoT for Sustainable Resource Management"** — IIT Guwahati (EICT Academy) × NIT Nagaland, Chumoukedima | **27–31 July 2026**

---

## 📅 Session Overview

| # | Day | Date | Time | Session | Format |
|---|---|---|---|---|---|
| 1 | Day 3 | 29 Jul 2026 | 03:45 PM – 05:30 PM | [Machine Learning Techniques for Environmental and Resource Monitoring](#-session-1-machine-learning-techniques-for-environmental-and-resource-monitoring) | Lecture |
| 2 | Day 4 | 30 Jul 2026 | 09:30 AM – 11:15 AM | [Hands-on Workshop: AI Model Development using Python](#-session-2-ai-model-development-using-python) | Hands-on / Notebook |
| 3 | Day 4 | 30 Jul 2026 | 11:30 AM – 01:00 PM | [Deep Learning Applications for Resource Optimization](#-session-3-deep-learning-applications-for-resource-optimization) | Hands-on / Notebook |

📁 Related files: [`lecture material/Slides-PDF/`](../lecture%20material/Slides-PDF/) · [`code/`](../code) · [`resources/`](../resources)

---

## 🌍 Session 1: Machine Learning Techniques for Environmental and Resource Monitoring

**Slide deck (PDF):** [`Machine Learning for Environmental & Resource Monitoring.pdf`](../lecture%20material/Slides-PDF/Machine%20Learning%20for%20Environmental%20%26%20Resource%20Monitoring.pdf) · **55 slides · 9 modules**

### 🎯 What This Session Covers

A broad, systems-level tour of how machine learning is applied across the entire environmental-monitoring pipeline — from raw satellite/IoT sensor data to deployed, production-grade decision-support systems. Unlike the two hands-on sessions, this is a **conceptual map** of the field: architectures, taxonomies, trade-offs, and real deployed case studies.

### 🧭 The 9 Modules

| Module | Focus | Key Slides |
|---|---|---|
| **1. Why This Matters** | Planetary-scale environmental challenges; why traditional monitoring fails | 3–4 |
| **2. Foundations** | History of remote sensing & ML; infrastructure pipeline; taxonomies | 5–14 |
| **3. Data Ecosystem** | Data sources, IoT sensor networks, cloud vs. edge processing | 15–19 |
| **4. The Label Bottleneck** | Why EO data is hard to label; transfer learning; self-supervised learning; foundation models | 20–23 |
| **5. Vision Architectures** | ViT vs. CNN; U-Net, DeepLab, YOLO; change detection; Siamese networks | 24–32 |
| **6. Forecasting Models** | ARIMA, LSTM, GRU, Transformers, Temporal Fusion Transformer | 33–39 |
| **7. Anomaly Detection & Trust** | Statistical methods, autoencoders, isolation forests, explainable AI, evaluation metrics | 40–45 |
| **8. Production & Ethics** | MLOps, operational challenges, responsible AI | 46–48 |
| **9. Case Studies & Future** | 5 real-world deployments + emerging research directions | 49–55 |

### 📖 Detailed Notes by Topic

#### 1️⃣ Why Environmental AI Matters Now
Climate volatility, biodiversity collapse, and resource scarcity are converging into what the deck calls a "planetary-scale crisis." Six interconnected domains where **traditional monitoring fails and ML becomes essential**:
- Deforestation & land-use change
- Water scarcity & flood risk
- Air quality & public health
- Biodiversity loss
- Food security / crop yield
- Disaster response & early warning

#### 2️⃣ Evolution of the Field
- **Remote sensing**: 100 years — from aerial photography → multispectral satellites → near-real-time planetary observation (Sentinel, Landsat missions).
- **Machine learning**: 7 decades — hand-crafted features → classical ML (SVM, Random Forest) → CNNs → Vision Transformers → billion-parameter **foundation models**.

#### 3️⃣ Core Taxonomies (important for exams / quick recall)

**Machine Learning Paradigms** (defined by what the model learns from):
| Paradigm | Feedback Signal |
|---|---|
| Supervised Learning | Labeled input–output pairs |
| Unsupervised Learning | No labels — structure discovery |
| Semi-supervised Learning | Small labeled + large unlabeled set |
| Reinforcement Learning | Reward signal from environment interaction |

**Computer Vision Tasks:**
| Task | Question Answered |
|---|---|
| Classification | "What is in this image?" |
| Object Detection | "Where are the objects (bounding boxes)?" |
| Semantic Segmentation | "What class is *every pixel*?" |
| Instance Segmentation | "Which pixels belong to *which specific object*?" |

**Remote Sensing Modalities:**
| Sensor Type | Physical Property Captured |
|---|---|
| Optical (RGB/Multispectral) | Reflected sunlight |
| Hyperspectral | Fine-grained spectral signatures (100s of bands) |
| SAR (Radar) | Surface roughness/moisture — works day/night, through cloud |
| LiDAR | 3D structure / elevation |

**Traditional ML vs. Deep Learning:** the deck frames this as a trade-off between **data volume, compute budget, and interpretability** — classical ML (Random Forest, SVM, XGBoost) wins on small tabular datasets and interpretability; deep learning wins when data is abundant and spatial/temporal structure is rich.

#### 4️⃣ Data Ecosystem & IoT Pipeline
- **8 families of environmental data sources**, each with its own volume/velocity/veracity profile (satellite imagery, in-situ sensors, weather stations, drones, citizen science, social media, government records, historical archives).
- **Sensor networks**: ground-truth data travels from a field sensor (e.g., soil moisture probe) via **LoRa** (long-range, low-power radio) and **MQTT** (lightweight pub-sub messaging protocol) to a central forecasting model.
- **Cloud vs. Edge**:
  - ☁️ **Cloud** — centralize for large model training, multi-sensor fusion, global-scale analysis.
  - 📡 **Edge** — process locally when latency, bandwidth, or autonomy matters (drones, field gateways, remote cameras).

#### 5️⃣ Beating the Label Bottleneck
Labeled Earth Observation data is estimated to be **~100× harder to produce** than labeled ImageNet-style images (needs domain experts, field visits, multi-spectral interpretation). Three mitigation strategies:
1. **Transfer Learning** — reuse models pretrained on data-rich domains (e.g., ImageNet) and fine-tune on scarce EO-labeled data.
2. **Self-Supervised Learning** — generate "labels" from the data itself (e.g., masked patch prediction), pretrain on millions of *unlabeled* tiles, then fine-tune on a handful of labeled examples.
3. **Foundation Models for EO** — general-purpose EO backbones (analogous to GPT/BERT for language) replacing task-specific CNNs trained from scratch each time.

#### 6️⃣ Vision Architectures Deep Dive
- **CNN vs. ViT** — different inductive biases: CNNs assume locality/translation-invariance (via convolution); ViTs make no such assumption and instead *learn* spatial relationships via self-attention — more data-hungry but more flexible. *(This exact comparison is explored hands-on in [Session 2](#-session-2-ai-model-development-using-python).)*
- **Segmentation architectures** (5 families for per-pixel land-cover mapping):
  - **U-Net** — encoder-decoder with skip connections; originally built for medical imaging (2015), still dominates EO segmentation in 2025 due to its efficiency on limited labeled data.
  - **DeepLab** — dilated ("atrous") convolutions + pyramid pooling to capture multi-scale context without losing resolution.
  - **YOLO** — object detection rather than segmentation; answers "where is each object" instead of "what is each pixel."
- **Change Detection & Siamese Networks** — given two images of the same location at different times, a **Siamese network** (two identical weight-shared subnetworks) learns to output a similarity/difference map — the standard backbone for deforestation, urban-growth, and disaster-damage detection.

#### 7️⃣ Forecasting Models (Time Series)
| Model | Era | Strength |
|---|---|---|
| **ARIMA** | ~1970s | 50-year-old classical baseline; still best for short-horizon, single-variable series |
| **LSTM** | 1997 | Gated recurrent cell that solved the vanishing-gradient problem; powered the first wave of deep time-series forecasting |
| **GRU** | 2014 | Simplified LSTM — 2 gates instead of 3, fewer parameters, often comparable accuracy |
| **Transformer for Time Series** | 2017+ | Self-attention over time steps — parallelizable, scales to long sequences, but has known pitfalls for forecasting (no innate notion of recency/causality) |
| **Temporal Fusion Transformer (TFT)** | 2019 | Multi-horizon forecasting **with native interpretability** — built for real operational decision-making, not just accuracy |

Key comparison flagged in the deck: **ARIMA vs. LSTM** — the classical method still wins on short, simple, single-variable series where a deep model would overfit; LSTM wins as data volume and multivariate complexity grow.

#### 8️⃣ Anomaly Detection
Six families, each detecting a *different definition* of "abnormal":
- **Classical statistics** — Z-score, IQR, time-series decomposition (simplest, often most useful first pass).
- **Autoencoders** — train to reconstruct "normal" data; anomalies reconstruct poorly → high reconstruction error flags them.
- **Isolation Forest** — anomalies are "few and different," so random partitioning isolates them faster (shorter path length in the tree) than normal points.

#### 9️⃣ Trust, Evaluation & Deployment
- **Explainable AI (XAI)** — when a model says "deforestation detected," operators need to know *why* before dispatching a costly field response.
- **Evaluation metrics** — accuracy alone is misleading on imbalanced environmental data; precision, recall, F1, and macro-averages matter more.
- **MLOps** — "the hardest 10% of ML" — taking a trained model and keeping it reliable in production (monitoring, retraining, versioning).
- **Operational challenges** — six recurring headaches: data drift, connectivity gaps, labeling costs, model staleness, hardware constraints, and stakeholder trust.
- **Responsible AI / Ethics** — six dimensions especially critical when models inform policy or emergency response (bias, transparency, accountability, data sovereignty, environmental cost of training, dual-use risk).

### 🏆 Real-World Case Studies Presented

| # | Case Study | Scale/Impact |
|---|---|---|
| 1 | 🌳 Deforestation Monitoring — Amazon Basin | Near-real-time illegal logging detection across ~5M km² of tropical forest |
| 2 | 🌊 Flood Detection — Global Disaster Response | Operational flood-extent mapping within hours of disaster onset, anywhere on Earth |
| 3 | 🌾 Crop Yield Prediction — National Scale | Pre-harvest yield forecasts at county resolution for food-security planning |
| 4 | 🔥 Wildfire Detection — Real-time Alerting | Sub-minute wildfire detection from geostationary satellites (western US) |
| 5 | 🏙️ Air Quality Forecasting — Urban PM2.5 | Hyperlocal 7-day PM2.5 forecasts for 200+ Indian cities, informing school closures & public advisories |

### 💡 Key Takeaways
- Environmental ML is a **full pipeline problem** — sensors → data engineering → modeling → deployment → trust — not just "train a model."
- The **label bottleneck** is the field's defining constraint; transfer learning, self-supervision, and foundation models exist specifically to work around it.
- **No single architecture wins everywhere** — the right choice (CNN vs. ViT, ARIMA vs. LSTM, cloud vs. edge) always depends on data volume, latency needs, and interpretability requirements.
- Real deployments (case studies above) prove this is **already operational at planetary scale**, not theoretical.

---

## 🤖 Session 2: AI Model Development using Python

**Slide deck (PDF):** [`AI for Environmental Monitoring using Satellite Images CNN vs Vision Transformer.pdf`](../lecture%20material/Slides-PDF/AI%20for%20Environmental%20Monitoring%20using%20Satellite%20Images%20CNN%20vs%20Vision%20Transformer.pdf) · **50 slides**
**Notebook:** [`AI_Model_Development_Workshop_LandCover_CNN.ipynb`](../code/ai_model_development/AI_Model_Development_Workshop_LandCover_CNN.ipynb) · **50 cells**

### 🎯 What This Session Covers
A fully hands-on, **build-both-from-scratch** comparison: a Convolutional Neural Network vs. a Vision Transformer, trained on the **exact same dataset, split, preprocessing, and optimizer** — so the only variable is architecture. The workshop is explicit about showing **honest, real training curves** (including volatility and failure modes), not idealized textbook numbers.

### 🗺️ Workshop Roadmap (7 sections, ~90 minutes)

| # | Section | Time |
|---|---|---|
| 1 | Setup, GPU & Reproducibility | ~10 min |
| 2 | EuroSAT Dataset & Class Balance | ~12 min |
| 3 | Preprocessing & Data Pipelines | ~12 min |
| 4 | Build & Train the CNN | ~18 min |
| 5 | Build & Train the ViT | ~18 min |
| 6 | Evaluation: Confusion Matrix | ~10 min |
| 7 | Head-to-Head Comparison + Math Deep-Dives | ~10 min |

### 📚 Dataset: EuroSAT

- **Source:** Sentinel-2 satellite imagery, simplified to 64×64 RGB patches (originally 13-band), hosted on a stable HuggingFace mirror.
- **Split:** 21,600 training images (~89%) / 2,700 test images (~11%), never seen during training.
- **10 land-cover classes:** Forest, River, Residential, Industrial, Annual Crop *(largest — 2,373 images)*, Permanent Crop, Pasture *(smallest — 1,626 images)*, Highway, Herbaceous Vegetation, Sea/Lake.
- **Class imbalance ratio:** 1.46× (Annual Crop vs. Pasture) — deliberately **left unmitigated** as a teaching device to later show its effect on precision/recall.

### 🐛 Case Study: The Class-Ordering Bug
A real bug hit during workshop preparation: the model stayed near random-guess accuracy until the team traced it to **dataset sort order** — `.shuffle(buffer=1000)` wasn't enough because the buffer only spanned 1,000 of 21,600 examples. **Fix:** shuffle at the *source* level, before pipeline construction. Lesson: a fixed random seed (42) doubles as a debugging tool — same seed, same bug, verifiable fix.

### ⚙️ Reproducibility Contract (5 pillars)
1. Fixed seed = 42 (`tf.random.set_seed` + `np.random.seed`)
2. Pinned library versions (protobuf, pyarrow, datasets)
3. GPU verified at startup — fail loudly if missing
4. Deterministic `tf.data` ops
5. `EarlyStopping(restore_best_weights=True)` — final weights are the *best*, not the *last*

### 🧩 Data Pipeline (`tf.data`, 6 stages)
Load → Decode → Normalize `[0,1]` → **Augment** (train only: horizontal/vertical flip + 90° rotation — no color distortion, since spectral signature carries class signal) → Batch (32) → Prefetch (`AUTOTUNE`). The **test pipeline skips augmentation** — evaluation happens on realistic, unmodified images.

### 🏗️ Model 1 — CNN (Baseline)

| Property | Value |
|---|---|
| Architecture | 3× (Conv2D → BatchNorm → MaxPool) blocks, filters 32→64→128, then GlobalAveragePooling2D → Dense head |
| Total parameters | **111,946** (111,498 trainable / 448 non-trainable) |
| Regularization | Dropout 0.3, BatchNorm |
| Optimizer | Adam, lr = 0.001, 8 epochs, EarlyStopping (patience 3) |

**Why GAP instead of Flatten?** GlobalAveragePooling2D collapses each feature map to a single number (128 total) instead of flattening 8×8×128 = 8,192 values — the single biggest parameter saver in the design, critical for controlling overfitting on 21,600 images.

**Real training results:** Validation accuracy spiked to **84.07% at epoch 5**, then *degraded* to 62.4% by epoch 7 — a textbook case of small-data volatility (BatchNorm running-stats interacting with the learning rate). `restore_best_weights=True` is what let the workshop report **84.07%** instead of the naive last-epoch **62.4%** — a **+21.7 percentage-point** difference purely from the safeguard, not the architecture.

**Test results:** 84.07% accuracy, loss 0.4669, ~7.5 min total training time on a Tesla T4.
**Where it struggles:** the CNN's largest class (Annual Crop) shows **recall 0.97 but precision 0.72** — the model defaults to guessing the majority class when uncertain, a direct, traceable consequence of class imbalance.

### 🏗️ Model 2 — Vision Transformer (ViT)

| Property | Value |
|---|---|
| Pipeline | Image → Patchify → Patch + Position Embedding → 4× Transformer blocks (multi-head self-attention) → Classification head |
| Total parameters | **160,074** — deliberately kept close to the CNN's 111,946 so the comparison isn't confounded by capacity |
| Why patches, not pixels? | Quadratic cost of full-pixel self-attention is intractable; patchifying reduces sequence length to a manageable size |

**Test results:** **83.63%** accuracy — nearly tied with the CNN (84.07%), but via a **very different error pattern** (different confusion-matrix mistakes), demonstrating that similar headline accuracy can hide very different learned representations.

### ⚖️ CNN vs. ViT — Head-to-Head

| Dimension | CNN | ViT |
|---|---|---|
| Inductive bias | Local pattern filters, built-in translation invariance | Global self-attention, learned spatial relationships |
| Data efficiency | Small-data efficient | Data-hungry but scalable |
| Test accuracy | 84.07% | 83.63% |
| Parameters | 111,946 | 160,074 |
| Strength | Small-data efficiency, local texture recognition | Long-range context, no locality assumption |
| Weakness | Limited receptive field, majority-class bias, training volatility | More parameters needed for comparable accuracy |

**Decision guidance from the deck:** choose CNN for small, texture-dominant datasets and limited compute; choose ViT when data is abundant and long-range spatial context matters more than local texture.

### 🧮 Math Deep-Dives (verified against real notebook output)
- **Convolution** — worked numeric example of a 3×3 kernel sliding over an input patch.
- **MaxPooling** — worked example of 2×2 window reduction.
- **Parameter counting** — formula `(k×k×in_channels + 1) × out_channels`, verified: e.g. `(3×3×3+1)×32 = 896` for the first conv layer.
- **Patch extraction** — image → sequence of flattened patches.
- **Self-attention** — Query/Key/Value projections, scaled dot-product attention (`softmax(QKᵀ/√d_k)V`), and how attention output produces context-aware patch representations.

### 💡 Key Takeaways
- **Reported accuracy is a function of your safeguards, not just your architecture** — always specify which epoch's weights you're reporting.
- Volatile training curves are **information, not failure** — diagnose the cause (here: BatchNorm + learning rate on small data) rather than suppressing it.
- Near-identical headline accuracy (84.07% vs. 83.63%) can still hide very different error patterns — always check the confusion matrix, not just the top-line number.
- Class imbalance shows up concretely as a **precision/recall divergence**, not just as an abstract "expected bias."

---

## ⚡ Session 3: Deep Learning Applications for Resource Optimization

**Slide deck:** [`Deep Learning Applications for Resource Optimization.pptx`](../slides/Deep%20Learning%20Applications%20for%20Resource%20Optimization.pptx) · **58 slides**
**Notebook:** [`Deep_Learning_Resource_Optimization_Workshop.ipynb`](../code/deep_learning_resource_optimization/Deep_Learning_Resource_Optimization_Workshop.ipynb) · **45 cells**

### 🎯 What This Session Covers
Where Session 2 asked "which architecture is more accurate," this session asks a different question entirely: **"how do we make an already-good model cheap enough to train and deploy?"** It covers the full efficiency stack — parameter-efficient fine-tuning, numeric precision, quantization, and ONNX export — then demonstrates all four **live**, with real measured before/after numbers on GPT-2.

### 🗺️ Session Roadmap (8 parts)

| Part | Topic | Type |
|---|---|---|
| 1 | Why Resource Optimization Matters | Conceptual |
| 2 | The Cost of Scale | Conceptual |
| 3 | PEFT & LoRA | Conceptual |
| 4 | Precision Formats | Conceptual |
| 5 | Quantization | Conceptual |
| 6 | Model Export & ONNX | Conceptual |
| 7 | Live Demo Setup | Hands-on |
| 8 | Live Results & Takeaways | Hands-on |

### 1️⃣ Why This Matters: The Cost of Scale
**Full fine-tuning** of a pretrained model requires storing, per weight: the parameter itself + gradient + optimizer state (Adam keeps 2 extra moments per parameter) — meaning memory scales roughly **4×** the raw parameter count in FP32. This memory wall is what motivates every technique that follows. Every technique in the session optimizes one of **three resources**: compute, memory, or storage/bandwidth.

### 2️⃣ PEFT & LoRA (Parameter-Efficient Fine-Tuning)

**Core idea:** freeze almost the entire pretrained model, and train only a small injected subset of parameters.

**Three families of PEFT:**
- Adapter-based (small bottleneck layers inserted between frozen layers)
- Prompt/prefix-based (learnable soft tokens prepended to input)
- **Low-rank based — LoRA** (covered in depth)

**LoRA — Low-Rank Adaptation:** instead of updating a full `d × k` weight matrix (which has `d×k` trainable values), LoRA decomposes the update into two much smaller matrices of rank `r`, so trainable parameters shrink to `r×(d+k)` — a small fraction of the full update when `r` is small (e.g., 8 or 16). This is where the savings come from: **the rank `r` directly controls the trainable-parameter/expressiveness trade-off.**

**QLoRA:** combines LoRA with quantization — the frozen base model is loaded in a heavily compressed **4-bit** format, while the small trainable LoRA matrices stay in higher precision. This lets fine-tuning happen on GPUs far too small to hold the full model in FP16/FP32.

### 3️⃣ Precision Formats

| Format | Bits | Notes |
|---|---|---|
| FP32 | 32 | Full precision — training default historically |
| FP16 | 16 | More *precision* (more mantissa bits), narrower dynamic range — can overflow/underflow |
| BF16 | 16 | Same exponent range as FP32 (wide dynamic range), less precision — more training-stable than FP16 |
| INT8 | 8 | Used for quantized inference, not training |

**Mixed-precision training:** the standard recipe for getting FP16/BF16 speed and memory gains **without** losing FP32-level final accuracy — critical layers (e.g., loss computation, batch norm stats) stay in FP32 while the bulk of compute runs in FP16/BF16.

### 4️⃣ Quantization

**What it does:** maps a wide range of floating-point values to a much smaller set of discrete levels (e.g., FP32 → INT8), shrinking both **model size** and, often, **inference latency**.

**Two strategies:**
- **Post-Training Quantization (PTQ)** — quantize an already-trained model. Calibration: a small representative batch of real input data is passed through the trained model to determine the right scaling ranges per layer.
- **Quantization-Aware Training (QAT)** — simulate quantization *during* training so the model learns to be robust to the precision loss (higher accuracy retention, more training cost).

**⚠️ Two real gotchas flagged in the deck:**
1. **Not all models quantize the same way** — some layer types silently fail to quantize or degrade sharply; this is a **silent failure mode**, not a crash.
2. **Measuring quantized model size correctly is non-trivial** — a "trusted" measurement tool can report misleading numbers if it doesn't account for how the framework actually stores quantized weights on disk.

### 5️⃣ Model Export & ONNX

**The problem ONNX solves:** a trained PyTorch/TensorFlow model is tied to its training framework and Python runtime — a deployment liability. **ONNX** (Open Neural Network Exchange) decouples the trained model from its original framework, enabling portable, framework-independent deployment.

**Export pipeline (3 steps):** trained model → export to ONNX format → run via ONNX Runtime.

**Why ONNX Runtime is often faster** — three independent optimization layers that *stack*: graph-level operator fusion, hardware-specific execution providers, and reduced Python-interpreter overhead.

**⚠️ Important clarification/common misconception:** exporting to ONNX **does not, by itself, shrink a model** — export is a format change, not compression. Size reduction still requires quantization or pruning on top of export.

### 🖥️ Live Demo (Part 7–8) — What Was Actually Built

Two models, in sequence, demonstrating the full optimization stack end-to-end:
1. **A tiny Transformer, trained from scratch** (character-level vocabulary, only a few thousand parameters) — used to make the full training loop (forward → loss → backward → update) visible and inspectable before touching a large pretrained model.
2. **GPT-2, fine-tuned with LoRA** — the full 124-million-parameter pretrained model is loaded and its actual parameter count confirmed live; a LoRA adapter is then trained on a small custom dataset and saved separately from the frozen base model.

**Stack used:** PyTorch + Hugging Face `transformers`, `peft` (LoRA), `optimum-onnx` (ONNX export), `onnxruntime`.

### 📊 Live Measured Results

| Stage | What Was Measured |
|---|---|
| **LoRA Fine-Tuning** | Trainable parameter count vs. full model (dramatic reduction); memory footprint during training |
| **Quantization** | Model size before/after INT8 quantization |
| **⚠️ Surprising finding** | Quantization made the model **smaller but slower** on the workshop hardware — a real, measured result contradicting the "quantization = always faster" assumption, used to teach that hardware support for low-precision ops varies |
| **ONNX Export** | Latency/throughput comparison, native PyTorch vs. ONNX Runtime |
| **Full comparison** | Every version tested today — baseline, LoRA fine-tuned, quantized, ONNX-exported — compared side by side on size, speed, and (where applicable) accuracy |

### 💡 The Three Big Ideas (Session's own summary)
1. **You almost never need to update every parameter** — LoRA-style low-rank updates get you most of the benefit of full fine-tuning at a fraction of the memory cost.
2. **Precision and quantization trade a controlled amount of numeric accuracy for real, measurable memory/speed gains** — but the gains are *hardware-dependent*, not guaranteed (see the quantization slowdown finding above).
3. **Export format ≠ compression** — ONNX buys portability and runtime optimizations, not smaller weights by itself; combine it with quantization for both benefits.

### 🔗 Mapping Back to Your Own Research
The deck explicitly connects each technique to faculty research use cases: LoRA for fine-tuning domain-specific language/vision models on limited GPU budgets; quantization for deploying models on edge devices (e.g., field IoT gateways, drones); ONNX for sharing trained models across labs using different frameworks.

---

## 🧑‍🏫 Presenter

**Er. Abhishek Kumar Shukla**
Senior AI Developer, UniConverge Technologies Pvt. Ltd.

---

## 📌 How to Use This Repository

1. Start with the **session notes above** for a fast conceptual overview of each topic.
2. Open the matching notebook in `code/` to run the hands-on exercises yourself (Google Colab with a GPU runtime is recommended for Sessions 2 & 3).
3. Refer to the original slide decks in `slides/` for the full visual explanations, diagrams, and speaker notes.
4. See [`resources/README.md`](../resources/README.md) for supporting research papers on AI in remote sensing.

*Compiled for the FDP on Integrating AI and IoT for Sustainable Resource Management — IIT Guwahati (EICT Academy) × NIT Nagaland, 27–31 July 2026.*
