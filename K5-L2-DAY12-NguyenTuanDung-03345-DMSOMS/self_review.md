# Tự đánh giá — Nguyễn Tuấn Dũng · G06

## 1. Tự rà soát 4 cảnh

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip`, `flag`, `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S03_rgb | `child_seat` ghế giữa | guess | `occupied=yes`, guideline 4.8 không có `yes` (chỉ `no`/`unknown`) | Đã sửa S03_rgb, S03_ir và S06_ir trong export_final_v2 |
| S01_rgb | box `face` của người lớn | missing | Mình vẽ face ở S01_ir nhưng thiếu ở S01_rgb (4.5) | Đã sửa (bản mới có 14 face) |
| D03 | `eye_left`/`eye_right` và 8 điểm mắt `face13` | flag | Mắt `unknown` nhưng điểm mắt không có cờ `occluded`/`outside` (4.6) | Không sửa: giữ nguyên `unknown` và cờ như cũ, có giải thích trong check_final_v2.txt |
| D05 | `eye_right` và 4 điểm mắt phải | flag | Như D03 | Đã sửa (cờ điểm mắt phải) |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Thuộc tính và cờ không nhất quán với nhau (đặt `occupied=yes` không hợp lệ; ghi mắt `unknown` mà không đánh cờ điểm mắt), và bỏ sót một đối tượng ở một trong hai ảnh của cùng cảnh (S01_rgb).

Vì sao mình mắc: [ĐIỀN LÝ DO CỦA RIÊNG BẠN]

Lần sau tránh bằng cách: Chạy `cabin_check` sớm sau mỗi vài ảnh (không chỉ ở checkpoint), và sau khi gán xong một cảnh thì so lại cặp `_rgb`/`_ir` xem còn thiếu đối tượng nào không.

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai: S01_rgb, bạn vẽ box `face` của người lớn còn mình thiếu. Mình học được: sau khi gán xong thì rà lại từng người trong ảnh, không chỉ nhìn ghế. [XÁC NHẬN BẰNG ẢNH]
