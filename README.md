# 📊 Principal Component Analysis (PCA) for Molecular Dynamics

This repository provides a **Python-based workflow** to perform **2D and 3D Principal Component Analysis (PCA)** on molecular dynamics trajectories.

It is especially useful for analyzing **protein conformational dynamics, clustering, and motion patterns** from simulations generated using GROMACS.

---

## 🧬 Overview

Principal Component Analysis (PCA), also known as **Essential Dynamics**, helps to:

* Identify dominant motions in proteins
* Reduce high-dimensional trajectory data
* Visualize conformational space
* Compare structural changes between systems

---

## 📌 Features

* ✅ PCA computation from trajectory data
* ✅ 2D PCA plots (PC1 vs PC2)
* ✅ 3D PCA plots (PC1 vs PC2 vs PC3)
* ✅ Clustering-ready outputs
* ✅ Compatible with GROMACS `.xtc` and `.gro` files
* ✅ Google Colab and local execution supported

---

## ⚙️ Workflow (GROMACS → PCA)

```bash
# Step 1: Remove periodic boundary conditions
gmx trjconv -s topol.tpr -f traj.xtc -o traj_noPBC.xtc -pbc mol -center

# Step 2: Calculate covariance matrix
gmx covar -s topol.tpr -f traj_noPBC.xtc -o eigenval.xvg -v eigenvec.trr

# Step 3: Project trajectory onto eigenvectors
gmx anaeig -v eigenvec.trr -f traj_noPBC.xtc -proj pca_proj.xvg
```

---

## 📂 Input

* `pca_proj.xvg` → PCA projection data
* Columns:

  * Column 1 → Time
  * Column 2 → PC1
  * Column 3 → PC2
  * Column 4 → PC3

---

## 🚀 Usage (Python / Colab)

### 🔹 2D PCA Plot

```python
import numpy as np
import matplotlib.pyplot as plt

data = np.loadtxt("pca_proj.xvg", comments=['@','#'])

pc1 = data[:,1]
pc2 = data[:,2]

plt.figure(figsize=(6,5))
plt.scatter(pc1, pc2, c=data[:,0], cmap='viridis', s=5)
plt.xlabel("PC1")
plt.ylabel("PC2")
plt.title("2D PCA Plot")
plt.colorbar(label="Time (ps)")
plt.show()
```

---

### 🔹 3D PCA Plot

```python
from mpl_toolkits.mplot3d import Axes3D
import matplotlib.pyplot as plt

pc1 = data[:,1]
pc2 = data[:,2]
pc3 = data[:,3]

fig = plt.figure(figsize=(7,6))
ax = fig.add_subplot(111, projection='3d')

p = ax.scatter(pc1, pc2, pc3, c=data[:,0], cmap='viridis', s=5)

ax.set_xlabel("PC1")
ax.set_ylabel("PC2")
ax.set_zlabel("PC3")

fig.colorbar(p, label="Time (ps)")
plt.title("3D PCA Plot")
plt.show()
```

---

## 📊 Output Interpretation

* **Clusters** → Stable conformational states
* **Spread** → Flexibility of protein
* **Compact region** → Stable structure
* **Wide distribution** → High dynamics

---

## 🧠 Applications

* Drug binding effect analysis
* Apo vs holo comparison
* Protein folding/unfolding
* Conformational clustering
* Essential motion analysis

---

## 🛠️ Dependencies

* Python 3.x
* NumPy
* Matplotlib
* mpl_toolkits (for 3D plotting)

---

## 🔥 Advanced Extensions

* 🔹 K-means clustering on PCA space
* 🔹 Free energy landscape (FEL)
* 🔹 Combine PCA with DSSP analysis
* 🔹 Time-resolved PCA trajectories

---

## 📈 Future Improvements

* Automated pipeline (GROMACS → PCA → Plot)
* Interactive 3D visualization
* Integration with machine learning clustering
* GPU acceleration

---

## 👨‍🔬 Author

**Rajesh S.**
M.Sc. Biochemistry
Research: Molecular modeling, drug design, computational biology

---

## 📜 License

MIT License

---

## ⭐ Acknowledgment

Please cite relevant tools such as:

* GROMACS
* PCA / Essential Dynamics methods

---
