# Eksplor-Data-Titanic

**Laporan Singkat:****

1. Eksplorasi Data

Dataset Titanic memiliki variabel numerik (Age, Fare, SibSp, Parch) dan kategorikal (Sex, Pclass, Embarked).

Terdapat missing values pada kolom Age, Cabin, dan Embarked.

2. Visualisasi Data & Insight

Survival Rate: Mayoritas penumpang tidak selamat (sekitar 62%).

Gender: Perempuan memiliki peluang selamat lebih tinggi dibanding laki-laki.

Age: Anak-anak memiliki survival rate lebih tinggi dibanding dewasa.

Class (Pclass): Penumpang kelas 1 jauh lebih banyak selamat dibanding kelas 3.

Embarked: Penumpang dari pelabuhan C cenderung lebih banyak selamat dibanding dari pelabuhan lain.

Fare: Penumpang dengan tiket mahal memiliki peluang selamat lebih tinggi.

3. Korelasi Antar Variabel

Fare berkorelasi negatif dengan Pclass → semakin mahal tiket, semakin tinggi kelas.

Survived punya korelasi kuat dengan Sex (-0.54) dan Pclass (-0.34).

4. Kesimpulan

Faktor yang paling berpengaruh terhadap keselamatan: Jenis kelamin, kelas penumpang, umur, dan harga tiket.

Pola ini menggambarkan bahwa penumpang perempuan, anak-anak, dan penumpang kelas atas memiliki kemungkinan lebih tinggi untuk selamat.

**Code**

# ==================================
# 1. Import Library
# ==================================
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# Styling default
sns.set(style="whitegrid")

# ==================================
# 2. Load Dataset
# ==================================
# ganti path sesuai lokasi dataset kamu
df = pd.read_csv("titanic.csv")

# ==================================
# 3. Eksplorasi Data Awal
# ==================================
print("\n--- Info Dataset ---")
print(df.info())

print("\n--- Statistik Deskriptif ---")
print(df.describe(include="all"))

print("\n--- Missing Values ---")
print(df.isnull().sum())

# ==================================
# 4. Visualisasi Distribusi Variabel
# ==================================

# Distribusi Survived
plt.figure(figsize=(6,4))
sns.countplot(data=df, x="Survived", palette="Set2")
plt.title("Distribusi Korban Titanic (Selamat vs Tidak)")
plt.show()

# Gender vs Survival
plt.figure(figsize=(6,4))
sns.countplot(data=df, x="Sex", hue="Survived", palette="coolwarm")
plt.title("Perbandingan Kelamin dengan Survival")
plt.show()

# Distribusi Umur
plt.figure(figsize=(8,5))
sns.histplot(data=df, x="Age", hue="Survived", kde=True, bins=30, palette="Set1")
plt.title("Distribusi Umur berdasarkan Survival")
plt.show()

# Pclass vs Survival
plt.figure(figsize=(6,4))
sns.countplot(data=df, x="Pclass", hue="Survived", palette="pastel")
plt.title("Kelas Penumpang vs Survival")
plt.show()

# Embarked vs Survival
plt.figure(figsize=(6,4))
sns.countplot(data=df, x="Embarked", hue="Survived", palette="muted")
plt.title("Pelabuhan Keberangkatan vs Survival")
plt.show()

# ==================================
# 5. Korelasi Antar Variabel Numerik
# ==================================
plt.figure(figsize=(10,6))
sns.heatmap(df.corr(numeric_only=True), annot=True, cmap="Blues", fmt=".2f")
plt.title("Heatmap Korelasi Variabel Numerik")
plt.show()

# ==================================
# 6. Analisis Fare
# ==================================
plt.figure(figsize=(7,5))
sns.boxplot(data=df, x="Survived", y="Fare", palette="Set3")
plt.title("Distribusi Harga Tiket berdasarkan Survival")
plt.show()

# ==================================
# 7. Insight Singkat (Output ke Terminal)
# ==================================
print("\n===== INSIGHT SINGKAT =====")
print("- Mayoritas penumpang tidak selamat (~62%).")
print("- Perempuan memiliki peluang selamat lebih tinggi daripada laki-laki.")
print("- Anak-anak lebih cenderung selamat dibanding dewasa.")
print("- Penumpang kelas 1 lebih banyak selamat dibanding kelas 3.")
print("- Penumpang dari pelabuhan C cenderung lebih banyak selamat.")
print("- Penumpang dengan tiket mahal memiliki peluang selamat lebih tinggi.")
print("- Variabel yang paling berpengaruh: Sex, Pclass, Age, Fare.")
