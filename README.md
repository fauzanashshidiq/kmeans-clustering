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

<img width="500" alt="image" src="https://github.com/user-attachments/assets/5cbde381-ff3e-4267-b13c-aea37bd0eca4" />

---

### 3. Data Understanding

```python
baca.info()
```

<img width="350" alt="image" src="https://github.com/user-attachments/assets/e062177f-2d58-4d31-9a74-434307f399ab" />


---

### 4. Data Cleaning
Kolom yang memiliki banyak missing value atau tidak diperlukan dihapus.

```python
baca = baca.drop(columns=['linha'])
```

<img width="500" alt="image" src="https://github.com/user-attachments/assets/9dc8aa9b-aa52-4c0c-b900-611844f76fcf" />


---

### 5. Feature Selection

Memvisualkan persebaran data

```python
plt.scatter(baca.distance, baca.speed, s =10, c = "red", marker = "o", alpha = 0.5)
plt.show()
```

<img width="350" alt="output" src="https://github.com/user-attachments/assets/82d11079-7403-4829-86fe-12db3c720435" />

Fitur yang digunakan untuk clustering:

```python
baca_x = baca.iloc[:, 1:3]

x_array = np.array(baca_x)
print(x_array)
```

<img width="150" alt="image" src="https://github.com/user-attachments/assets/36868648-aeb5-4d6b-9d90-38ec976b358b" /> 

---

### 6. Normalisasi Data
Normalisasi dilakukan menggunakan MinMaxScaler agar skala data seragam.

```python
scaler = MinMaxScaler()
x_scaled = scaler.fit_transform(x_array)
```

<img width="150" alt="image" src="https://github.com/user-attachments/assets/d2ace2db-839e-417b-a036-655773bc83fd" />

---

### 7. K-Means Clustering
Model K-Means digunakan untuk membentuk cluster.

```python
kmeans = KMeans(n_clusters=3, random_state=42)
cluster = kmeans.fit_predict(baca)

baca['cluster'] = kmeans.labels_
```

<img width="350" alt="image" src="https://github.com/user-attachments/assets/59a6708e-b58f-441f-ba87-effd379b3205" />

---

### 8. Evaluasi Model
Evaluasi dilakukan menggunakan Silhouette Score.

```python
sil_score = silhouette_score(baca, kmeans.labels_)
print(f"Silhouette Score      : {sil_score:.4f}")
```
<img width="250" alt="image" src="https://github.com/user-attachments/assets/52f7c1d6-8e7d-4a48-96dc-c20805cf5154" />


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

<img width="350" alt="output2" src="https://github.com/user-attachments/assets/58621dd6-f53b-44a1-b74a-ebb65dfb9717" />


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
---

# Mall Customer Segmentation using K-Means Clustering

## Deskripsi Proyek
Proyek ini bertujuan untuk melakukan segmentasi pelanggan mall menggunakan algoritma **K-Means Clustering**. Dengan mengelompokkan pelanggan berdasarkan pendapatan tahunan dan skor pengeluaran, hasil clustering dapat digunakan untuk menyusun strategi pemasaran yang lebih tepat sasaran.

Dataset dianalisis menggunakan Python dengan bantuan library data science seperti Pandas, NumPy, Matplotlib, Seaborn, dan Scikit-Learn.

---

