# TenderJalanJawa 🛣️
### Sistem Tender Infrastruktur Jalan Berbasis Blockchain Ethereum
**Kelompok 7 | Teknologi Blockchain | Institut Teknologi PLN**

---

## Struktur Folder

```
TenderJalanJawa/
│
├── smart-contract/
│   └── TenderJalanJawa.sol    ← Kode Solidity utama
│
├── frontend/
│   ├── login.html             ← Halaman login & autentikasi
│   ├── admin.html             ← Halaman Pokja Pemilihan (admin)
│   ├── vendor.html            ← Halaman Portal Vendor
│   ├── publik.html            ← Halaman Papan Transparansi Publik
│   ├── style.css              ← Stylesheet global aplikasi
│   ├── blockchain.js          ← Koneksi MetaMask & fungsi Ethers.js
│   ├── config.js              ← Contract address, ABI, akun demo
│   └── session.js             ← Manajemen state antar halaman (sessionStorage)
│
└── README.md
```

---

## Alur Navigasi Antar Halaman

```
login.html
    │
    ├── admin123 / admin123  ──────────────→ admin.html
    │                                            │
    ├── vendor01 / Vendor01@2026 ──→ vendor.html ←─┘ (admin bisa akses)
    │
    └── Masuk sebagai Publik ──→ publik.html (semua role bisa akses)
```

**State antar halaman** dikelola via `sessionStorage` melalui `js/session.js`.
Variabel seperti `role`, `status`, `kual`, `vendors`, dan `winner` otomatis
tersedia di setiap halaman tanpa perlu kirim ulang.

---

## Cara Menjalankan

### Prasyarat
- Browser Chrome/Firefox + ekstensi **MetaMask**
- MetaMask aktif di **Sepolia Testnet**
- ETH Sepolia gratis: [sepoliafaucet.com](https://sepoliafaucet.com)

### Langkah
1. Buka proyek menggunakan editor VS Code, masuk ke dalam folder frontend, lalu klik kanan pada berkas login.html $\rightarrow$ pilih Open with Live Server.


2. Login sesuai role:

| Role | Username | Password | Keterangan Akun |
| :--- | :---: | :---: | :--- |
| **Admin** | `admin123` | `admin123` | Panitia / Pokja Pemilihan |
| **Vendor** | `vendor01` | `Vendor01@2026` | Kontraktor Pengaju Tender (Vendor 01) |
| **Vendor** | `vendor02` | `Vendor02@2026` | Kontraktor Pengaju Tender (Vendor 02) |
| **Vendor** | `vendor03` | `Vendor03@2026` | Kontraktor Pengaju Tender (Vendor 03) |
| **Vendor** | `vendor04` | `Vendor04@2026` | Kontraktor Pengaju Tender (Vendor 04) |
| **Vendor** | `vendor05` | `Vendor05@2026` | Kontraktor Pengaju Tender (Vendor 05) |
| **Publik** | — | klik tombol | Masyarakat Umum (Read-Only) |





3. Hubungkan MetaMask di halaman yang memerlukan transaksi

---

## Update Contract Address

Setelah redeploy di Remix IDE, ubah di `js/config.js`:

```javascript
const contractAddress = "0x...ADDRESS_BARU...";
```

---

## Smart Contract

| | |
|---|---|
| **Network** | Ethereum Sepolia Testnet |
| **Address** | `0xE43FdE37B49f337FF64f052e45fC3866f5f3B97e` |
| **Etherscan** | https://sepolia.etherscan.io/address/0xE43... |
| **Solidity** | `^0.8.19` |

### Fungsi Utama Smart Contract

| Fungsi | Akses | Keterangan |
| :--- | :---: | :--- |
| `lockKualifikasi()` | Admin | Mengunci parameter acuan ambang batas kualifikasi tender di awal lelang. |
| `submitProposal()` | Vendor | Mengirimkan data penawaran harga dan berkas hash dokumen vendor ke blockchain. |
| `closeBidding()` | Admin | Menutup gerbang masa penawaran tender secara mutlak. |
| `announceWinner()` | Admin | Memicu kontrak untuk mengalkulasi skor relatif dan menetapkan pemenang otomatis. |
| `getProposals()` | Semua | Membaca seluruh list proposal yang masuk untuk kebutuhan transparansi publik. |

---

## Teknologi

| | |
|---|---|
| **Solidity ^0.8.19** | Smart Contract |
| **Ethers.js v6** | Koneksi frontend ↔ blockchain |
| **Web Crypto API** | Hash SHA-256 dokumen PDF |
| **MetaMask** | Wallet & ECDSA signing |
| **sessionStorage** | State sharing antar halaman |

---
*Institut Teknologi PLN · Fakultas Telematika Energi · 2025/2026*
