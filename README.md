# Notebook Đại số tuyến tính

Dự án lưu trữ các ghi chép bài giảng môn **Đại số tuyến tính** (Mã lớp: MA003.F32.LT.CNTT). Các bài giảng được biên soạn bằng hệ thống tạo tài liệu **LaTeX** với cấu hình hỗ trợ hiển thị hoàn chỉnh tiếng Việt.

## 📁 Cấu trúc thư mục

Các bài giảng được chia theo từng buổi học. Mỗi buổi là một thư mục riêng biệt chứa file `.tex` độc lập (tự build riêng) để dễ dàng quản lý và biên dịch.

```text
NoiDungHoc/
└── BaiGiang.tex/
    ├── buoi1/Buoi_01.tex
    ├── buoi2/buoi2.tex
    ├── buoi3/buoi3.tex
    └── ...
```

## ⚙️ Yêu cầu hệ thống

Để biên dịch (build) các file LaTeX chứa tiếng Việt trong dự án này, bạn cần cài đặt các gói TeX cơ bản cùng với gói hỗ trợ ngôn ngữ.

### Cài đặt trên Ubuntu/Debian

Chạy lệnh sau để cài đặt các gói cần thiết:

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

> **⚠️ Quan trọng:** Gói `texlive-lang-other` là **bắt buộc**. Gói này cung cấp:
> - **T5 encoding** (`t5enc.def`) — bảng mã font dành riêng cho tiếng Việt.
> - **VNTeX fonts** — font hỗ trợ đầy đủ các tổ hợp dấu tiếng Việt (ữ, ố, ộ, ẩ, ề, ở...).
> 
> Nếu thiếu gói này, tiến trình biên dịch sẽ báo lỗi `Encoding scheme 'T5' unknown` hoặc `Unicode character ... not set up for use with LaTeX`.

## 🚀 Hướng dẫn biên dịch (Build)

Dự án này yêu cầu sử dụng lệnh `pdflatex` (không sử dụng `xelatex` hay `lualatex`).

Để build một bài giảng cụ thể, bạn mở terminal, di chuyển tới thư mục của buổi học đó và chạy lệnh `pdflatex`:

```bash
# Ví dụ build bài giảng buổi 1
cd NoiDungHoc/BaiGiang.tex/buoi1
pdflatex Buoi_01.tex
```

Sau khi tiến trình chạy thành công, một file định dạng PDF (ví dụ: `Buoi_01.pdf`) sẽ được sinh ra trong cùng thư mục.

## 📝 Quy ước viết mã LaTeX

Khi tạo một file tài liệu bài giảng (`.tex`) mới, bạn **bắt buộc** phải sử dụng đoạn *preamble* chuẩn dưới đây để đảm bảo bộ gõ tiếng Việt hoạt động trơn tru:

```latex
\documentclass[12pt,a4paper]{article}
\usepackage[utf8]{inputenc}
\usepackage[T5]{fontenc}          % BẮT BUỘC: T5 = Vietnamese encoding (KHÔNG dùng T1)
\usepackage[vietnamese]{babel}
\usepackage{amsmath, amssymb, amsfonts}
```

**Lưu ý khi cấu hình:**
- Luôn sử dụng encoding **UTF-8** khi lưu file.
- Tuyệt đối không dùng `\usepackage[T1]{fontenc}` vì bảng mã T1 (Western European) không có đủ các ký tự tiếng Việt có dấu kép, gây ra lỗi hiển thị.
