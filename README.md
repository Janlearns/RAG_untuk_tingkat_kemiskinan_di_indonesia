# RAG Chatbot untuk Analisis Kemiskinan di Indonesia

## 📋 Deskripsi Project

Project ini adalah implementasi **Retrieval Augmented Generation (RAG)** untuk membangun chatbot yang dapat menjawab pertanyaan tentang faktor sosial-ekonomi dan kualitas lingkungan terhadap kemiskinan di Indonesia. Sistem ini menggabungkan Large Language Model (LLM), embedding model, dan vector database untuk memberikan jawaban yang akurat berdasarkan knowledge base yang telah dikurasi.

## 🎯 Tujuan

- Menganalisis faktor-faktor yang mempengaruhi kemiskinan di Indonesia
- Membangun sistem RAG yang dapat memberikan jawaban berdasarkan data dari jurnal akademik
- Mengurangi hallucination dari LLM dengan membatasi konteks dari knowledge base yang spesifik
- Mendemonstrasikan implementasi RAG dalam konteks data science

## 📁 Struktur Project

```
RAG_untuk_tingkat_kemiskinan_di_indonesia/
├── README.md                                    # Dokumentasi project
├── RayzanFazriRamdany_DSML40_Day46.ipynb       # File utama - Jupyter Notebook          # Script Python (referensi)
└── .env                                         # Konfigurasi API (tidak di-track)
```

## 🧠 Knowledge Base

Knowledge base dalam project ini bersumber dari:

- **Jurnal Akademik**: Penelitian dari Google Scholar
- **Format**: File PDF yang diekstrak menjadi teks
- **Topik**: Analisis faktor sosial-ekonomi dan kualitas lingkungan terhadap kemiskinan di Indonesia

### Menambahkan Referensi Jurnal

Untuk menambahkan referensi jurnal baru ke dalam knowledge base, silakan masukkan link jurnal dari Google Scholar:

```
📚 Sumber Jurnal:
Link: https://journal.satyamandiri.com/index.php/iej/article/view/6
Judul: PENGARUH FAKTOR SOSIAL EKONOMI DAN KUALITAS LINGKUNGAN TERHADAP TINGKAT KEMISKINAN DI INDONESIA
Author: Della Nurma Sagita
Tahun: 2026
```

Knowledge base dapat diperbarui secara dinamis melalui fungsi `add_to_knowledge_base()` di dalam notebook.

## 🏗️ Arsitektur Sistem RAG

### Komponen Utama

| Komponen | Pilihan | Alasan |
|----------|---------|--------|
| **Language Model (LLM)** | Groq (llama-3.1-8b-instant) | Gratis, kecepatan respons tinggi, model terbaru |
| **Embedding Model** | Ollama (nomic-embed-text) | Berjalan lokal, tanpa biaya cloud, performa solid |
| **Vector Database** | FAISS (CPU) | Ringan, tidak perlu server eksternal, cocok untuk skala notebook |
| **Text Splitter** | RecursiveCharacterTextSplitter | Mempertahankan konteks antar chunk, mengurangi context fragmentation |

### Alur Sistem

```
Pertanyaan Pengguna
       ↓
Embedding Query
       ↓
Similarity Search (FAISS)
       ↓
Retrieval Top-K Documents
       ↓
Format Context + Prompt Template
       ↓
LLM (Groq) Processing
       ↓
Jawaban Berbasis Knowledge Base
```

## 🚀 Cara Menggunakan

### Prasyarat

1. Python 3.8+
2. Jupyter Notebook atau JupyterLab
3. API Key dari Groq (gratis di [groq.com](https://console.groq.com))
4. Ollama terpasang untuk embedding model lokal

### Instalasi

1. **Clone atau download project ini**

2. **Buat file `.env` di root project:**
   ```
   GROQ_API_KEY=your_groq_api_key_here
   ```

3. **Instal dependencies:**
   ```bash
   pip install langchain-groq langchain-ollama langchain-community faiss-cpu python-dotenv
   ```

4. **Pastikan Ollama berjalan** (untuk embedding):
   ```bash
   ollama pull nomic-embed-text
   ollama serve
   ```

### Menjalankan Project

1. **Buka Jupyter Notebook:**
   ```bash
   jupyter notebook RayzanFazriRamdany_DSML40_Day46.ipynb
   ```

2. **Jalankan semua cell secara berurutan** (Ctrl+A → Shift+Enter)

3. **Berinteraksi dengan chatbot** di cell terakhir:
   - Masukkan pertanyaan Anda
   - Ketik `stop` untuk keluar dari chat loop

## 📊 Hasil Evaluasi

| No | Pertanyaan | Status |
|----|-----------|--------|
| 1 | Sebutkan 3 faktor penyebab kemiskinan di Indonesia | ✅ Terjawab |
| 2 | Hari raya Indonesia | ❌ Diluar Knowledge Base |
| 3 | Sebutkan 3 faktor kemiskinan di Indonesia dalam aspek sosial | ✅ Terjawab |

**Insight:**
- Sistem berhasil menjawab pertanyaan yang relevan dengan knowledge base
- Sistem dengan tepat menolak pertanyaan di luar scope knowledge base (tidak hallucinate)
- Kualitas jawaban sangat bergantung pada struktur dan kejelasan knowledge base

## 💡 Fitur Utama

✨ **Dynamic Knowledge Base Update**
- Tambahkan dokumen baru tanpa rebuild dari awal
- Fungsi `add_to_knowledge_base()` untuk ekspansi dinamis

✨ **Context-Aware Retrieval**
- Mengambil top-K dokumen paling relevan (default: k=3)
- Similarity search berbasis embedding

✨ **Safety Mechanism**
- Prompt template yang jelas untuk membatasi LLM
- Mencegah hallucination dengan phrase "hanya gunakan context yang diberikan"

## 🔍 Teknologi yang Digunakan

- **LangChain**: Framework untuk membangun aplikasi LLM
- **FAISS**: Facebook AI Similarity Search untuk vector operations
- **Ollama**: Local LLM/embedding inference
- **Groq**: Cloud LLM provider untuk inference cepat
- **Python**: Bahasa pemrograman utama

## 🎓 Pembelajaran Utama

1. **Pentingnya Quality Knowledge Base**: Kualitas jawaban sistem sangat bergantung pada struktur dan isi knowledge base
2. **RAG vs Pure LLM**: RAG mengurangi hallucination dengan membatasi konteks pada data spesifik
3. **Trade-off Desain**: Pemilihan chunk_size, embedding model, dan k-value mempengaruhi akurasi

## 🚧 Rekomendasi Pengembangan Lanjutan

1. **Hybrid Search**: Gabungkan dense retrieval (semantic) dengan sparse retrieval (keyword/BM25)
2. **Reranking**: Tambahkan model reranker (misal: Cohere Rerank) untuk mengurutkan ulang hasil retrieval
3. **Evaluasi Kuantitatif**: Gunakan RAGAS framework untuk pengukuran otomatis (faithfulness, relevancy, precision)
4. **Persistent Vector Store**: Simpan FAISS index ke disk agar tidak perlu rebuild
5. **Multi-document QA**: Dukung pertanyaan yang membutuhkan informasi dari multiple documents
6. **Chat History**: Implementasi memory untuk multi-turn conversation

## 📝 Format File

Project menggunakan format **Jupyter Notebook (.ipynb)** sebagai file utama, yang memungkinkan:
- Integrasi code dan dokumentasi
- Visualisasi output langsung
- Eksekusi cell secara interaktif
- Lebih mudah untuk presentasi dan sharing
