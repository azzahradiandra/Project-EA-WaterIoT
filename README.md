# 💧 Project EA — Intelligent Water Resource Management using IoT & Predictive Analytics

> **Rancangan Enterprise Architecture IS/IT**  
> Mata Kuliah: Enterprise Architecture  
> Program Studi: Sistem Informasi  

---

## 👥 Anggota Kelompok

| Nama | NIM | Tugas |
|------|-----|-------|
| Azzahra Nayla Diandra | 245150401111044 | Fondasi & Bisnis (Fase Preliminary, A, B) |
| Najwa Tazkiya Rahman | 245150401111042 | Sistem Informasi & Data (Fase C — Aplikasi, ML, ERD) |
| Yasmine Nailatul F.G. | 245150407111005 | Teknologi & Perencanaan (Fase D, E, F, G, H) |

---

## 📌 Deskripsi Proyek

Proyek ini merancang **Enterprise Architecture (EA)** untuk sistem pengelolaan kualitas air berbasis IoT dan analitik prediktif, menggunakan framework **TOGAF ADM**. Sistem ini mengintegrasikan:

- 🌊 **3 node sensor IoT** (Node-A Hulu, Node-B Tengah, Node-C Hilir)
- 📊 **9 parameter kimia air**: pH, Hardness, Solids, Chloramines, Sulfate, Conductivity, Organic Carbon, Trihalomethanes, Turbidity
- 🤖 **Machine Learning**: Random Forest Classifier + SMOTE untuk prediksi potabilitas air
- ⚡ **Real-time monitoring** setiap 15 menit (3.276 baris data)

---

## 🗂️ Struktur Repository

```
Project-EA-WaterIoT/
│
├── README.md                        # Dokumentasi utama
├── .gitignore                       # File yang diabaikan git
│
├── dataset/
│   └── water_potability.csv         # Dataset Water Quality IoT
│
├── notebook/
│   └── RandomForestClassifier.ipynb # Notebook ML Pipeline
│
└── docs/
    ├── EA_WaterIoT_Laporan.md       # Laporan rancangan EA lengkap
    ├── diagrams/
    │   ├── 01_ea_overview.puml      # EA Overview (Three-Layer)
    │   ├── 02_togaf_adm.puml        # TOGAF ADM Flow
    │   ├── 03_value_chain.puml      # Value Chain Diagram
    │   ├── 04_business_process.puml # Business Process Flow
    │   ├── 05_usecase.puml          # Use Case Diagram
    │   ├── 06_ml_pipeline.puml      # ML Pipeline Diagram
    │   ├── 07_erd.puml              # Entity Relationship Diagram
    │   ├── 08_technology.puml       # Technology Architecture
    │   └── 09_migration.puml        # Migration Planning Gantt
    └── artifacts/
        ├── capability_map.md        # Capability Map
        ├── archimate_views.md       # ArchiMate Diagram (teks)
        ├── gap_analysis.md          # Analisa Gap Bisnis & SI
        └── technology_catalog.md   # Technology Portfolio Catalog
```

---

## 🔬 ML Pipeline — Ringkasan Hasil

### Dataset
| Atribut | Nilai |
|---------|-------|
| Jumlah baris | 3.276 |
| Jumlah fitur | 9 parameter kimia |
| Target | Potability (0 = tidak layak, 1 = layak) |
| Missing values | Ada di beberapa kolom |

### Hasil Model

#### Random Forest — Sebelum SMOTE (Baseline)
| Metrik | Kelas 0 | Kelas 1 | Overall |
|--------|---------|---------|---------|
| Precision | 0.69 | 0.60 | — |
| Recall | 0.87 | 0.34 | — |
| F1-Score | 0.77 | 0.43 | 0.60 (macro) |
| **Accuracy** | — | — | **0.6707** |

> ⚠️ Model bias ke kelas 0 (tidak layak) karena data imbalanced.

#### Random Forest — Setelah SMOTE ✅
| Metrik | Kelas 0 | Kelas 1 | Overall |
|--------|---------|---------|---------|
| Precision | 0.69 | 0.73 | — |
| Recall | 0.75 | 0.67 | — |
| F1-Score | 0.72 | 0.70 | 0.71 (macro) |
| **Accuracy** | — | — | **0.7075** |

> ✅ Model lebih seimbang setelah SMOTE — kedua kelas memiliki performa yang adil.

### Perbandingan
```
Accuracy sebelum SMOTE : 67.07%
Accuracy setelah SMOTE : 70.75%
Peningkatan            : +3.68%
F1-Score macro (before): 0.60
F1-Score macro (after) : 0.71  ← lebih representatif
```

---

## 🏗️ Arsitektur Sistem (Ringkasan)

```
┌─────────────────────────────────────────────────────┐
│                  BUSINESS LAYER                      │
│   Operator Lapangan · Manajer Air · Regulator        │
├─────────────────────────────────────────────────────┤
│                 APPLICATION LAYER                    │
│  Monitoring RT · ML Prediksi · Alert · Pelaporan     │
├─────────────────────────────────────────────────────┤
│                 TECHNOLOGY LAYER                     │
│  IoT Sensor · MQTT · Spark · InfluxDB · MySQL        │
│  Python/sklearn · FastAPI · Grafana · Ubuntu Server  │
└─────────────────────────────────────────────────────┘
```

---

## 🚀 Cara Menjalankan Notebook

### Prasyarat
```bash
pip install pandas scikit-learn imbalanced-learn matplotlib
```

### Jalankan
```bash
jupyter notebook notebook/RandomForestClassifier.ipynb
```

Atau upload ke [Kaggle](https://kaggle.com) dengan dataset dari:  
`dataset/water_potability.csv`

---

## 📚 Referensi

1. Kelompok 2 SI 5C UIN Suska Riau, *"Project Case Study Rancangan EA IS/IT (Studi Kasus: PT. Adei Plantation & Industry)"*, 2024.
2. PBGC, *"Enterprise Architecture Blueprint"*, www.pbgc.gov.
3. The Open Group, *"TOGAF Standard, Version 9.2"*.
4. Permenkes No. 492/MENKES/PER/IV/2010 tentang Persyaratan Kualitas Air Minum.

---

## 📄 Lisensi

Proyek ini dibuat untuk keperluan akademik — Mata Kuliah Enterprise Architecture, UIN Suska Riau 2024.
