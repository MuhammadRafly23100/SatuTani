Build a complete Flutter mobile application called "TaniDirect" — a Direct 
Farmer-to-Consumer Food Platform. Use mock data for all content.

---

## TECH STACK
* Flutter (Dart) + Material 3
* State Management: Riverpod
* Navigation: GoRouter
* Charts: fl_chart
* Fonts: Google Fonts (Plus Jakarta Sans)

---

## COLOR THEME
```dart
class AppColors {
  static const primary      = Color(0xFF2D7D46); // hijau pertanian
  static const primaryLight = Color(0xFFE8F5E9);
  static const primaryDark  = Color(0xFF1B5E20);
  static const secondary    = Color(0xFFF5A623); // kuning panen
  static const secondaryLight = Color(0xFFFFF8E7);
  static const success      = Color(0xFF388E3C);
  static const warning      = Color(0xFFF57C00);
  static const danger       = Color(0xFFD32F2F);
  static const info         = Color(0xFF1976D2);
  static const background   = Color(0xFFF9F7F2); // putih hangat
  static const surface      = Color(0xFFFFFFFF);
  static const textPrimary  = Color(0xFF1A1A1A);
  static const textSecondary= Color(0xFF6B7280);
  static const border       = Color(0xFFE5E7EB);
}
```

Status badge colors:
* Menunggu     → background: 0xFFFFF3E0, text: 0xFFE65100
* Dikonfirmasi → background: 0xFFE3F2FD, text: 0xFF1565C0
* Dipanen      → background: 0xFFE8F5E9, text: 0xFF2D7D46
* Dikirim      → background: 0xFFF3E5F5, text: 0xFF6A1B9A
* Selesai      → background: 0xFFE8F5E9, text: 0xFF1B5E20
* Dibatalkan   → background: 0xFFFFEBEE, text: 0xFFB71C1C

---

## FEATURES

### ONBOARDING
* Splash screen: logo animasi fade-in + loading bar
* Welcome: 3 slide carousel dengan smooth_page_indicator
  - Slide 1: "Dari Kebun Langsung ke Mejamu"
  - Slide 2: "AI Bantu Prediksi Harga Terbaik"
  - Slide 3: "Lacak Produkmu Sampai ke Pintu"
* Role select: 2 kartu besar — Petani dan Pembeli/Konsumen

---

### AUTH
* Login: email + password, show/hide toggle, Google login button (mockup)
* Register Petani: stepper 3 langkah
  - Step 1: Data diri (nama, email, no HP, password)
  - Step 2: Data kebun (nama kebun, provinsi, kabupaten, luas lahan, ID Gapoktan, 
    multi-select komoditas chips)
  - Step 3: Verifikasi (upload KTP, nomor rekening, nama bank)
* Register Konsumen: form singkat + pilih tipe 
  (Individu | Restoran | Hotel | Kantin | Institusi)

---

### FARMER APP (Bottom Nav: Beranda | Produk | Pesanan | Pendapatan | Profil)

**Beranda**
* Header: sapaan + tanggal + notifikasi bell + avatar
* KPI cards horizontal scroll:
  Pendapatan Hari Ini | Pesanan Aktif | Stok Hampir Habis | Rating
* Banner peringatan panen: "🌾 Panen Tomat dalam 3 hari"
* Quick actions 2x2 grid: Tambah Produk | Cek Harga AI | Prakiraan Pasar | Ajukan KUR
* Pesanan terbaru (3 item) + "Lihat Semua"
* AI price alert banner: harga komoditas naik/turun

**Produk Saya**
* Filter chips: Semua | Aktif | Habis | Pre-Order
* List produk: thumbnail + nama + harga + stok progress bar + status toggle + 
  3-dot menu (edit, hapus, duplikat)
* FAB: "+ Tambah Produk"
* Empty state: ilustrasi + pesan + tombol tambah

