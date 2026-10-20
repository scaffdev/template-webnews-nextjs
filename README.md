# NusantaraKini — Template Website Berita (Next.js)

Template portal berita harian berbahasa Indonesia yang siap pakai: headline hero,
breaking-news ticker, pencarian, halaman kategori, detail artikel, berita terkait,
tombol bagikan, dan tampilan responsif. Berjalan **tanpa backend** — seluruh berita
memakai data mock di `src/lib/data/`, mudah diganti dengan API nyata.

## Tech Stack

| Kebutuhan | Teknologi |
|---|---|
| Framework | Next.js 16 (App Router) + React 19 |
| Bahasa | TypeScript 5 |
| Styling | Tailwind CSS v4 |
| Ikon | lucide-react |
| Font | Google Fonts (Inter + Playfair Display) via `next/font` |
| Data | Mock statis (`src/lib/data/`) |

> Catatan: situs dikunci **light mode** (toggle dark dinonaktifkan) agar tampilan
> identik di semua perangkat. Cara mengaktifkan ulang ada di bagian bawah.

## Menjalankan

```bash
npm install
cp .env.example .env.local   # opsional, template berjalan tanpa env
npm run dev                  # http://localhost:3000

npm run build                # build produksi (wajib lolos sebelum publish)
npm run lint                 # ESLint
npm run format               # Prettier
```

Syarat: Node.js 20+ (disarankan 22+ agar kompatibel bila menambah integrasi Supabase).

## Struktur Folder

```
src/
├── app/
│   ├── layout.tsx            # Root layout: Navbar, ticker, Footer, metadata
│   ├── page.tsx              # Beranda (Hero + grid + per-kategori)
│   ├── berita/[slug]/        # Detail artikel
│   ├── kategori/[slug]/      # Daftar berita per kategori
│   ├── cari/                 # Pencarian
│   └── tentang/              # Profil redaksi
├── components/
│   ├── layout/               # Navbar, Footer, BreakingNewsTicker
│   ├── sections/             # HeroSection, CategorySection, Sidebar
│   ├── theme/                # ThemeProvider
│   └── ui/                   # NewsCard, CategoryBadge, ShareButtons, ThemeToggle
└── lib/
    ├── data/                 # berita.ts (mock artikel), kategori.ts
    ├── types.ts              # Tipe terpusat (Berita, Kategori, dll)
    └── utils.ts              # cn(), format tanggal/waktu
```

## Kustomisasi cepat

| Yang diganti | File |
|---|---|
| Nama & tagline media | `src/components/layout/Navbar.tsx`, `Footer.tsx` |
| Judul tab & SEO | `src/app/layout.tsx` (`metadata`) |
| Warna utama (merah) | `src/app/globals.css` + class `bg-red-*`/`text-red-*`, `src/components/ui/CategoryBadge.tsx` |
| Tambah/edit/hapus berita | `src/lib/data/berita.ts` → array `beritaList` (lihat komentar tipe) |
| Tambah/edit kategori | `src/lib/data/kategori.ts` → array `kategoriList` |
| Gambar | taruh di `public/images/` atau isi URL di field `gambar` (ada fallback otomatis) |
| Ticker berjalan | `src/components/layout/BreakingNewsTicker.tsx` (kecepatan via `.animate-marquee` di `globals.css`) |

Menambah kategori cukup lewat `kategoriList`; halaman `/kategori/[slug]` dan menu
navbar dibuat otomatis (`generateStaticParams`).

## Mengaktifkan dark mode kembali

1. Hapus baris `@custom-variant dark ...` di `src/app/globals.css`, kembalikan blok `.dark` + `color-scheme`.
2. Kembalikan `ThemeProvider` versi toggle dan `ThemeToggle` tombol asli, pasang di `Navbar`.
3. Kembalikan class `dark:` pada komponen, lalu uji di OS terang & gelap.

## Checklist sebelum publish

- [ ] `npm run build` sukses tanpa error
- [ ] Cek 360px / 768px / 1280px: hero tidak kepotong, grid 1→2→3 kolom, sidebar tidak overlap
- [ ] Semua badge kategori terbaca, ticker berjalan tanpa scroll horizontal
- [ ] Tiap slug berita dibuka (tidak 404), gambar tidak broken

## Lisensi

MIT.
