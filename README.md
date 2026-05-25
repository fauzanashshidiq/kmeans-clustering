# K-Means Clustering GPS Trajectories

- Nama: Muhammad Fauzan Ashshidiq
- NIM: 1237050051
- Kelas: IF-C
- Pembelajaran Mesin

## Deskripsi Proyek
Proyek ini bertujuan untuk melakukan clustering terhadap data GPS trajectories menggunakan algoritma K-Means Clustering. 

Dataset dianalisis menggunakan Python dengan bantuan library data science seperti Pandas, NumPy, Matplotlib, dan Scikit-Learn.

---

## Dataset
Dataset berisi data perjalanan GPS dengan beberapa atribut, seperti:

| Kolom | Deskripsi |
|---|---|
| id | ID data |
| id_android | ID perangkat Android |
| speed | Kecepatan kendaraan |
| distance | Jarak tempuh |
| rating | Rating perjalanan |
| car_or_bus | Jenis kendaraan |
| linha | Jalur/route |

---

## Tools & Library
Project ini menggunakan beberapa library berikut:

```python
pandas
numpy
matplotlib
seaborn
scikit-learn
```

Install dependencies:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

---

## Tahapan Project

### 1. Import Library
Library yang digunakan untuk analisis data, visualisasi, dan machine learning diimport terlebih dahulu.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans
from sklearn.preprocessing import MinMaxScaler
from sklearn.metrics import silhouette_score
```

---

### 2. Load Dataset
Dataset dibaca menggunakan Pandas.

```python
baca = pd.read_csv('go_track_tracks.csv')
```

---

### 3. Data Understanding
Dilakukan pengecekan:
- Struktur dataset
- Tipe data
- Missing values
- Statistik deskriptif

```python
baca.info()
baca.describe()
```

---

### 4. Data Cleaning
Kolom yang memiliki banyak missing value atau tidak diperlukan dihapus.

```python
baca = baca.drop(columns=['linha'])
```

---

### 5. Feature Selection
Fitur yang digunakan untuk clustering:

```python
baca_x = baca.iloc[:, 1:3]

x_array = np.array(baca_x)
print(x_array)
```

Memvisualkan persebaran data

```python
plt.scatter(baca.distance, baca.speed, s =10, c = "red", marker = "o", alpha = 0.5)
plt.show()
```

<img width="552" height="415" alt="output" src="https://github.com/user-attachments/assets/82d11079-7403-4829-86fe-12db3c720435" />


---

### 6. Normalisasi Data
Normalisasi dilakukan menggunakan MinMaxScaler agar skala data seragam.

```python
scaler = MinMaxScaler()
x_scaled = scaler.fit_transform(x_array)
```

---

### 7. K-Means Clustering
Model K-Means digunakan untuk membentuk cluster.

```python
kmeans = KMeans(n_clusters=3, random_state=42)
cluster = kmeans.fit_predict(baca)

baca['cluster'] = kmeans.labels_
```

---

### 8. Evaluasi Model
Evaluasi dilakukan menggunakan Silhouette Score.

```python
sil_score = silhouette_score(baca, kmeans.labels_)
print(f"Silhouette Score      : {sil_score:.4f}")
```

Semakin mendekati 1, maka kualitas cluster semakin baik.

---

### 9. Visualisasi Cluster
Hasil clustering divisualisasikan menggunakan scatter plot.

```python
plt.figure(figsize=(8,6))

plt.scatter(
    baca['id_android'],
    baca['speed'],
    c=baca['kluster'],
    cmap='viridis'
)

plt.scatter(
    kmeans.cluster_centers_[:, 1],   # Frequency
    kmeans.cluster_centers_[:, 2],   # Monetary
    s=200,
    c='red',
    marker='X',
    label='Centroid'
)

plt.xlabel('Frequency')
plt.ylabel('Monetary')
plt.title('K-Means Clustering')
plt.legend()

plt.show()
```

<img width="695" height="547" alt="output2" src="https://github.com/user-attachments/assets/58621dd6-f53b-44a1-b74a-ebb65dfb9717" />


---

## Evaluasi
Model dievaluasi menggunakan:
- Silhouette Score

Evaluasi membantu mengetahui seberapa baik pemisahan antar cluster.

---

## Struktur Project

```bash
├── README.md
└── gps_trajectories
    ├── kmeans_clustering_gps_trajectories.ipynb
    └── go_track_tracks.csv
```

---
