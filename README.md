# TTE-submit-

Aplikasi website untuk pengajuan tanda tangan elektronik yang terhubung dengan Excel. Sistem ini memungkinkan user membuat pengajuan, mengirimkan ke signer yang ditentukan, menandatangani pengajuan melalui web, dan mengekspor hasil ke file Excel untuk keperluan analisa atau rekap.

## Fitur utama

- Form pengajuan online
- Manajemen user dan peran:
  - admin
  - pengaju
  - signer
- Upload dokumen pendukung
- Tanda tangan digital berbasis web
- Opsi tanda tangan:
  - signature pad
  - cap/stamp
  - upload stamp perusahaan
- Workflow approval multi-step
- Notifikasi ke signer
- Rekap status pengajuan
- Export ke Excel (.xlsx)
- Log audit trail setiap perubahan
- Dashboard statistik

## Teknologi yang direkomendasikan

- Frontend: Next.js / React
- Backend: NestJS / FastAPI / Node.js
- Database: PostgreSQL
- ORM: Prisma
- Excel: xlsx / ExcelJS
- Signature: react-signature-canvas / canvas
- Styling: Tailwind CSS
- Authentication: JWT / Auth session
- Storage: local storage / S3 / Cloudinary

## Arsitektur aplikasi

Aplikasi terdiri dari:
1. Frontend web
2. Backend API
3. Database PostgreSQL
4. Storage file
5. Excel export/import module

### Alur kerja

1. User membuat pengajuan
2. Data disimpan ke database
3. Data di-mapping untuk Excel
4. Pengajuan dikirim ke signer
5. Signer menandatangani via form
6. Status approval diperbarui
7. Hasil disimpan dan diekspor ke Excel

## Struktur project

```bash
electronic-signature-app/
├─ apps/
│  ├─ web/
│  │  ├─ src/
│  │  ├─ public/
│  │  └─ package.json
│  └─ api/
│     ├─ src/
│     └─ package.json
├─ packages/
│  ├─ ui/
│  ├─ shared/
│  └─ eslint-config/
├─ prisma/
│  ├─ schema.prisma
│  └─ seed.ts
├─ docs/
├─ docker-compose.yml
├─ .env.example
├─ .gitignore
├─ package.json
├─ README.md
├─ tsconfig.base.json
└─ pnpm-workspace.yaml
```

## Alur bisnis

### 1. Pembuatan pengajuan
Pengaju membuka form pengajuan dan mengisi data berikut:
- Nama
- Divisi
- Tanggal
- Jenis pengajuan
- Keterangan
- Dokumen pendukung
- Signer yang dituju

### 2. Validasi data
Sistem melakukan validasi:
- field wajib diisi
- format file valid
- signer valid
- status default: pending

### 3. Pengiriman ke signer
Sistem menghasilkan notifikasi dan menandai status:
- waiting_signature

### 4. Penandatanganan
Signer membuka detail pengajuan dan memilih:
- signature pad
- cap/stamp
- upload stamp

### 5. Persetujuan
Signer dapat:
- approve
- reject
- request revision

### 6. Output dan Excel
Data hasil final siap:
- disimpan ke database
- ditampilkan di dashboard
- diekspor ke Excel

## Database utama

### Tabel utama
- users
- roles
- requests
- approvals
- signatures
- documents
- excel_exports
- audit_logs

### Contoh field request
- id
- user_id
- title
- category
- description
- status
- signer_id
- created_at
- updated_at

## Flow status
```text
draft
  -> submitted
      -> waiting_signature
          -> approved
          -> rejected
          -> revision_requested
```

## Instalasi

### Prasyarat
- Node.js 18+
- PostgreSQL 14+
- pnpm atau npm
- Git

### Langkah instalasi
1. Clone repository
```bash
git clone https://github.com/yourusername/electronic-signature-app.git
cd electronic-signature-app
```

2. Install dependency
```bash
pnpm install
```

3. Copy env example
```bash
cp .env.example .env
```

4. Setup database
```bash
pnpm prisma migrate dev
```

5. Jalankan aplikasi
```bash
pnpm dev
```

## Environment variables

```env
DATABASE_URL="postgresql://user:password@localhost:5432/e_signature_db"
JWT_SECRET="your-secret-key"
APP_URL="http://localhost:3000"
STORAGE_PATH="./storage"
EXCEL_EXPORT_PATH="./exports"
```

## Struktur folder backend

```bash
apps/api/src/
├─ config
├─ controllers
├─ services
├─ modules
├─ dto
├─ entities
├─ middleware
├─ utils
├─ app.module.ts
└─ main.ts
```

## Struktur folder frontend

```bash
apps/web/src/
├─ app
├─ components
├─ hooks
├─ lib
├─ store
├─ styles
├─ utils
└─ public
```

## Catatan penting

- Sistem ini bisa mendukung cap/stamp untuk kebutuhan internal dan operasional.
- Jika kebutuhan untuk legalitas formal, gunakan digital signature dengan sertifikat yang sesuai peraturan.
- Untuk audit trail, pastikan disimpan data:
  - siapa yang menandatangani
  - waktu
  - tipe tanda tangan
  - dokumen versi
  - log perubahan

## Roadmap
- [ ] Login dan role management
- [ ] Form pengajuan
- [ ] Dashboard admin
- [ ] Dashboard signer
- [ ] Signature pad
- [ ] Upload cap/stamp
- [ ] Export Excel
- [ ] Notification email
- [ ] Audit trail
- [ ] PDF final output

## Lisensi
MIT License

## Kontributor
- Tim Pengembangan
