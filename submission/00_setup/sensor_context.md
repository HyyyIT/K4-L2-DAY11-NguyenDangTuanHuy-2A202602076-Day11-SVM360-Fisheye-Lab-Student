# Sensor context

- Rig: Camera fisheye được gắn hướng ra phía trước xe (forward-facing). Nhìn từ quan sát ảnh ADASIND, camera đặt cao — có thể trên mui xe hoặc phía trên kính chắn gió. Xe ego di chuyển trên đường một/hai chiều khu vực ngoại ô, nông thôn (Ấn Độ). Không có tài liệu rig chính thức kèm theo dataset ADASIND; mô tả này dựa hoàn toàn vào quan sát ảnh.

- `ego_body`: Phần thân xe ego nhìn thấy ở **phía dưới cùng** bên trong vòng kính — có thể thấy bóng/hình của đầu xe (dạng hình chữ T hoặc hình thang tối) ở đáy frame, chiếm khoảng 10–15% chiều cao vùng hình tròn. Một số frame (ví dụ `adasind_006840.jpg`, `adasind_271039.jpg`) không có ego body nhìn thấy rõ và không vẽ polygon ego_body cho những frame đó.

- Vòng kính (lens circle): Nằm **chính giữa** khung ảnh hình chữ nhật. Đường kính vòng tròn fisheye chiếm khoảng **85–90%** chiều rộng khung hình. Vùng ngoài vòng kính ở bốn góc là màu đen hoàn toàn — không chứa thông tin ảnh thực tế và được đánh dấu là `lens_border` (ignore_region với reason=lens_border). Rìa trong của vòng kính có hiện tượng méo (distortion) rõ ràng do đặc tính ống kính góc rộng.