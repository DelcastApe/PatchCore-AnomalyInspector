# 🔍 PatchCore Anomaly Inspector  
Advanced Visual Defect Detection with FastAPI + ResNet18 + KNN PatchCore

PatchCore Anomaly Inspector is a complete system for **real-time industrial defect detection** using a PatchCore-based anomaly segmentation pipeline, combined with a modern and fast web interface.

This project provides:
- A **FastAPI backend** that runs PatchCore inference with ResNet-18 feature extraction.
- A fully interactive **web interface** to analyze images, folders, or live camera input.
- Automatic generation of **heatmaps, masks, polygons, IoU, and defect areas**.
- **Batch analysis** with CSV export and global KPIs (recall, defect rate, avg. defect area).
- Support for **ROI masks**, threshold tuning, and different sensitivity modes.

---

## 🚀 Features

### 🧠 AI / Anomaly Detection
- PatchCore-style feature extraction using **ResNet-18 (layer2 + layer3 hooks)**.
- K-Nearest Neighbors over a precomputed **memory bank**.
- Pixel-level **heatmaps**, binary masks, and polygon extraction.
- Automatic **IoU computation** (real IoU or approximate IoU when no GT is provided).
- Threshold override:  
  - `auto`  
  - manual threshold  
  - `sensitive` / `strict` modes.

---

### 📊 Metrics & Batch KPIs
For batches of images, the system computes:

- **Recall** (TP / (TP + FN))  
- Defect rate  
- Average defect area  
- Total images  
- Normals vs anomalies  

All results can be exported in **CSV format**.

---

### 🖥 Web Interface
Built with HTML, CSS and vanilla JS:

- Drag & drop image uploads  
- Folder upload  
- Switchable gallery & table views  
- Real-time camera inference (every 1.5s)  
- Score, IoU, state, and overlays in real time  
- Interactive GT labeling for recall calculation  

---

### ⚙️ Technology Stack
- **FastAPI** (Python)
- **PyTorch** (ResNet-18 backbone)
- **scikit-learn** (KNN)
- **OpenCV** (masks, contours, overlays)
- **NumPy**
- **Docker** (CPU or GPU profiles supported)

---

## 📁 Project Structure

```

Backend/
├── main.py                # FastAPI service + PatchCore pipeline
├── models/patchcore/      # Memory bank + config.json
├── static/                # Saved overlays, masks, heatmaps
├── templates/index.html   # Web interface
└── logs/                  # CSV logs of predictions

Frontend/
├── static/assets/         # JS, CSS
└── app.js                 # Main frontend logic

````

---

## 🐳 Running with Docker

### CPU mode
```bash
docker compose --profile cpu up --build
````

### GPU mode (if supported)

```bash
docker compose --profile gpu up --build
```

The service will be available at:

```
http://localhost:8000
```

---

## 📌 API Endpoints

### `POST /predict`

Analyze a single image.
Returns:

* score
* anomaly flag
* IoU
* polygons
* defect areas
* overlay URL

### `POST /predict_batch`

Analyze multiple images.
Supports:

* per-image results
* global summary
* optional ground-truth labels for recall

### `GET /health`

Basic health/status info.

---

## 📈 Example Results

* Heatmaps and overlays saved automatically under `/static/overlays/`.
* JSON response includes polygons, IoU, areas, and state labels.

---

## 🛠 Future Improvements

* Memory bank builder for custom datasets.
* Multi-class anomaly models.
* Faster inference with ONNX or TensorRT.
* User authentication dashboard.

---

## 👤 Author

**Jhonnatan Del Castillo**

AI Engineer & Full-Stack Developer

GitHub: [DelcastApe](https://github.com/DelcastApe)

LinkedIn: https://www.linkedin.com/in/jhonnatan-del-castillo-a73a24316/

---

## ⭐ If you find this project useful, consider giving it a star!

```
⭐ Star this repo — it helps a lot!
```

