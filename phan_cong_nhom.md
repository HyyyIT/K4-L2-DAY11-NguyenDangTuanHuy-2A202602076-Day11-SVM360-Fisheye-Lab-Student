# 📋 Phân Công Công Việc Nhóm 3 Người — Lab 11 SVM360 Fisheye

> [!IMPORTANT]
> **Lưu ý quan trọng:** Mỗi người **BẮT BUỘC nộp repo cá nhân riêng** (Public). Trao đổi nhóm được phép nhưng không chia sẻ bài làm, gán nhãn, hoặc nộp chung một repo. Phân công dưới đây giúp nhóm phối hợp hiệu quả trong 240 phút.

---

## 👥 Phân Vai Theo 3 Giai Đoạn Chính

Lab xoay quanh **3 vai luân phiên** (Annotator → QA → Diagnostician). Nhóm 3 người phân công như sau:

| Người | Vai chính ban đầu | Slice gán nhãn |
|---|---|---|
| **Thành viên A** | Annotator | Slice của A (do `mode` lệnh giao) |
| **Thành viên B** | Annotator | Slice của B |
| **Thành viên C** | Annotator | Slice của C |

> Cả 3 người đều làm **đầy đủ tất cả các phần** (P0–P6), nhưng ở P3 (QA) sẽ **đổi bài** theo vòng: A review B, B review C, C review A.

---

## ⏱️ Chi Tiết Phân Công Theo Từng Giai Đoạn (240 phút)

### 🟦 P0 · Phút 0–40 — Khởi động (Cả 3 làm độc lập)

| Nhiệm vụ | Ai làm | Output |
|---|---|---|
| Clone repo cá nhân, bật CVAT | **Cả 3** | Repo riêng của mỗi người |
| Chạy `python3 lab11.py doctor` | **Cả 3** | `submission/00_setup/doctor.txt` |
| Chạy `python3 lab11.py mode --members an,binh,chi --self <tên-mình>` | **Cả 3** (mỗi người tự khai `--self`) | `submission/00_setup/mode.json` |
| Điền `sensor_context.md` | **Cả 3** | `submission/00_setup/sensor_context.md` |
| Tạo task parking trong CVAT, vẽ `parking_line` và `free_space` | **Cả 3** | `submission/parking/annotations.xml` |
| Điền `parking/observations.md` | **Cả 3** | File observations |
| Phác thảo `45_sampling_plan.csv` (8 ô, tổng 200 frame) | **Cả 3 thảo luận chung**, mỗi người ghi vào repo riêng | `submission/45_sampling_plan.csv` |

> 💡 **Mẹo nhóm:** Phần vẽ parking có thể thảo luận "vạch nào là parking_line" nhưng mỗi người tự vẽ và ghi observations riêng.

---

### 🟩 P1 · Phút 40–70 — Calibration C0 (Cả 3 làm độc lập)

| Nhiệm vụ | Ai làm | Output |
|---|---|---|
| Chạy `python3 lab11.py cvat C0`, tạo task, import prefill | **Cả 3** | Task C0 trên CVAT riêng |
| Gán nhãn / chỉnh sửa ảnh C0 theo rules | **Cả 3** (TỰ LÀM, chưa xem reference) | Nhãn trong CVAT |
| Export ZIP, chạy `lock calib`, `reference calib`, `compare calib` | **Cả 3** | `submission/p1_calib/` đầy đủ |
| Ghi 3 dòng đầu vào `findings.csv` | **Cả 3** | `submission/findings.csv` |

---

### 🟨 P2 · Phút 70–125 — Gán Nhãn Fisheye (Cả 3 làm độc lập)

| Nhiệm vụ | Ai làm | Output |
|---|---|---|
| Chạy `cvat <slice-riêng>`, tạo task, import prefill | **Cả 3** (slice khác nhau!) | Task fisheye riêng |
| Gán nhãn 3 ảnh trong slice | **Cả 3** | Nhãn CVAT |
| `draft`, `selfqc`, sửa rồi `lock r1_craft` | **Cả 3** | `submission/r1_craft/` |
| **Gửi mã khoá và file ZIP cho người review** | A → B, B → C, C → A | Chuẩn bị cho P3 |

---

### 🟥 P3 · Phút 140–165 — QA Mù (Đổi bài theo vòng)

