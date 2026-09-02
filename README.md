# S-Partners Advisory Company (SP Advisory) — Web Project Guide

Tài liệu hướng dẫn toàn diện dành cho lập trình viên và thành viên mới tham gia phát triển website **SP Advisory**.

---

## 1. Tổng Quan Dự Án & Hạ Tầng

* **Thương hiệu:** S-Partners Advisory Company (SP Advisory) — Boutique Financial Advisory Firm.
* **Tên miền hoạt động:**
  * Chính thức: [`https://spadvisory.com.vn`](https://spadvisory.com.vn) & [`https://www.spadvisory.com.vn`](https://www.spadvisory.com.vn)
  * Tên miền phụ / Testing: [`https://spadvisory.io.vn`](https://spadvisory.io.vn)
* **GitHub Repository:** [`NST1511/spadvisory-web`](https://github.com/NST1511/spadvisory-web.git)
* **Hạ tầng Hosting & CI/CD:** **Cloudflare Pages** (Tự động build và deploy ngay khi push code lên nhánh `main`).
* **Quản lý DNS:** Cloudflare Nameservers (`clay.ns.cloudflare.com`, `heidi.ns.cloudflare.com`).

---

## 2. Công Nghệ Sử Dụng (Tech Stack)

* **Framework:** [Astro v5](https://astro.build/) (Static Site Generation - SSG).
* **CSS Framework:** [Tailwind CSS v4](https://tailwindcss.com/) (Tích hợp qua `@tailwindcss/vite`).
* **Typography:**
  * **Tiêu đề (Headings):** `Noto Serif` (Google Fonts).
  * **Nội dung (Body):** `Inter` (Google Fonts).
* **Quản lý nội dung:** Astro Content Collections (Bản tin Markdown `.md`).
* **Môi trường Node.js:** Node.js version **22** (được chỉ định trong `.nvmrc`).

---

## 3. Bảng Màu Thương Hiệu Chuẩn (Design Tokens)

Website áp dụng bảng màu *Mayfair Executive* sang trọng:

| Tên màu | Mã HEX | Vị trí sử dụng |
|---|---|---|
| **Midnight Navy** | `#0A1628` | Nền chính Footer, Header solid, Hero phải, màu chữ tiêu đề |
| **Signature Gold** | `#C5A55A` | Điểm nhấn thương hiệu, viền nút CTA, icon, màu hover |
| **Gold Muted** | `#8B7A3E` | Màu chữ slogan phụ, trạng thái active đậm |
| **Off-White Light** | `#FAFAFA` | Nền trang nội dung, nền khối Hero bên trái |
| **Border Slate** | `#0A1628`/10 | Đường kẻ phân cách, viền card dịch vụ |

---

## 4. Cấu Trúc Thư Mục Dự Án (Project Structure)

```text
spadvisory-web/
├── .nvmrc                          # Khai báo Node.js version (22)
├── package.json                    # Dependencies & scripts
├── astro.config.mjs                # Cấu hình Astro & Tailwind Vite plugin
├── src/
│   ├── styles/
│   │   └── global.css              # Font face, Tailwind layer, custom animations
│   ├── layouts/
│   │   └── BaseLayout.astro        # Layout khung chung (SEO meta, OG, Header, Footer, Gate)
│   ├── components/
│   │   ├── Header.astro            # Header thanh điều hướng + Nút Globe Dropdown chọn ngôn ngữ
│   │   ├── Footer.astro            # Chân trang (Dịch vụ, Liên hệ, Bản quyền đa ngôn ngữ)
│   │   ├── Hero.astro              # Khối Hero 2 mảng màu (White / Navy)
│   │   ├── ServiceCard.astro       # Thẻ hiển thị tóm tắt dịch vụ
│   │   ├── NewsletterCard.astro    # Thẻ hiển thị bài viết Bản tin / Insight
│   │   └── PasswordGate.astro      # Màn hình khóa mật khẩu bảo vệ duyệt web nội bộ (Song ngữ)
│   ├── content/
│   │   ├── config.ts               # Định nghĩa Schema cho Content Collections (Newsletters)
│   │   └── newsletters/            # Thư mục chứa các bài viết Markdown (.md)
│   └── pages/
│       ├── index.astro             # [EN] Trang chủ mặc định (Tiếng Anh)
│       ├── services.astro          # [EN] Trang dịch vụ (5 phân nhóm)
│       ├── about-us.astro          # [EN] Trang Về chúng tôi (Câu chuyện & Ban lãnh đạo)
│       ├── contact.astro           # [EN] Trang Liên hệ
│       ├── news/
│       │   ├── index.astro         # [EN] Danh sách bài viết tin tức & nhận định
│       │   └── [...slug].astro     # [EN] Chi tiết bài viết tin tức
│       ├── vi/                     # [VI] Toàn bộ phiên bản Tiếng Việt
│       │   ├── index.astro         # Trang chủ Tiếng Việt
│       │   ├── dich-vu.astro       # Dịch vụ Tiếng Việt
│       │   ├── ve-chung-toi.astro  # Về chúng tôi Tiếng Việt
│       │   ├── lien-he.astro       # Liên hệ Tiếng Việt
│       │   └── ban-tin/
│       │       ├── index.astro     # Danh sách bản tin Tiếng Việt
│       │       └── [...slug].astro # Chi tiết bản tin Tiếng Việt
│       └── 404.astro               # Trang lỗi 404
```

---

## 5. Hướng Dẫn Cài Đặt & Chạy Môi Trường Local

### Yêu cầu tiên quyết:
* Cài đặt **Node.js >= 20** (khuyên dùng Node 22).

### Các lệnh thực thi:

```bash
# 1. Clone mã nguồn về máy
git clone https://github.com/NST1511/spadvisory-web.git
cd spadvisory-web

# 2. Cài đặt các gói thư viện
npm install

# 3. Khởi chạy môi trường lập trình (Local Dev Server)
npm run dev
# Mở trình duyệt tại: http://localhost:4321

# 4. Kiểm tra build tĩnh trước khi push code
npm run build

# 5. Xem trước bản build tĩnh hoàn chỉnh
npm run preview
```

---

## 6. Hướng Dẫn Quản Lý Nội Dung Thường Gặp

### A. Cách đăng bài viết Bản tin / Nhận định mới
Tất cả các bài viết được lưu dưới dạng file Markdown tại: `src/content/newsletters/`.
Để đăng bài mới, tạo một file mới (ví dụ: `src/content/newsletters/tuan-2026-09-01.md`) với cấu trúc:

```markdown
---
title: "Bản tin Thị trường & Kinh tế Tuần 01/09/2026"
description: "Phân tích biến động tỷ giá, lãi suất và diễn biến thị trường M&A quý 3."
date: 2026-09-01
type: "weekly" # hoặc "deep-dive" cho bài phân tích sâu
draft: false
---

## 1. Tiêu điểm kinh tế vĩ mô
Nội dung bài viết viết bằng định dạng Markdown thông thường...

## 2. Nhận định chiến lược
...
```
*Bài viết sẽ tự động xuất hiện trên cả trang `/news` (EN) và `/vi/ban-tin` (VI).*

---

### B. Cơ chế Khóa Mật khẩu (Private Preview) & Cách Mở Public
* Hiện tại toàn bộ website đang được bảo vệ bởi component `src/components/PasswordGate.astro`.
* **Mật khẩu truy cập nội bộ:** `SPAdvisory2026` hoặc `SP@2026`.
* **Khi chốt nội dung và muốn mở PUBLIC cho toàn thế giới:**
  1. Mở file `src/layouts/BaseLayout.astro`.
  2. Xóa hoặc comment lại dòng:
     ```astro
     <!-- <PasswordGate lang={lang} /> -->
     ```
  3. Commit và push code lên GitHub ➔ Toàn bộ website sẽ lập tức mở tự do mà không hỏi mật khẩu.

---

### C. Cơ chế Đa Ngôn Ngữ (i18n) & Điều Hướng
* Website sử dụng **Tiếng Anh làm mặc định** (Root: `/`, `/services`, `/about-us`, `/news`, `/contact`).
* Tiếng Việt sử dụng tiền tố **`/vi/`** (`/vi`, `/vi/dich-vu`, `/vi/ve-chung-toi`, `/vi/ban-tin`, `/vi/lien-he`).
* Cụm nút **Globe Dropdown** trên `src/components/Header.astro` tự động tính toán URL đối ứng khi chuyển ngữ để người dùng không bị văng về trang chủ.

---

## 7. Quy Trình Triển Khai (Deployment Workflow)

1. Mọi commit được đẩy lên nhánh **`main`** của GitHub (`git push origin main`).
2. Cloudflare Pages sẽ tự động kích hoạt Worker Build (`astro build`) và deploy ra mạng lưới toàn cầu.
3. Thời gian deploy trung bình: **~30 đến 45 giây**.
4. Trạng thái build có thể xem trực tiếp tại [Cloudflare Dashboard - Pages Projects](https://dash.cloudflare.com/).

---

## 8. Danh Sách Liên Hệ Quản Trị

* **Email quản trị chung:** `admin@spadvisory.com.vn`
* **Hotline hỗ trợ:** `(+84) 964 008 304`
* **Văn phòng:** BT2D-19, Khu đô thị Mỗ Lao, Quận Hà Đông, Hà Nội, Việt Nam.