## Dataset
Dataset yang digunakan adalah **Mall Customer Segmentation Data** yang tersedia di Kaggle: [Mall Customer Segmentation Data](https://www.kaggle.com/datasets/vjchoudhary7/customer-segmentation-tutorial-in-python)

Dataset berisi data 200 pelanggan dengan atribut sebagai berikut:

| Kolom | Deskripsi |
|-------|-----------|
| CustomerID | ID unik pelanggan |
| Gender | Jenis kelamin (Male/Female) |
| Age | Usia pelanggan (tahun) |
| Annual Income (k$) | Pendapatan tahunan (dalam ribuan dollar) |
| Spending Score (1-100) | Skor pengeluaran pelanggan di mall |

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
import seaborn as sns
from sklearn.preprocessing import StandardScaler
from sklearn.cluster import KMeans
from sklearn.metrics import silhouette_score
```

### 2. Load Dataset
Dataset dibaca menggunakan Pandas.

```python
df = pd.read_csv('Mall_Customers.csv')
df.head()
```

**Output:**
| CustomerID | Gender | Age | Annual Income (k$) | Spending Score (1-100) |
|------------|--------|-----|--------------------|------------------------|
| 1 | Male | 19 | 15 | 39 |
| 2 | Male | 21 | 15 | 81 |
| 3 | Female | 20 | 16 | 6 |
| 4 | Female | 23 | 16 | 77 |
| 5 | Female | 31 | 17 | 40 |

### 3. Data Understanding

```python
df.info()
```

**Output:**
```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 200 entries, 0 to 199
Data columns (total 5 columns):
 #   Column                  Non-Null Count  Dtype 
---  ------                  --------------  ----- 
 0   CustomerID              200 non-null    int64 
 1   Gender                  200 non-null    object
 2   Age                     200 non-null    int64 
 3   Annual Income (k$)      200 non-null    int64 
 4   Spending Score (1-100)  200 non-null    int64 
dtypes: int64(4), object(1)
memory usage: 7.9+ KB
```

### 4. Exploratory Data Analysis (EDA)

#### Distribusi Data
```python
fig, axes = plt.subplots(2, 2, figsize=(14, 10))

num_cols = ['Age', 'Annual Income (k$)', 'Spending Score (1-100)']

for i, col in enumerate(num_cols):
    ax = axes[i//2][i%2]
    ax.hist(df[col], bins=20, color='#00B4D8', edgecolor='white', alpha=0.7)
    ax.set_title(f'Distribution of {col}', fontweight='bold', fontsize=12)
    ax.set_xlabel(col, fontsize=10)
    ax.set_ylabel('Count', fontsize=10)
    ax.axvline(df[col].mean(), color='#FF6B6B', linestyle='--', linewidth=2, label=f'Mean={df[col].mean():.1f}')
    ax.legend(fontsize=9)
    ax.grid(True, alpha=0.3)

axes[1][1].pie(df['Gender'].value_counts(), labels=['Female', 'Male'],
                colors=['#FF6B6B', '#4ECDC4'], autopct='%1.1f%%', startangle=90,
                textprops={'fontsize': 11, 'fontweight': 'bold'})
axes[1][1].set_title('Gender Distribution', fontweight='bold', fontsize=12)

plt.suptitle('Customer Data — Distributions', fontsize=16, fontweight='bold', color='#2B2D42')
plt.tight_layout()
plt.show()
```

<img width="500" alt="image" src="https://github.com/user-attachments/assets/5b060300-47d4-446c-a8bc-4e94d66ab4a0" />

#### Scatter Plot Income vs Spending Score
```python
colors = {'Male':'#118AB2', 'Female':'#EF476F'}
plt.figure(figsize=(8,6))
for gender, grp in df.groupby('Gender'):
    plt.scatter(grp['Annual Income (k$)'], grp['Spending Score (1-100)'],
                c=colors[gender], label=gender, alpha=0.7, s=60, edgecolors='white', linewidths=0.5)

plt.xlabel('Annual Income (k$)')
plt.ylabel('Spending Score (1-100)')
plt.title('Distribution of Customers by Income and Spending Score')
plt.legend(fontsize=12)
plt.show()
```

<img width="350" alt="image" src="https://github.com/user-attachments/assets/d4541408-1787-4845-8757-6be96f69bc8c" />

#### Correlation Heatmap
```python
plt.figure(figsize=(8, 6))
numeric_cols = df[['Age', 'Annual Income (k$)', 'Spending Score (1-100)']]
sns.heatmap(numeric_cols.corr(), annot=True, fmt='.2f', cmap='coolwarm',
            center=0, square=True, linewidths=0.5)
plt.title('Feature Correlation Heatmap', fontsize=14, fontweight='bold')
plt.tight_layout()
plt.show()
```

<img width="350" alt="image" src="https://github.com/user-attachments/assets/5fba9734-5982-4130-9b57-786d5a65c265" />

### 5. Feature Selection
Fitur yang digunakan untuk clustering adalah `Annual Income (k$)` dan `Spending Score (1-100)`.

```python
X = df[['Annual Income (k$)', 'Spending Score (1-100)']]
```

### 6. Data Scaling
Data distandarisasi menggunakan `StandardScaler` agar kedua fitur memiliki skala yang sama.

```python
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

print(f"Mean: {X_scaled.mean():.2f}")
print(f"Std: {X_scaled.std():.2f}")
```

**Output:**
```
Mean: -0.00
Std: 1.00
```

### 7. Menentukan Jumlah Cluster Optimal (k)

#### Elbow Method
```python
wcss = []
for k in range(1, 11):
    kmeans = KMeans(n_clusters=k, random_state=42, n_init=10)
    kmeans.fit(X_scaled)
    wcss.append(kmeans.inertia_)

plt.figure(figsize=(8,5))
plt.plot(range(1, 11), wcss, marker='o', linestyle='--')
plt.xlabel('Number of Clusters (k)')
plt.ylabel('WCSS (Inertia)')
plt.title('Elbow Method for Optimal k')
plt.show()
```

<img width="350" alt="image" src="https://github.com/user-attachments/assets/56d2d48a-bf49-404b-a1af-b5b083bbf436" />

Dari grafik Elbow, titik "siku" (elbow) terlihat pada **k = 5**.

#### Silhouette Score (Validasi)
```python
sil_scores = []
for k in range(2, 11):
    kmeans = KMeans(n_clusters=k, random_state=42, n_init=10)
    labels = kmeans.fit_predict(X_scaled)
    sil_scores.append(silhouette_score(X_scaled, labels))

plt.figure(figsize=(8,5))
plt.plot(range(2, 11), sil_scores, marker='o', linestyle='--')
plt.xlabel('Number of Clusters (k)')
plt.ylabel('Silhouette Score')
plt.title('Silhouette Score for Optimal k')
plt.show()
```

<img width="350" alt="image" src="https://github.com/user-attachments/assets/d559422c-38f6-42d7-ab90-470b7aec1786" />

Silhouette Score juga mengkonfirmasi bahwa k = 5 adalah pilihan yang baik.

### 8. Membangun Model K-Means
Model K-Means dengan k = 5 dilatih pada data yang telah distandarisasi.

```python
optimal_k = 5
kmeans = KMeans(n_clusters=optimal_k, random_state=42, n_init=10)
clusters = kmeans.fit_predict(X_scaled)

df['Cluster'] = clusters
df[['Annual Income (k$)', 'Spending Score (1-100)', 'Cluster']].head()
```

**Output:**
| | Annual Income (k$) | Spending Score (1-100) | Cluster |
|---|--------------------|------------------------|---------|
| 0 | 15 | 39 | 4 |
| 1 | 15 | 81 | 2 |
| 2 | 16 | 6 | 4 |
| 3 | 16 | 77 | 2 |
| 4 | 17 | 40 | 4 |

### 9. Visualisasi Hasil Clustering
Hasil clustering divisualisasikan dengan scatter plot, menampilkan 5 cluster beserta centroid-nya.

```python
plt.figure(figsize=(10,7))

X_original = df[['Annual Income (k$)', 'Spending Score (1-100)']].values

for cluster in range(optimal_k):
    cluster_data = X_original[clusters == cluster]
    plt.scatter(cluster_data[:, 0], cluster_data[:, 1], 
                label=f'Cluster {cluster}', alpha=0.6, s=50)

centroids = scaler.inverse_transform(kmeans.cluster_centers_)
plt.scatter(centroids[:, 0], centroids[:, 1], c='black', s=200, marker='X',
            label='Centroids', zorder=10, edgecolors='white', linewidths=1.5)

plt.xlabel('Annual Income (k$)', fontsize=12)
plt.ylabel('Spending Score (1-100)', fontsize=12)
plt.title(f'Customer Segments (k={optimal_k})', fontsize=14, fontweight='bold')
plt.legend(loc='best')
plt.grid(True, alpha=0.3)
plt.show()
```

<img width="500" alt="image" src="https://github.com/user-attachments/assets/23ea731e-3fb1-43ea-a57d-1d120fc2f775" />

### 10. Interpretasi Cluster

#### Tabel 1: Karakteristik Utama Setiap Cluster

| Cluster | Usia (tahun) | Pendapatan (k$) | Skor Belanja | Jumlah Pelanggan | Nama Segmentasi |
|:---:|:---:|:---:|:---:|:---:|:---|
| **0** | 42.7 | 55.3 | 49.5 | 81 | **Pelanggan Menengah Stabil** |
| **1** | 32.7 | 86.5 | 82.1 | 39 | **Pelanggan Berpenghasilan Tinggi** |
| **2** | 25.3 | 25.7 | 79.4 | 22 | **Pelanggan Hemat Berbelanja Tinggi** |
| **3** | 41.1 | 88.2 | 17.1 | 35 | **Pelanggan Kaya Namun Hemat** |
| **4** | 45.2 | 26.3 | 20.9 | 23 | **Pelanggan Berpenghasilan Rendah** |

#### Tabel 2: Komposisi Gender per Cluster

| Cluster | Segmentasi | Perempuan | Laki-laki | Dominasi |
|:---:|:---|:---:|:---:|:---|
| **0** | Pelanggan Menengah Stabil | 48 | 33 |  Perempuan (59%) |
| **1** | Pelanggan Berpenghasilan Tinggi | 21 | 18 |  Perempuan (54%) |
| **2** | Pelanggan Hemat Berbelanja Tinggi | 13 | 9 |  Perempuan (59%) |
| **3** | Pelanggan Kaya Namun Hemat | 16 | 19 |  Laki-laki (54%) |
| **4** | Pelanggan Berpenghasilan Rendah | 14 | 9 |  Perempuan (61%) |

**Total Seluruh Pelanggan:** 200 orang
- **Perempuan:** 112 orang (56%)
- **Laki-laki:** 88 orang (44%)