| Người | Review bài của | Nhiệm vụ |
|---|---|---|
| **Thành viên A** | **Thành viên B** | Chạy `qa --slice <slice-B> --file <zip-B> --code <mã-B>`, điền `qa_review.md` |
| **Thành viên B** | **Thành viên C** | Chạy `qa --slice <slice-C> --file <zip-C> --code <mã-C>`, điền `qa_review.md` |
| **Thành viên C** | **Thành viên A** | Chạy `qa --slice <slice-A> --file <zip-A> --code <mã-A>`, điền `qa_review.md` |

> [!WARNING]
> **CHƯA được mở** teaching reference, model overlay hay worked HTML trong pha QA này. Review chỉ dựa vào ảnh gốc và rules.

---

### 🟪 P4 · Phút 165–200 — Chẩn Đoán (Cả 3 làm độc lập trên slice của mình)

| Nhiệm vụ | Ai làm | Output |
|---|---|---|
| `reference r1_craft`, `compare r1_craft` | **Cả 3** | `compare.md`, `compare.html` |
| `local-quality`, `model`, `iou-sweep` | **Cả 3** | `r3_diag/` |
| Điền `why`, `severity`, `action` vào `findings.csv`, chạy `triage` | **Cả 3** | `findings.csv` hoàn chỉnh |
| Điền nhận xét `zone_table.md` | **Cả 3** | `r3_diag/zone_table.md` |

---

### 🔶 P5 · Phút 200–215 — Rework (Cả 3 làm trên slice của mình)

| Nhiệm vụ | Ai làm | Output |
|---|---|---|
| Lọc `action=rework`, sửa trong CVAT | **Cả 3** | CVAT task đã sửa |
| `lock rework`, `rework`, đọc `delta.md` | **Cả 3** | `submission/rework/` |

---

### 🏁 P6 · Phút 215–240 — Hoàn Tất & Nộp (Cả 3 làm)

| Nhiệm vụ | Ai làm | Có thể thảo luận nhóm? |
|---|---|---|
| `python3 lab11.py card`, điền `10_error_card.md` | **Cả 3** | Có thể thảo luận pattern lỗi chung |
| Điền `20_guideline_patch.md`, `30_escalation_ticket.md` | **Cả 3** | Thảo luận được, nội dung riêng |
| Điền `40_decision_log.csv` | **Cả 3** | Riêng từng người |
| Hoàn tất `45_sampling_plan.csv` (tổng 200, 8 ô) | **Cả 3 + thảo luận số phân bổ** | Có thể thảo luận rationale |
| Điền `46_gold_set_plan.md` | **Cả 3** | Thảo luận được |
| Điền `50_exit_ticket.md` (3 câu tự nhìn lại) | **Cả 3** (riêng từng người) | Không |
| `python3 lab11.py check` → exit 0 | **Cả 3** | Giúp nhau sửa lỗi |
| Commit, push repo Public, gửi link | **Cả 3** | — |

---

## 🤝 Điều Có Thể Chia Sẻ vs. Phải Tự Làm

| ✅ Được phép chia sẻ / thảo luận | ❌ Phải tự làm riêng |
|---|---|
| Thảo luận rule, giải thích luật | Vẽ nhãn, gán box/polyline/polygon |
| Hỏi "vạch này là parking_line không?" | Ghi `observations.md` bằng lời của mình |
| Chia sẻ file ZIP đã khoá để người khác QA | Nộp chung một repo |
| Thảo luận số phân bổ 200 frame | Lý do phân bổ (rationale) riêng từng người |
| Thảo luận lỗi thấy trong P4 | Điền `findings.csv` và `why` riêng |
| Giúp nhau sửa lỗi `check` về cấu trúc file | Thay đổi nhãn hay quyết định của người khác |

---

## 📌 Tóm Tắt Nhanh — "Ai làm gì?"

```
Cả 3 người (độc lập):
  → P0: Setup, parking, phác plan 200 frame
  → P1: Calibration C0
  → P2: Gán nhãn slice riêng, lock
  → P4: Chẩn đoán (sau khi đổi reference)
  → P5: Rework
  → P6: Hoàn tất, check, push

Đổi chéo (P3 - QA mù):
  → A review B
  → B review C  
  → C review A
```

---

> [!TIP]
> **Gợi ý thứ tự ưu tiên nếu bị trễ:** Không bỏ `lock`, `reference`, `local-quality`, `parking`, kế hoạch 4 camera và `python3 lab11.py check`. Xem [docs/08-degrade-vi.md](file:///h:/VinAI_ThucChien/Lecture-Lab/Lab11/Day11-SVM360-Fisheye-Lab-Student/docs/08-degrade-vi.md) để biết cái gì có thể cắt giảm.
