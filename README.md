
# 🌐 PathCore: Dashboard Monitoring Infrastruktur Jaringan

**PathCore** adalah solusi manajemen infrastruktur jaringan yang dirancang khusus untuk mengatasi kendala operasional pada *Internet Service Provider* (ISP) berskala besar. Sistem ini mendigitalisasi pemetaan topologi jaringan untuk mengotomatisasi identifikasi pelanggan terdampak saat terjadi gangguan massal.

---

## 🚩 Latar Belakang (Problem Statement)
Dalam operasional ISP, gangguan massal seperti *device failure*, *link down*, atau masalah pada *upstream* sering kali menjadi momen kritis. Kendala utama yang dihadapi adalah:
* **Identifikasi Manual:** Proses menentukan pelanggan mana saja yang terdampak sering kali memakan waktu lama karena data tersebar.
* **Faktor Memori Manusia:** Teknisi sering kali harus mengandalkan ingatan terhadap ratusan topologi yang kompleks untuk menentukan jalur routing.
* **Inefisiensi SLA:** Keterlambatan identifikasi menghambat pengiriman notifikasi ke pelanggan dan pendokumentasian laporan SLA (*Service Level Agreement*).
* **Risiko Operasional:** Proses identifikasi yang lambat berisiko menurunkan tingkat kepuasan pelanggan dan akurasi data laporan ke manajemen.

## 💡 Solusi: PathCore
PathCore hadir untuk memetakan hubungan antara infrastruktur fisik (Gateway, Link, Upstream) dengan layanan logika pelanggan melalui database relasional yang terstruktur. 

### Fitur Utama:
* **Network Inventory Management:** Pendataan perangkat *gateway*, *link* interkoneksi, dan rekanan penyedia jaringan secara terpusat.
* **Dynamic Routing Mapping:** Pemetaan alokasi IP pelanggan ke jalur routing tertentu dengan klasifikasi *Main Link* atau *Backup Link*.
* **Real-time Verification:** Validasi cepat notifikasi gangguan untuk menghindari *false alarm* dari sistem monitoring.
* **Automated Impact Analysis:** Penarikan data pelanggan terdampak secara instan untuk kebutuhan notifikasi massal dan pembukaan tiket gangguan.

---

## 🛠️ Perancangan Basis Data (ERD)

Desain database PathCore difokuskan pada kecepatan *query* untuk mendapatkan data pelanggan dari titik gangguan terkecil sekalipun.

### Tautan ERD
Anda dapat melihat rancangan database secara interaktif melalui tautan berikut:
🔗 **[Live ERD - PathCore Dashboard](https://dbdiagram.io/d/db_pathcore_dashbord-69d1485a80896296841ca27b)**

### Logika Relasi Utama:
1. **Core Infrastructure:** Tabel `gateways` dan `providers` mendefinisikan aset fisik.
2. **Path Mapping:** Tabel `routing_paths` menghubungkan gateway ke provider dan menentukan peran link (Main/Backup).
3. **Impact Bridge:** Tabel `ip_allocations` menjadi jembatan antara teknis jaringan (`routing_paths`) dan data layanan pelanggan (`subscriptions`).

---

## 🔄 Alur Kerja Sistem (System Workflow)

1. **Input Data:**
   - **Marketing/Admin:** Menginput data pelanggan, produk, dan status layanan.
   - **NetworkOps:** Menginput perangkat, link interkoneksi, alokasi IP, dan memetakan jalur routingnya.
2. **Monitoring & Verifikasi:**
   - Tim memantau jaringan. Jika terjadi gangguan, sistem memvalidasi apakah gangguan tersebut bersifat valid (bukan *false alarm* monitoring).
3. **Analisis Dampak:**
   - Saat link dikonfirmasi *down*, sistem menjalankan query untuk menarik daftar pelanggan yang menggunakan jalur tersebut.
4. **Notifikasi & Dokumentasi:**
   - Sistem mengirimkan notifikasi (WA/Email) kepada pelanggan terdampak dan membuka tiket gangguan otomatis untuk perhitungan durasi SLA.

---