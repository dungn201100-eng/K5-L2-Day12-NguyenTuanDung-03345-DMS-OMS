# TEAM — Ngày 12

Mã bộ ảnh: **G06** · Hình thức: nhóm

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Nguyễn Tuấn Dũng | 03345 | có | Nguyễn Tiến Thịnh (03354) | 17 |

Ca hai bạn vẫn không thống nhất, ghi lại để hỏi coach (ghi tên ảnh + đối tượng):

- G06 S02, S07, S08: ghế là `child_seat` hay `infant_seat`.
- G06 S01, S02, S05: giá trị `facing` của `infant_seat`.
- G06 D03: điểm mắt `face13` khi mắt `unknown` có cần cờ `occluded` hay không (mình không bật cờ, bạn bật `occluded`).
- G06 S06_ir: ghế trẻ em có hình giống trẻ em, dùng `occupied=yes` hay `unknown`.

## Cá nhân

### NguyenTuanDung-03345
- Phần mình làm (ngoài 22 ảnh của mình): review chéo với Nguyễn Tiến Thịnh trên task chính 22 ảnh; gán thêm S09–S10 (`export_extra.zip`).
- Điều mình học được hôm nay: ghế gọi theo xe, trái/phải theo người, và khi không thấy rõ thì ghi `unknown` kèm cờ cho điểm mắt thay vì đoán. Chạy `cabin_check` và đối chiếu với bạn giúp mình tìm ra lỗi mà tự nhìn không thấy (thiếu box `face` ở S01_rgb).