**Tambah / Edit Produk**
* Upload 3 foto (kamera/galeri)
* Fields: nama, kategori (bottom sheet), harga/kg, stok (kg), 
  estimasi panen (date picker), metode pertanian (radio: Organik|Konvensional|Semi-Organik), 
  toggle pre-order, deskripsi
* Bottom bar fixed: tombol Simpan

**Pesanan**
* Tab bar: Semua | Menunggu | Dikonfirmasi | Dipanen | Dikirim | Selesai
* Order card: ID pesanan, nama konsumen + tipe, list produk, total, status badge
* Action button sesuai status:
  - Menunggu → "Konfirmasi" (hijau) + "Tolak" (merah outline)
  - Dikonfirmasi → "Tandai Sudah Dipanen"
  - Dipanen → "Hubungi Kurir"
* Detail pesanan: info konsumen, breakdown harga, timeline status, generate QR produk

**AI Pricing Advisor**
* Form: komoditas (bottom sheet + search), provinsi, kuantitas (slider), 
  kualitas (Grade A/B/C segmented)
* Tombol "Analisis Sekarang"
* Result card slide-up:
  - Harga rekomendasi (besar, hijau)
  - Range harga pasar
  - Tren badge: ↑ Naik / ↓ Turun / → Stabil
  - Bar chart: harga perantara vs harga TaniDirect vs rekomendasi
  - Teks reasoning AI

**Prakiraan Permintaan**
* Tab komoditas: Bawang Merah | Cabai | Tomat | Beras | Sayuran
* Line chart 4 minggu ke depan (fl_chart)
* Tabel demand per provinsi dengan badge: Tinggi | Sedang | Rendah
* Event cards: "Ramadan +45% demand sayuran"
* Rekomendasi box hijau: saran tanam minggu ini

**Pendapatan**
* Summary cards: Total Bulan Ini | Transaksi Selesai | Rata-rata per Order
* Grouped bar chart: "Pendapatan dengan Perantara" (merah) vs 
  "Pendapatan TaniDirect" (hijau) — 6 bulan terakhir
* Tabel riwayat: tanggal, produk, pembeli, jumlah, komisi, diterima petani
* Tombol "Cairkan Dana" (mockup)

**Profil Petani**
* Cover photo + avatar + nama + verifikasi badge
* Stats row: Total Penjualan | Rating | Bergabung Sejak | Komoditas
* Menu list: Edit Profil | Rekening Bank | Notifikasi | Bantuan | Keluar

---

### CONSUMER APP (Bottom Nav: Beranda | Jelajahi | Keranjang | Pesanan | Profil)

**Beranda**
* Header: sapaan + lokasi + notifikasi bell + avatar
* Search bar: "Cari produk segar dari petani..."
* Banner promo carousel (3 banner)
* Kategori horizontal scroll icons:
  🥬 Sayuran | 🍎 Buah | 🌾 Beras | 🌶️ Rempah | 🐟 Ikan
* Produk terpopuler: grid 2 kolom ProductCard
* Petani terdekat: horizontal scroll FarmerCard
* Subscription CTA banner: "Langganan Paket Sayur Mingguan"
* Flash sale section (jika ada pre-order murah)

**Jelajahi Produk**
* Search bar sticky + filter icon
* Filter bottom sheet:
  - Kategori (checkboxes)
  - Provinsi (dropdown)
  - Harga (range slider: Rp 0 – Rp 100.000/kg)
  - Toggle: Organik saja | Pre-Order Tersedia
  - Sort: Termurah | Terpopuler | Terbaru | Terdekat
* Toggle view: Grid 2 kolom | List
* ProductCard: foto, nama, harga/kg, nama petani + lokasi, 
  badge organik, badge pre-order, stok indicator, tombol "Pesan"

**Detail Produk**
* Image carousel dengan thumbnail row
* Nama, kategori badge, organik badge
* Harga besar (hijau) + stok progress bar
* Estimasi panen chip
* Farmer info card: avatar, nama kebun, lokasi, verifikasi badge, rating, 
  "Lihat Profil" link
