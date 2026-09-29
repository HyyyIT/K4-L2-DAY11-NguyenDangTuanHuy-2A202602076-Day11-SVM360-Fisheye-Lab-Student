# 📋 Hướng Dẫn QA — Dành cho KimNguyenKhoi

## Thông tin bài cần review

| Thông tin | Giá trị |
|---|---|
| **Người làm bài** | NguyenDangTuanHuy |
| **Slice** | `B4-edge` |
| **Mã khóa** | `5B46-395B` |
| **File ZIP** | `B4.zip` (nhận từ Huy qua chat/drive) |

---

## ⚠️ Quy tắc QA mù — BẮT BUỘC

- **CHƯA được mở** teaching reference, model overlay hay worked HTML
- Review **chỉ dựa vào ảnh gốc và rules** trong `docs/02-rules-vi.md`
- `why` để **trống** — QA chỉ ghi quan sát và rule, KHÔNG chẩn đoán nguyên nhân

---

## Các bước thực hiện

### Bước 1 — Chạy lệnh QA trong **repo của bạn (KimNguyenKhoi)**

Mở terminal trong thư mục repo của bạn, chạy:

```bat
py lab11.py qa --slice B4-edge --file <đường-dẫn-đến-B4.zip> --code 5B46-395B
```

> Ví dụ nếu file B4.zip ở Downloads:
> ```bat
> py lab11.py qa --slice B4-edge --file "C:\Users\<tên-bạn>\Downloads\B4.zip" --code 5B46-395B
> ```

Lệnh sẽ tạo ra:
- `submission/r2_qa/qa_overlay.html` → mở bằng trình duyệt để xem overlay
- `submission/r2_qa/qa_review.md` → điền nhận xét vào đây

---

### Bước 2 — Mở overlay xem ảnh

```bat
start submission\r2_qa\qa_overlay.html
```

---

### Bước 3 — Điền `qa_review.md`

Mở `submission/r2_qa/qa_review.md` và ghi nhận xét theo mẫu:

```
Frame: adasind_236370.jpg
Object: L3
Rule: R02
Nhận xét: Box vượt ra ngoài phần vật nhìn thấy, cạnh trái chạm vào vùng bị che
```

Mỗi nhận xét cần có:
- **Frame** cụ thể (tên file ảnh)
- **Object** (L1, L2, R1... theo overlay)
- **Rule ID** (R01, R02... theo docs/02-rules-vi.md)
- **Nhận xét** dựa trên ảnh, KHÔNG đoán nguyên nhân

---

### Bước 4 — Thêm vào findings.csv

Thêm các dòng QA vào `submission/findings.csv` với:
- `round` = `r2_qa`
- `cell` = `L_only` (hoặc theo overlay)
- `why` = **để trống**

---

### Bước 5 — Hoàn tất

Sau khi điền xong `qa_review.md` (hết TODO) → **báo lại cho Huy** biết đã QA xong để Huy làm P4.

---

## 3 ảnh trong slice B4-edge

```
adasind_236370.jpg
adasind_258420.jpg
adasind_310008.jpg
```

---

## Tài liệu tham khảo

- Rules: `docs/02-rules-vi.md`
- Checklist QA 9 mục: `docs/04-selfqc-checklist-vi.md`
- Taxonomy: `docs/05-taxonomy-vi.md`
