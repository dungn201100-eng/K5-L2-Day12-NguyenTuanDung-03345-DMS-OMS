# Tự đánh giá — Nguyễn Tuấn Dũng · G06

## 1. Tự rà soát 4 cảnh

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip`, `flag`, `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S03_rgb | `child_seat` ghế giữa | guess | Bản đầu ghi `occupied=yes`. Guideline v1.0 mục 4.8 chỉ có `no`/`unknown`; sau đó coach cho phép thêm `yes`. Mình chọn nộp `unknown` vì không xác định chắc bên trong ghế | Đã sửa S03_rgb, S03_ir và S06_ir trong export_final_v2 |
| S01_rgb | box `face` của người lớn | missing | Mình vẽ `face` ở S01_ir nhưng thiếu ở S01_rgb, trong khi OMS cần box `face` cho mỗi người lớn (4.5) | Đã sửa (export_final_v2 có đủ 14 box `face`) |
| D03 | `eye_left`/`eye_right` và 8 điểm mắt `face13` | flag | Mắt ghi `unknown` nhưng điểm mắt không có cờ `occluded`/`outside` (4.6); bạn ghép đánh `occluded` | Không sửa: giữ nguyên, có giải thích ở check_final_v2.txt |
| D05 | `eye_right` và 4 điểm mắt phải | flag | Cùng kiểu với D03: mắt `unknown` mà điểm mắt chưa có cờ | Đã sửa (bật cờ cho điểm mắt phải) |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Thuộc tính và cờ không nhất quán với nhau. Cụ thể là ghi mắt `unknown` mà không đánh cờ cho các điểm mắt (D03, D05), và đặt `occupied=yes` ở ba ghế trẻ em (S03, S06) khi guideline v1.0 chưa có giá trị này. Ngoài ra mình bỏ sót một đối tượng ở một trong hai ảnh của cùng cảnh (box `face` ở S01_rgb).

Vì sao mình mắc: Mình xử lý từng thuộc tính riêng lẻ trên từng ảnh thay vì kiểm lại xem các trường của cùng một đối tượng có khớp nhau không (mắt `unknown` thì điểm mắt phải có cờ). Với `occupied`, project CVAT của mình cho chọn `yes` nên mình chọn khi thấy ghế có vẻ đang có người, mà chưa đối chiếu với mục 4.8. Với S01, mình gán `_rgb` và `_ir` ở hai thời điểm nên không rà đối chiếu hai ảnh.

Lần sau tránh bằng cách: Chạy `cabin_check` sớm sau mỗi vài ảnh (không chỉ ở checkpoint), đọc lại mục guideline của lớp trước khi chọn giá trị lạ, và sau khi gán xong một cảnh thì so lại cặp `_rgb`/`_ir` xem còn thiếu đối tượng nào không.

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai: S01_rgb, bạn vẽ box `face` của người lớn còn mình thiếu. Mình học được: sau khi gán xong thì rà lại từng người trong ảnh và tự hỏi "người này đã có đủ `person` và `face` chưa", không chỉ nhìn ghế.

Về D03, hai bạn vẫn khác nhau: bạn ghép đánh `occluded` cho các điểm mắt, còn mình giữ nguyên và ghi giải thích trong check_final_v2.txt.
