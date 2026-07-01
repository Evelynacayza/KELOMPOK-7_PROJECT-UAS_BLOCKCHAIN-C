# TenderJalanJawa 🛣️
### Sistem Tender Infrastruktur Jalan Berbasis Blockchain Ethereum
**Kelompok 7 | Teknologi Blockchain | Institut Teknologi PLN**

---

## Struktur Folder

```
TenderJalanJawa/
│
├── login.html          ← Halaman login & autentikasi
├── admin.html          ← Halaman Pokja Pemilihan (admin)
├── vendor.html         ← Halaman Portal Vendor
├── publik.html         ← Halaman Papan Transparansi Publik
│
├── css/
│   └── style.css       ← Stylesheet global (dipakai semua halaman)
│
├── js/
│   ├── config.js       ← Contract address, ABI, akun demo
│   ├── session.js      ← Manajemen state antar halaman (sessionStorage)
│   └── blockchain.js   ← Koneksi MetaMask & fungsi Ethers.js
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
    ├── vendor01 / password01 ──→ vendor.html ←─┘ (admin bisa akses)
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
1. Buka project dengan **Live Server** di VS Code
   (klik kanan `login.html` → *Open with Live Server*)
   > ⚠️ Jangan buka dengan `file://` — MetaMask butuh `http://`

2. Login sesuai role:

| Role   | Username   | Password    |
|--------|------------|-------------|
| Admin  | `admin123` | `admin123`  |
| Vendor | `vendor01` | `password01`|
| Publik | —          | klik tombol |

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

### Fungsi

| Fungsi | Akses | Keterangan |
|--------|-------|------------|
| `submitProposal()` | Vendor | Submit penawaran ke blockchain |
| `closeBidding()` | Admin | Tutup gerbang lelang |
| `announceWinner()` | Admin | Kontrak otomatis pilih skor tertinggi |
| `getProposals()` | Semua | Baca semua penawaran |
| `isBiddingOpen` | Semua | Status lelang |
| `hasWinner` | Semua | Ada/tidaknya pemenang |

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
