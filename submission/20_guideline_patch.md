# Guideline patch

- **Rule mới đề xuất:** Bổ sung ví dụ minh họa kèm ngưỡng số (r/R cụ thể) vào R10 để annotator tự kiểm tra zone mà không cần tính tay; thêm sub-rule R03b phân biệt rõ ba trạng thái của người và xe hai bánh: (a) đang lái/ngồi → một box Bike bao cả, (b) đang dắt bộ → tách Pedestrian + Bike riêng, (c) đứng cạnh xe không tương tác → tách riêng với lý do ghi chú.
- **Áp dụng cho:** class `Bike`, `Pedestrian`; attribute `edge_zone`; zone `edge` (r/R ≥ 0.60)
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** R10 chỉ mô tả ngưỡng r/R dạng văn bản mà không có ví dụ overlay để annotator so sánh trực quan; R03 không phân biệt đủ rõ ba trạng thái của rider khiến hai QA reviewer (Tuan Khoi và bản thân) quan sát cùng frame nhưng cho kết quả khác nhau.
- **`rules_version` mới:** 1.1.0
- **Hiệu lực từ:** r1_craft của round tiếp theo sau khi patch được duyệt bởi Lab Coach