* QR Traceability preview card:
  - QR code mockup kecil
  - Tanggal tanam, tanggal panen, status pestisida
  - "Scan untuk Detail Lengkap"
* Ulasan: rata-rata bintang + bar breakdown + review cards
* Produk serupa horizontal scroll
* Bottom bar fixed: quantity picker (- angka +) + "Pesan Sekarang" + 
  "Pre-Order" (jika tersedia)

**Direktori Petani**
* Search bar + filter provinsi
* Toggle: Grid | Map view (flutter_map dengan marker tiap petani)
* FarmerCard: foto kebun, nama petani, lokasi, rating, jumlah produk aktif,
  komoditas chips, "Lihat Produk" tombol

**Profil Petani Publik**
* Cover photo + avatar + nama + verifikasi badge + lokasi
* Stats row: Total Terjual | Rating | Sejak | Komoditas
* Mini map lokasi kebun
* Grid produk aktif (reuse ProductCard)
* Ulasan section

**Keranjang**
* List item: foto, nama, petani, quantity stepper, harga, hapus
* Estimasi berat total
* Form alamat pengiriman (text field + "Pilih di Peta" button)
* Pilih jadwal pengiriman (date picker)
* Ringkasan order: subtotal, ongkir, biaya platform, total
* Tombol "Lanjut ke Pembayaran"

**Checkout & Pembayaran**
* Review item list (compact, read-only)
* Alamat konfirmasi
* Pilih metode pembayaran (radio cards dengan logo):
  QRIS | Virtual Account BRI/BCA/Mandiri | GoPay | OVO | Dana
* Promo code field
* Breakdown harga
* Tombol "Bayar Sekarang — Rp X.XXX.XXX"
* Order success screen: animasi centang + order ID + 
  tombol "Lacak Pesanan" & "Belanja Lagi"

**Pesanan**
* Tab: Semua | Menunggu | Dikonfirmasi | Dikirim | Selesai | Dibatalkan
* Order card: foto produk, nama, petani, total, status badge, 
  tombol "Lacak" & "Nilai"
* Detail + Tracking screen:
  - Order info header
  - Status stepper vertikal:
    ✓ Pesanan Dikonfirmasi → ✓ Dipanen Petani → Dijemput Kurir → 
    Dalam Perjalanan → Diterima
  - Peta rute pengiriman (mockup flutter_map)
  - Cold chain log: mini line chart suhu
  - Tombol "Hubungi Petani" (WhatsApp)
  - Tombol "Konfirmasi Diterima" (saat status Dikirim)

**Langganan**
* Active subscription cards:
  nama paket, petani, isi produk, harga/minggu, hari pengiriman, 
  tombol Jeda | Batal
* Tombol "+ Buat Langganan Baru"
* Subscription Builder (bottom sheet multi-step):
  - Step 1: Pilih petani
  - Step 2: Pilih produk + kuantitas
  - Step 3: Pilih hari pengiriman + review harga
  - Step 4: Konfirmasi

**Traceability Scanner**
* Kamera full screen dengan overlay frame scan
* Instruksi: "Arahkan kamera ke QR Code pada produk"
* Manual input code option
* Hasil scan → navigasi ke halaman traceability

**Halaman Traceability (`/lacak/[kode]`)**
* Header: nama produk + QR code display
* Farmer card: foto, nama, koordinat GPS, tombol "Lihat Kebun di Peta"
* Journey timeline vertikal:
  - 🌱 Tanam [tanggal]
  - 🌾 Panen [tanggal]
  - 📦 Dikemas [tanggal + waktu]
  - 🌡️ Cold Storage [suhu: 4°C]
  - 🚛 Diambil Kurir [tanggal]
  - 🏠 Diterima [tanggal]
* Detail pertanian: metode, pupuk, riwayat pestisida
* Cold chain temperature chart (fl_chart line chart)
* Tombol "Unduh Sertifikat" + "Bagikan"

