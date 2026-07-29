# 🗒️ Session Notes

> Detailed notes for all sessions delivered by **Er. Abhishek Kumar Shukla** (Senior AI Developer, UniConverge Technologies Pvt. Ltd.) at the One-Week FDP on **"Integrating AI and IoT for Sustainable Resource Management"** — IIT Guwahati (EICT Academy) × NIT Nagaland, Chumoukedima | **27–31 July 2026**

---

## 📅 Session Overview

| # | Day | Date | Time | Session | Format |
|---|---|---|---|---|---|
| 1 | Day 2 | 28 Jul 2026 | 02:00 PM – 03:30 PM | [Cloud Computing for AI](#-session-1-cloud-computing-for-ai) | Lecture + Hands-on |
| 2 | Day 3 | 29 Jul 2026 | 03:45 PM – 05:30 PM | [Machine Learning Techniques for Environmental and Resource Monitoring](#-session-2-machine-learning-techniques-for-environmental-and-resource-monitoring) | Lecture |
| 3 | Day 4 | 30 Jul 2026 | 09:30 AM – 11:15 AM | [Hands-on Workshop: AI Model Development using Python](#-session-3-ai-model-development-using-python) | Hands-on / Notebook |
| 4 | Day 4 | 30 Jul 2026 | 11:30 AM – 01:00 PM | [Deep Learning Applications for Resource Optimization](#-session-4-deep-learning-applications-for-resource-optimization) | Hands-on / Notebook |

📁 Related files: [`lecture material/Slides-PDF/`](../lecture%20material/Slides-PDF/) · [`code/`](../code) · [`resources/`](../resources)

---

## ☁️ Session 1: Cloud Computing for AI

**Slide deck (PDF):** [`Cloud Computing for AI.pdf`](<../lecture material/Slides-PDF/Cloud Computing for AI.pdf>) · **18 slides**

### 🎯 What This Session Covers

A ground-up tour of cloud computing framed specifically around AI workloads — starting from the NIST definition of cloud computing and building up to a real production case study and a hands-on introduction to a free GPU platform. Where the later sessions go deep on specific model architectures, this session is the **infrastructure layer underneath all of them** — the "where does the compute for all this actually come from" question.

### 🗺️ Session Roadmap (3 phases, 9 parts)

| Phase | Part | Focus |
|---|---|---|
| **Phase 1 · Foundations** | 01 · Cloud Fundamentals | NIST definition, characteristics, evolution |
| | 02 · Service & Deployment Models | IaaS, PaaS, SaaS · Public, Private, Hybrid, Multi-Cloud |
| | 03 · Cloud Providers for AI | AWS, GCP, Azure, IBM compared |
| **Phase 2 · Infrastructure** | 04 · GPU / TPU Computing | Specialized high-performance hardware on-demand |
| | 05 · Cloud AI/ML Platforms | SageMaker, Vertex AI, Azure ML Studio |
| | 06 · Storage & Data Services | S3, data lakes, managed databases, feature stores |
| **Phase 3 · Operations** | 07 · Training & Deployment | Distributed training, containerized serving, edge–cloud hybrid |
| | 08 · MLOps in the Cloud | CI/CD pipelines, versioning, drift monitoring |
| | 09 · Case Study & Hands-On | AWS AI-search case study + Lightning.ai free tier |

### 1️⃣ What Is Cloud Computing?

**NIST definition (the one to memorize):** a model for enabling ubiquitous, convenient, on-demand network access to a shared pool of configurable computing resources — networks, servers, storage, applications, services — that can be rapidly provisioned and released with minimal management effort.

**The intuition the deck leans on:** cloud computing is the **electricity grid** for compute. You plug in and pay for usage instead of owning a power plant; with cloud you rent compute and pay per hour instead of owning a data center.

**Three defining traits, restated simply:**
- Delivered over the internet — resources are accessed remotely, never physically owned by the user
- Pay only for what you use — OpEx instead of CapEx, no large upfront hardware investment
- Elastic & self-service — provision compute, storage, or networking in minutes, scale up or down on demand

### 2️⃣ Why AI Specifically Needs the Cloud

Three reasons the deck gives for why modern AI workloads are an especially good fit for cloud infrastructure:

| Reason | Detail |
|---|---|
| **Massive elastic compute** | Training large models needs thousands of GPU-hours; cloud lets you spin up 100 GPUs for a week then shut them down, instead of buying hardware that sits idle 90% of the time |
| **Cost-efficient by design** | On-prem GPU clusters are cost-prohibitive for most institutions; pay-as-you-go pricing converts large CapEx into predictable OpEx |
| **Specialized hardware access** | Cloud providers refresh GPU/TPU generations faster than most organizations can buy them — instant access to silicon like NVIDIA H100, Google TPU v5, AWS Trainium, with zero procurement overhead |

### 3️⃣ From Data Centers to Cloud AI — A Four-Stage Evolution

| Stage | Characteristics |
|---|---|
| **On-Prem** | Owned physical servers, fixed capacity & high CapEx, manual provisioning, hardware bought & racked |
| **Virtualization** | Multiple VMs per host, higher hardware utilization, snapshot & migrate jobs, decouples OS from hardware |
| **Cloud Onward** | AWS launches EC2 & S3, rented by the hour, self-service & elastic, compute as a utility |
| **AI Cloud Onward** | AlexNet sparks the AI boom, GPU/TPU cloud instances, custom silicon chips, cloud built specifically for AI |

**Key milestone flagged in the deck:** the 2012 deep-learning breakthrough (AlexNet) is what triggered cloud providers to pivot rapidly toward AI-optimized hardware — the AI-cloud era didn't exist before this.

### 4️⃣ NIST's Five Essential Characteristics — with an AI Angle on Each

| # | Characteristic | AI-Specific Angle |
|---|---|---|
| 1 | On-Demand Self-Service | A data scientist provisions a GPU instance in minutes — no IT ticket, no approval step |
| 2 | Broad Network Access | Models, datasets, and APIs reachable from anywhere — laptops, phones, edge devices |
| 3 | Resource Pooling | Multi-tenancy — multiple customers share physical infrastructure, dynamically assigned |
| 4 | Rapid Elasticity | **AI angle: training clusters** — auto-scale from 1 to 64 GPUs in minutes during a job, then back to zero when training ends |
| 5 | Measured Service | **AI angle: metered GPU-hours** — billing is metered precisely (GPU-hours, storage-GB, API calls); you pay only for what you consumed |

### 5️⃣ Service Models: IaaS · PaaS · SaaS

**Framing:** as you move IaaS → PaaS → SaaS, you gain convenience but lose control. Each layer has a natural AI use case.

| Model | You Manage | Provider Manages | AI Example |
|---|---|---|---|
| **IaaS** (most control) | OS + software | Only physical hardware | Renting a raw GPU VM (e.g., AWS EC2 P4 instance) and installing your own PyTorch/TensorFlow stack from scratch |
| **PaaS** (balanced) | Your code + data | Provisioning, scaling, orchestration, runtime | Amazon SageMaker or Google Vertex AI — managed notebooks, distributed training jobs, one-click endpoints |
| **SaaS** (most convenient) | Nothing | Everything | A ready-made AI assistant like ChatGPT, or a hosted document-intelligence API — you only call it |

**Teaching point from the deck:** more convenience always means less control — pick the layer that matches your team's skills and use case, not the "most advanced-sounding" option.

### 6️⃣ Deployment Models: Public · Private · Hybrid · Multi-Cloud

| Model | Trade-off |
|---|---|
| **Public Cloud** | Lowest cost. Shared infrastructure (AWS/Azure/GCP), multi-tenant, billed by usage, no upfront commitment. *Pro:* cheapest, fastest to start. *Con:* least control, shared tenancy. |
| **Private Cloud** | Full control. Dedicated infrastructure for one organization — required for highly sensitive AI data (e.g., healthcare, defense). *Pro:* max control, compliance-friendly. *Con:* expensive, slower to scale. |
| **Hybrid Cloud** | Balanced. Mix of public + private — train models in public cloud, keep sensitive data on private infrastructure. Common in regulated industries. *Pro:* best of both worlds. *Con:* network & data-flow complexity. |
| **Multi-Cloud** | No lock-in. More than one public cloud — e.g., AWS for storage, GCP for a specific AI API. *Pro:* avoids vendor lock-in. *Con:* higher operational complexity. |

### 7️⃣ Key Cloud Providers for AI

**Framing:** there's no single "best" provider — the right choice depends on existing infrastructure, budget, compliance needs, and team familiarity.

| Provider | Positioning | Key AI Assets |
|---|---|---|
| **Amazon Web Services** | Industry leader, deepest catalog | SageMaker (end-to-end ML), S3/EC2/Lambda ecosystem, custom Trainium/Inferentia silicon |
| **Google Cloud Platform** | Research-grade ML, TensorFlow-native | Vertex AI (unified AutoML + custom training), exclusive TPU pods, BigQuery + ML integration |
| **Microsoft Azure** | Enterprise integration, OpenAI partnership | Azure ML Studio (visual designer), exclusive hosted OpenAI models, Azure DevOps MLOps |
| **IBM Cloud** | Hybrid & Watson, regulated industries | Watson AI services (NLP/speech/vision), Red Hat OpenShift hybrid, quantum-safe security |

### 8️⃣ GPU / TPU Computing in the Cloud

**Why specialized hardware matters — CPU vs. GPU vs. TPU:**

| Hardware | Processing Style | Best For |
|---|---|---|
| **CPU** | Sequential — a handful of powerful cores | General tasks; slow for the matrix multiplications at the heart of neural networks |
| **GPU** | Thousands of parallel cores | Massively parallel — ideal for deep-learning matrix multiplies; originally built for graphics, now the AI workhorse |
| **TPU** | Custom tensor silicon | Google-built chips purpose-designed for tensor ops — highest throughput for compatible workloads |

**Cloud-specific cost lever — Spot / Preemptible Instances:** discounted, interruptible GPU access for non-urgent jobs, **60–90% cheaper than on-demand**. The trade-off is possible mid-job interruption, which is why checkpointing (covered in Part 07) matters.

### 9️⃣ Cloud AI/ML Platforms

All three platforms below abstract away infrastructure so teams focus on data and models instead of server provisioning:

| Platform | Provider | What It Is | Key Features |
|---|---|---|---|
| **Amazon SageMaker** | AWS | End-to-end ML lifecycle — labeling, distributed training, hyperparameter tuning, production monitoring | Built-in algorithms & custom frameworks · managed notebooks & training jobs · automatic model tuning · one-click endpoint deployment |
| **Google Vertex AI** | Google Cloud | Unifies AutoML (no-code) with custom training | AutoML for tabular/image/text/video · custom training with PyTorch/TF/JAX · BigQuery & Feature Store integration · Model Registry & Endpoints |
| **Azure ML Studio** | Microsoft Azure | Visual pipeline designer + code-first notebooks | Visual designer + code notebooks · automated ML & hyperparameter tuning · Azure DevOps native CI/CD · Responsible AI dashboard built-in |

### 🔟 Storage & Data Services for AI

The data layer feeds every ML pipeline — from raw ingestion through feature engineering to model artifacts:

| Layer | Purpose | Examples |
|---|---|---|
| **Object Storage** | Unstructured data at massive scale, low cost/GB — images, video, audio, raw text | Amazon S3, Google Cloud Storage, Azure Blob |
| **Data Lakes** | Centralized repositories holding raw data in native format until needed | AWS Lake Formation, Delta Lake, Apache Iceberg |
| **Managed Databases** | Structured/relational data feeding feature-engineering pipelines; provider handles scaling | Amazon RDS, Cloud SQL, Azure SQL |
| **Feature Stores** | Centralized repository ensuring the same engineered feature definitions are used globally | SageMaker Feature Store, Feast, Vertex Feature Store |

### 1️⃣1️⃣ Cloud-Based Model Training

Three techniques that turn weeks of single-machine training into hours:

- **Distributed Training** — split a job across multiple GPUs/nodes. Two strategies: **data parallelism** (same model, different data shards) and **model parallelism** (model itself split across devices). Scales roughly linearly with GPU count.
- **Auto-Scaling Clusters** — nodes are added/removed automatically based on training-job demand; a 64-GPU job spins up only for the run, then drops to zero. You never pay for idle capacity between jobs.
- **Spot Instances** — discounted, interruptible compute for non-time-critical jobs; up to 90% cost reduction, at the cost of possible mid-job interruption, handled via checkpointing.

### 1️⃣2️⃣ Cloud-Based Model Deployment (Inference & Serving)

| Pattern | What It Does |
|---|---|
| **Model Serving (API Endpoints)** | Trained model exposed via a REST or WebSocket API endpoint so applications can send data and get predictions back |
| **Containers & Kubernetes** | Models packaged in Docker containers for consistent deployment across dev/test/prod; Kubernetes orchestrates and auto-scales inference workloads based on request volume |
| **Edge–Cloud Hybrid Inference** | Lightweight inference runs on edge devices (phones, cameras, IoT) for ultra-low latency, while heavier/batch processing happens in the cloud |

**The general pattern the deck names explicitly:** a containerized model behind an API, auto-scaled by request load — this is the *exact same shape* used in the Section 9 case study below.

### 1️⃣3️⃣ MLOps in the Cloud

Applying DevOps principles (CI/CD, automation, monitoring) to the ML lifecycle — without this, models become "science projects" that never reliably reach production.

| Practice | What It Solves | Example Tools |
|---|---|---|
| **CI/CD for ML** | Automated testing and deployment of new model versions; every code change triggers tests, training, and controlled rollout | GitHub Actions, GitLab CI |
| **Pipeline Automation** | Automates the full sequence from data preprocessing to deployment — retraining becomes reproducible at the push of a button | Kubeflow, Airflow |
| **Model Versioning** | Tracks production models with full lineage back to training data; enables instant rollback if a new version underperforms | MLflow, Model Registry |
| **Monitoring for Drift** | Detects when model performance degrades due to real-world data drift; triggers alerts and retraining cycles automatically | Evidently, SageMaker Model Monitor |

### 1️⃣4️⃣ Case Study — AI Search Project, End-to-End on AWS

A real production system walked through step by step: client uploads a video, sends a natural-language query, and gets the top 5 matching moments back in real time.

| Step | What Happens |
|---|---|
| 1. Video Upload | Client sends video via REST API (`/upload_ai_search_video`) |
| 2. Amazon S3 Storage | Video stored in an S3 bucket; access URL returned |
| 3. WebSocket Connection | Client opens `/ws/ai_search/{id}`, sends `search_text` + video URL |
| 4. Frame Extraction (OpenCV) | FPS-based smart batching — processes ~1 batch/sec, not every frame |
| 5. AI Inference Model | Batch of frames + search text → matches with confidence scores |
| 6. Top 5 Results Returned | Timestamps + confidence scores pushed back via WebSocket, earliest match first |

**Why AWS, specifically, for this system:**
- **S3 storage** — scalable, durable video storage at roughly $0.023/GB
- **Co-location** — region-based deployment keeps storage and compute co-located for low latency
- **EC2/GPU compute** — runs the FastAPI backend + AI inference with no owned servers

**The reusable pattern the deck extracts from this case study:** object storage + compute + a real-time connection + an AI inference step — this same shape recurs across most production cloud-AI systems, not just video search.

### 1️⃣5️⃣ Hands-On: Lightning.ai Free Tier

The session's pivot from "watching a production AWS example" to "you build and deploy your own model, today, for free":

| Feature | What It Gives You |
|---|---|
| **Free GPU Compute** | Free GPU-backed compute for training/experimentation — no cloud infrastructure to provision, no surprise bills |
| **AI Studio Environments** | Pre-built, cloud-hosted dev environments that launch instantly in-browser — no local Python/CUDA/driver setup |
| **Ready-Made Templates** | Templates for common AI workflows — fine-tuning a model, building an inference API, deploying a model-serving endpoint |
| **Built for Learning** | Lowers the barrier from "learning about cloud AI" to "actually deploying a model," in a single session |

### 💡 Key Takeaways (session's own summary)

1. **Cloud is AI's compute backbone** — elastic, on-demand GPU/TPU access is what makes modern AI training affordable at all.
2. **Every model is a trade-off** — IaaS/PaaS/SaaS and public/private/hybrid/multi-cloud each balance control, cost, and convenience differently; there's no universally "best" choice.
3. **A repeatable pattern underlies production systems** — storage + compute + data pipeline + inference is the shape of nearly every production cloud-AI system, as shown concretely in the AI-search case study.
4. **Free practice is real, not hypothetical** — Lightning.ai lets you start deploying models today with no budget required.

### 🔭 Future Trends Flagged

- **Edge–Cloud Convergence** — more inference moves to edge devices (phones, cameras, IoT) for low latency; the cloud increasingly specializes in training and heavier batch processing.
- **Sustainable / Green AI** — providers are optimizing data centers for energy efficiency as AI's power demands grow; carbon-aware training is becoming standard practice.
- **Serverless AI Inference** — pay-per-request model serving with zero server management; you invoke an endpoint and pay only for the milliseconds of compute used.

---

## 🌍 Session 2: Machine Learning Techniques for Environmental and Resource Monitoring

**Slide deck (PDF):** [`Machine Learning for Environmental & Resource Monitoring.pdf`](../lecture%20material/Slides-PDF/Machine%20Learning%20for%20Environmental%20%26%20Resource%20Monitoring.pdf) · **55 slides · 9 modules**

### 🎯 What This Session Covers

A broad, systems-level tour of how machine learning is applied across the entire environmental-monitoring pipeline — from raw satellite/IoT sensor data to deployed, production-grade decision-support systems. Unlike the hands-on sessions, this is a **conceptual map** of the field: architectures, taxonomies, trade-offs, and real deployed case studies.

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
- **CNN vs. ViT** — different inductive biases: CNNs assume locality/translation-invariance (via convolution); ViTs make no such assumption and instead *learn* spatial relationships via self-attention — more data-hungry but more flexible. *(This exact comparison is explored hands-on in [Session 3](#-session-3-ai-model-development-using-python).)*
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

## 🤖 Session 3: AI Model Development using Python

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

## ⚡ Session 4: Deep Learning Applications for Resource Optimization

**Slide deck (PDF):** [`Deep Learning Applications for Resource Optimization.pdf`](../lecture%20material/Slides-PDF/Deep%20Learning%20Applications%20for%20Resource%20Optimization.pdf) · **58 slides**
**Notebook:** [`Deep_Learning_Resource_Optimization_Workshop.ipynb`](../code/deep_learning_resource_optimization/Deep_Learning_Resource_Optimization_Workshop.ipynb) · **45 cells**

### 🎯 What This Session Covers
Where Session 3 asked "which architecture is more accurate," this session asks a different question entirely: **"how do we make an already-good model cheap enough to train and deploy?"** It covers the full efficiency stack — parameter-efficient fine-tuning, numeric precision, quantization, and ONNX export — then demonstrates all four **live**, with real measured before/after numbers on GPT-2.

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
2. Open the matching notebook in `code/` to run the hands-on exercises yourself (Google Colab with a GPU runtime is recommended for Sessions 3 & 4).
3. Refer to the PDF slide decks in `lecture material/Slides-PDF/` for the complete visual explanations, diagrams, and speaker notes.
4. See [`resources/README.md`](../resources/README.md) for supporting research papers on AI in remote sensing.

*Compiled for the FDP on Integrating AI and IoT for Sustainable Resource Management — IIT Guwahati (EICT Academy) × NIT Nagaland, 27–31 July 2026.*
