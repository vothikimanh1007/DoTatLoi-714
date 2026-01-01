# DoTatLoi-714: Vietnamese Traditional Medicine Graph Benchmark 🌿💊

**DoTatLoi-714** is a curated, low-resource graph dataset for **Vietnamese Traditional Medicine (VTM)**. It is digitized from the classic pharmacopoeia *"Những cây thuốc và vị thuốc Việt Nam"* by Prof. Do Tat Loi.

This benchmark is designed to evaluate **Graph Neural Networks (GNNs)** and **Hypergraph models** on tasks like:
* Herbal Synergy Prediction
* Functional Clustering

## 📂 Dataset Structure

The dataset consists of three main CSV files located in the `data/` directory:

### 1. `ViThuoc.csv` (Herbs / Nodes)
Contains metadata for **714 herbs**.
* **ID_ViThuoc:** Unique integer ID (e.g., 1, 2, ...).
* **TenVietNam:** Vietnamese name of the herb.
* **TenKhoaHoc:** Scientific name (Latin).
* **TinhVi:** Nature and Taste (e.g., "Vị cay, tính ấm").
* **QuyKinh:** Meridian tropism (e.g., "Quy kinh Can, Thận").

### 2. `CongThuc_Cleaned.csv` (Formulas / Hyperedges)
Represents the many-to-many relationships between herbs and prescriptions.
* **ID_BaiThuoc:** Unique ID for the prescription formula.
* **ID_ViThuoc:** ID of the herb used in that formula.

> **Note:** This file corresponds to the **Hypergraph Incidence Matrix**.

### 3. `BaiThuoc.csv` (Formula Metadata)
Contains details about the prescriptions.
* **ID_BaiThuoc:** Formula ID.
* **TenBaiThuoc:** Name of the formula (e.g., "Cao Ích Mẫu").
* **ChuTri:** Therapeutic indications (what disease it treats).

## 🚀 Usage

### Requirements
* Python 3.8+
* PyTorch
* PyTorch Geometric
* Pandas, NetworkX

##📊 Benchmarking Results
We benchmarked this dataset using HyperG-TCM, a Heterogeneous Hypergraph Neural Network.

| Model | Graph Type | Test AUC | Test AP |
| :--- | :--- | :--- | :--- |
| GCN | Pairwise | 0.8571 | 0.9286 |
| GAT | Pairwise | 1.0000 | 1.0000 |
| HyperG-TCM | Hypergraph | 1.0000 | 1.0000 |
Note: While accuracy saturates on this small pilot set, HyperG-TCM achieves 50% lower training loss, indicating better structural understanding.

##📜 Citation
If you use this dataset in your research, please cite our paper:
@article{HyperG_TCM_2026,
  title={HyperG-TCM: A Heterogeneous Hypergraph Framework for Unveiling Herbal Synergy in Low-Resource Traditional Medicine},
  author={Vo Thi Kim Anh},
  journal={Proceedings of the [Conference Name]},
  year={2026}
}

##⚖️ License

This dataset is licensed under the Creative Commons Attribution 4.0 International (CC BY 4.0).
Original content copyright belongs to the publisher of "Những cây thuốc và vị thuốc Việt Nam". This dataset is a derived work for academic research purposes.

Contact: Vo Thi Kim Anh (vothikimanh@tdtu.edu.vn, thi.kim.anh.vo.st@vsb.cz)

### Quick Start (Loading the Graph)

```python
import pandas as pd
import torch
from torch_geometric.data import HeteroData

# Load Data
df_herbs = pd.read_csv('data/ViThuoc.csv')
df_formulas = pd.read_csv('data/CongThuc_Cleaned.csv')

# Example: Inspecting a formula
formula_id = 101
herbs_in_formula = df_formulas[df_formulas['ID_BaiThuoc'] == formula_id]['ID_ViThuoc'].tolist()

print(f"Herbs in Formula {formula_id}: {herbs_in_formula}")