**Notifikasi**
* List notifikasi dengan ikon warna per tipe:
  🟢 Pesanan dikonfirmasi
  🟡 Panen siap dijemput
  🔵 Pembayaran berhasil
  🔴 Stok hampir habis
  ⚪ Promo baru
* Swipe to dismiss
* "Tandai semua dibaca"

**Profil Konsumen**
* Avatar + nama + email + tipe pembeli badge
* Stats: Total Pesanan | Total Belanja | Petani Favorit
* Menu list: Edit Profil | Alamat Tersimpan | Metode Pembayaran | 
  Riwayat Langganan | Bantuan | Pengaturan | Keluar

---

## SHARED WIDGETS
```dart
// Status Badge
StatusBadge(status: OrderStatus.menunggu)

// KPI Card  
KpiCard(
  icon: Icons.payments_outlined,
  label: 'Pendapatan Hari Ini',
  value: 'Rp 450.000',
  trend: '+12% dari kemarin',
  trendPositive: true,
)

// Product Card
ProductCard(product: product, onTap: ...)

// Farmer Card  
FarmerCard(farmer: farmer, onTap: ...)

// Section Header
SectionHeader(title: 'Pesanan Terbaru', actionLabel: 'Lihat Semua', onAction: ...)

// Empty State
EmptyState(
  emoji: '📦',
  title: 'Belum ada pesanan',
  subtitle: 'Pesananmu akan muncul di sini',
  actionLabel: 'Mulai Belanja',
  onAction: ...,
)

// Loading Skeleton (shimmer)
ProductCardSkeleton()
FarmerCardSkeleton()
OrderCardSkeleton()

// Currency display helper
CurrencyText('8500', style: AppTextStyles.heading1, color: AppColors.primary)
// renders: "Rp 8.500"

// Traceability Timeline Item
TraceabilityStep(
  icon: '🌱',
  title: 'Ditanam',
  date: '1 Maret 2026',
  description: 'Kebun Pak Budi, Garut',
  isCompleted: true,
)
```

---

## MOCK DATA REQUIREMENTS

Buat file `lib/data/mock/` berisi:

**farmers_mock.dart** — 10 petani:
* Tersebar di Jawa Barat, Jawa Tengah, Sumatera Utara
* Lengkap: nama, foto, lokasi GPS, komoditas, rating, total penjualan, verifikasi

**products_mock.dart** — 30 produk:
* Kategori: Sayuran (10), Buah (8), Beras (4), Rempah (5), Ikan (3)
* Harga realistis dalam Rupiah
* Campuran: tersedia, pre-order, habis
* Beberapa berlabel organik

**orders_mock.dart** — 20 pesanan:
* Semua status terwakili
* Untuk farmer view dan consumer view

**traceability_mock.dart** — 5 record:
* Journey lengkap dengan timestamp
* Data suhu cold chain (list titik suhu per jam)
* Detail pupuk dan pestisida

**analytics_mock.dart**:
* Data forecast 4 minggu × 5 komoditas
* Data pendapatan 6 bulan (petani vs perantara)
* Data demand per provinsi

---

## UX REQUIREMENTS
* Semua teks UI dalam Bahasa Indonesia
* Format mata uang: "Rp 1.500.000" (titik sebagai pemisah ribuan)
* Format tanggal: "12 Maret 2026"
* Shimmer loading skeleton untuk semua list dan card
* Empty state dengan emoji + pesan untuk setiap list kosong
* Pull-to-refresh di semua screen list
* Haptic feedback pada tombol utama
* Smooth page transition (fade + slide)
* SnackBar untuk feedback aksi: berhasil, gagal, stok habis
* Bottom sheet untuk picker (provinsi, kategori, metode bayar)
* Semua form punya validasi inline dengan pesan error Bahasa Indonesia
* SafeArea di semua screen
* Keyboard dismiss on tap outside