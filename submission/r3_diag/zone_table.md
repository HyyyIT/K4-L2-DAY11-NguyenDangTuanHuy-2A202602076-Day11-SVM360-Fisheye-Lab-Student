# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 4 | 0 | 0 | 2 | 2 | — |
| mid | 9 | 4 | 2 | 3 | 8 | MISSING (4) |
| edge | 7 | 1 | 0 | 1 | 1 | MISSING (1) |

## Nhận xét

- Zone nào người (L) và model (M) gãy nhiều nhất, dẫn số ở bảng trên: Zone **mid** gãy nhiều nhất ở cả người (L missing=4, L spurious=2) lẫn model (M thừa=8, M missing=3). Zone center không có lỗi L; zone edge chỉ có 1 missing ở L và 1 ở M. Riêng frame `adasind_258420.jpg` chiếm phần lớn lỗi (precision=0.600, recall=0.375) do annotator bỏ sót nhiều box trong cảnh đông đúc.
- Giả thuyết vì sao (méo fisheye, box lỏng, thiếu `ego_body`, ...) và giới hạn của slice ba frame: Vùng mid của camera fisheye 360° bị méo không gian đáng kể — vật bị kéo dài hoặc bẹt theo chiều ngang khiến annotator khó xác định ranh giới box chính xác. Frame `adasind_258420.jpg` có mật độ vật cao (xe máy, người đi bộ đan xen), kết hợp với méo fisheye làm nhiều vật bị che khuất lẫn nhau, dẫn đến bỏ sót hệ thống. Model YOLOv26m cũng bị ảnh hưởng tương tự nhưng có xu hướng ngược lại — phát hiện thêm nhiều box thừa (M_only=8 trong zone mid) do ảo giác quang học từ biến dạng ảnh. Giới hạn: chỉ có 3 frame nên không thể rút ra kết luận thống kê về tỷ lệ lỗi tổng thể; cần ít nhất 30–50 frame để đánh giá pattern đáng tin cậy.
