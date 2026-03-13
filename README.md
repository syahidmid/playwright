# Playwright Meta Updater

Browser automation untuk bulk update meta title & description di WordPress (Yoast SEO) dan Shopify via Playwright.

---

## Requirements

- macOS
- Python 3.x (sudah terinstall di Mac)
- Terminal (zsh)

---

## Setup Pertama Kali

Lakukan ini sekali saja saat pertama kali clone repo.

```bash
# 1. Masuk ke folder repo
cd ~/shopify-meta

# 2. Buat virtual environment
python3 -m venv venv

# 3. Aktifkan venv
source venv/bin/activate

# 4. Install dependencies
pip install playwright pandas

# 5. Install browser Chromium
python3 -m playwright install chromium
```

---

## Cara Menjalankan

Setiap kali mau menjalankan script, ikuti langkah ini:

```bash
# 1. Masuk ke folder repo
cd ~/shopify-meta

# 2. Aktifkan venv (wajib setiap sesi baru)
source venv/bin/activate

# 3. Jalankan script WordPress
python3 wp_yoast_meta_updater.py

# atau script Shopify
python3 shopify_meta_updater.py
```

> Tanda venv aktif: prompt terminal berubah jadi `(venv) ...`

---

## Struktur CSV

Siapkan file CSV dengan format berikut sebelum menjalankan script.

**WordPress (`meta_updates_wp.csv`):**
```
url,meta_title,meta_description
https://infojatengpos.com/wp-admin/post.php?post=123&action=edit,Judul Meta,Deskripsi meta di sini
```

**Shopify (`meta_updates.csv`):**
```
url,meta_title,meta_description
https://admin.shopify.com/store/sme-brother/pages/103652262087,Page Title,Deskripsi meta di sini
```

---

## Konfigurasi Credentials

Buka file script dengan text editor, lalu isi bagian config di atas:

```python
WP_USERNAME = "username_kamu"
WP_PASSWORD = "password_kamu"
```

> Jangan commit credentials ke Git. Tambahkan ke `.gitignore` atau gunakan file `.env`.

---

## Output

Setelah script selesai, akan muncul file log:
- `log_wp.csv` — hasil update WordPress
- `update_log.csv` — hasil update Shopify

Kolom log: `url`, `meta_title`, `meta_description`, `status`, `error`

Status: `success` / `failed` / `skipped`

---

## Troubleshooting

| Error | Solusi |
|-------|--------|
| `command not found: python` | Gunakan `python3` |
| `externally-managed-environment` | Pastikan venv aktif (`source venv/bin/activate`) |
| `command not found: playwright` | Jalankan via `python3 -m playwright ...` |
| Browser tidak terbuka | Pastikan `HEADLESS = False` di config script |
| Field tidak terdeteksi | Screenshot error, kirim untuk debug selector |