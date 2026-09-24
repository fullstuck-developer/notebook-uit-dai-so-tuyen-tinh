# Agent Setup Guide — Notebook Đại số tuyến tính

## Tổng quan dự án

Dự án ghi chép bài giảng môn **Đại số tuyến tính** (MA003.F32.LT.CNTT) dưới dạng LaTeX, viết bằng **tiếng Việt**.

## Cấu trúc thư mục

```
NoiDungHoc/
└── BaiGiang.tex/
    ├── buoi1/Buoi_01.tex
    ├── buoi2/buoi2.tex
    ├── buoi3/buoi3.tex
    ├── buoi4/buoi4.tex
    ├── buoi5/Buoi_05.tex
    ├── buoi6/Buoi_06.tex
    └── buoi8/Buoi_08.tex
NoiDungThi/
├── CauTrucDe/CauTrucDe.tex
└── Phao/Phao.tex
```

Mỗi buổi là một file `.tex` độc lập, tự build riêng.

## Yêu cầu hệ thống

### Gói TeX cần cài đặt

```bash
sudo apt-get update
sudo apt-get install -y \
  texlive-base \
  texlive-latex-base \
  texlive-latex-recommended \
  texlive-latex-extra \
  texlive-fonts-recommended \
  texlive-lang-other
```

> **Quan trọng**: Gói `texlive-lang-other` là **bắt buộc**. Gói này cung cấp:
> - **T5 encoding** (`t5enc.def`) — bảng mã font dành riêng cho tiếng Việt
> - **VNTeX fonts** — font hỗ trợ đầy đủ các tổ hợp dấu tiếng Việt (ữ, ố, ộ, ẩ, ề, ở...)
>
> Nếu thiếu gói này, pdflatex sẽ báo lỗi `Encoding scheme 'T5' unknown` và `Unicode character ... not set up for use with LaTeX`.

### Kiểm tra cài đặt

```bash
# Kiểm tra pdflatex
pdflatex --version

# Kiểm tra T5 encoding đã có
kpsewhich t5enc.def
# Kết quả mong đợi: /usr/share/texlive/texmf-dist/tex/latex/vntex/t5enc.def
```

## Quy ước LaTeX cho tiếng Việt

### Preamble chuẩn

Tất cả file `.tex` trong dự án này **phải** dùng preamble sau:

```latex
\documentclass[12pt,a4paper]{article}
\usepackage[utf8]{inputenc}
\usepackage[T5]{fontenc}          % T5 = Vietnamese encoding (KHÔNG dùng T1)
\usepackage[vietnamese]{babel}
\usepackage{amsmath, amssymb, amsfonts}
```

### Lưu ý quan trọng

- **PHẢI dùng `T5`**, không dùng `T1`. Encoding T1 (Western European) không có đủ ký tự tiếng Việt có dấu kép.
- **PHẢI dùng `pdflatex`** để build (không dùng xelatex hay lualatex).
- File phải được lưu với encoding **UTF-8**.
- Khi tạo file `.tex` mới, luôn copy preamble chuẩn ở trên.

## Build

```bash
# Build một buổi cụ thể
cd NoiDungHoc/BaiGiang.tex/buoi1
pdflatex -interaction=nonstopmode Buoi_01.tex

# Kiểm tra build thành công (không có lỗi Unicode hoặc T5)
pdflatex -interaction=nonstopmode Buoi_01.tex 2>&1 | grep -E "Error|Missing"
# Kết quả mong đợi: không có output
```

## Sửa lỗi thường gặp

| Lỗi | Nguyên nhân | Cách sửa |
|-----|-------------|----------|
| `Encoding scheme 'T5' unknown` | Chưa cài `texlive-lang-other` | `sudo apt-get install -y texlive-lang-other` |
| `Unicode character ữ (U+1EEF) not set up` | Đang dùng `T1` thay vì `T5` | Đổi `\usepackage[T1]{fontenc}` thành `\usepackage[T5]{fontenc}` |
| Font bị lỗi dấu tiếng Việt | Thiếu vntex fonts | `sudo apt-get install -y texlive-lang-other` |

