# Boolean Retrieval System - Sistem Pencarian Berita Olahraga

Sistem pencarian dokumen berbasis Boolean Retrieval yang dirancang khusus untuk pencarian berita olahraga dengan antarmuka interaktif menggunakan Jupyter Notebook.

## 🌟 Fitur Utama

- **Boolean Search**: Mendukung operator AND, OR, dan NOT
- **Phrase Search**: Pencarian frasa dengan tanda kutip
- **Highlighting**: Menyoroti kata kunci dalam hasil pencarian  
- **Interactive Interface**: Antarmuka yang user-friendly dengan Jupyter widgets
- **Flexible CSV Upload**: Mendukung berbagai format kolom CSV
- **Indonesian Stopwords**: Filter kata-kata umum bahasa Indonesia
- **Error Handling**: Penanganan error yang robust dengan fallback search

## 🔧 Requirements

```python
pandas
re (built-in)
collections (built-in)
ipywidgets
IPython
io (built-in)
```

## 📦 Instalasi

1. Install dependencies:
```bash
pip install pandas ipywidgets
```

2. Enable Jupyter widgets:
```bash
jupyter nbextension enable --py widgetsnbextension
```

3. Salin kode ke Jupyter Notebook Anda

## 📊 Format Dataset

Sistem ini mendukung file CSV dengan kolom-kolom berikut:

### Kolom Wajib:
- **Judul**: `judul`, `title`, atau `headline`
- **Konten**: `text`, `content`, `konten`, `isi`, atau `berita`

### Kolom Opsional:
- **Kategori**: `kategori`, `category`, atau `topic`

### Contoh Format CSV:
```csv
judul,konten,kategori
"Timnas Indonesia Menang 2-1","Indonesia berhasil mengalahkan Malaysia dengan skor 2-1 dalam pertandingan persahabatan...","Sepak Bola"
"PSSI Umumkan Pelatih Baru","Persatuan Sepak Bola Seluruh Indonesia mengumumkan pelatih baru untuk timnas...","Sepak Bola"
```

## 🚀 Cara Penggunaan

### 1. Inisialisasi Sistem
```python
system = demo_boolean_retrieval()
```

### 2. Upload Dataset
- Klik tombol "Upload CSV"
- Pilih file CSV berita olahraga Anda
- Sistem akan otomatis memproses dan membangun inverted index

### 3. Melakukan Pencarian

#### Contoh Query:

**Basic Search:**
```
sepak bola
indonesia
```

**Boolean Operators:**
```
timnas AND indonesia
sepak bola OR basket
indonesia NOT malaysia
```

**Phrase Search:**
```
"timnas indonesia"
"piala dunia"
```

**Complex Queries:**
```
(timnas OR PSSI) AND indonesia
sepak bola AND (indonesia OR thailand)
"liga 1" AND NOT persib
```

## 🔍 Operator Boolean yang Didukung

| Operator | Simbol | Deskripsi | Contoh |
|----------|--------|-----------|---------|
| AND | `AND`, `&` | Kedua term harus ada | `sepak AND bola` |
| OR | `OR`, `\|` | Salah satu term harus ada | `sepak OR basket` |
| NOT | `NOT`, `!` | Term tidak boleh ada | `indonesia NOT malaysia` |

## 🏗️ Arsitektur Sistem

### BooleanRetrievalSystem Class

#### Komponen Utama:
- `inverted_index`: Dictionary yang memetakan term ke set dokumen
- `universal_set`: Set semua ID dokumen
- `stopwords`: Daftar kata-kata umum bahasa Indonesia

#### Method Utama:
- `tokenize()`: Preprocessing dan tokenisasi teks
- `build_inverted_index()`: Membangun inverted index
- `boolean_search()`: Melakukan pencarian Boolean
- `highlight_text()`: Menyoroti kata kunci dalam hasil
- `search_and_display()`: Menampilkan hasil pencarian

## 🛠️ Preprocessing

1. **Case Normalization**: Mengubah semua teks ke lowercase
2. **Tokenization**: Memisahkan teks berdasarkan kata
3. **Stopword Removal**: Menghapus kata-kata umum bahasa Indonesia
4. **Length Filtering**: Hanya memproses token dengan panjang > 2 karakter

## 📈 Optimasi Performa

- **Inverted Index**: Struktur data efisien untuk pencarian cepat
- **Set Operations**: Menggunakan operasi set Python untuk Boolean logic
- **Memory Efficient**: Hanya menyimpan referensi dokumen, bukan teks penuh
- **Error Recovery**: Fallback mechanism untuk query yang tidak valid

## 🐛 Error Handling

Sistem dilengkapi dengan penanganan error untuk:
- Query syntax yang tidak valid
- File CSV yang corrupt atau format salah
- Kolom yang hilang atau tidak sesuai
- Dataset kosong atau tidak memenuhi kriteria minimal
- Memory constraints untuk dataset besar

## 💡 Tips Penggunaan

1. **Dataset Quality**: Pastikan setiap dokumen memiliki minimal 20 kata
2. **Query Optimization**: Gunakan term yang spesifik untuk hasil yang lebih akurat
3. **Boolean Logic**: Gunakan tanda kurung untuk query yang kompleks
4. **Phrase Search**: Gunakan tanda kutip untuk pencarian frasa eksak
5. **Fallback Search**: Jika query Boolean gagal, sistem akan melakukan pencarian OR sederhana

## 🔧 Troubleshooting

### Error Upload CSV:
- Pastikan file berformat CSV yang valid
- Periksa encoding file (gunakan UTF-8)
- Pastikan ada kolom judul dan konten

### Hasil Pencarian Kosong:
- Periksa ejaan kata kunci
- Coba gunakan term yang lebih umum
- Periksa sample terms yang ditampilkan sistem
- Gunakan operator OR untuk alternatif

### Performance Issues:
- Batasi ukuran dataset untuk performa optimal
- Gunakan query yang lebih spesifik
- Restart kernel jika memory penuh

## 📝 Contoh Lengkap

```python
# Inisialisasi sistem
system = BooleanRetrievalSystem()

# Manual dataset (opsional)
docs = [
    {"judul": "Timnas Indonesia Menang", "konten": "Indonesia mengalahkan Malaysia 2-1"},
    {"judul": "PSSI Umumkan Pelatih", "konten": "Pelatih baru untuk timnas Indonesia"}
]

system.dataset = docs
system.build_inverted_index(docs)

# Pencarian
results = system.boolean_search("timnas AND indonesia")
print(f"Ditemukan {len(results)} dokumen")
```

## 🎯 Use Cases

- **Media Monitoring**: Monitoring berita olahraga dari berbagai sumber
- **Research**: Penelitian akademik tentang pemberitaan olahraga
- **Content Management**: Manajemen konten portal berita olahraga
- **Archive Search**: Pencarian arsip berita olahraga historis

## 🔮 Future Enhancements

- [ ] Support untuk lebih banyak format file (JSON, XML)
- [ ] Fuzzy search untuk typo tolerance
- [ ] Ranking berdasarkan relevance score
- [ ] Export hasil pencarian ke berbagai format
- [ ] Support untuk multiple languages
- [ ] Advanced query syntax (proximity, wildcard)
- [ ] Machine learning-based result ranking


**Made by Lucians** 
