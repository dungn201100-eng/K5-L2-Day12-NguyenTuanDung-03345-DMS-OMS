# Danh sách lớp v0 — Nguyễn Tuấn Dũng · G06

Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | eye_left / eye_right | open / closed / unknown | Phát hiện mắt nhắm kéo dài (buồn ngủ). `unknown` để model không bị dạy từ nhãn đoán khi mắt bị che | Có, trừ khi kính phản xạ LED hoặc kính râm tối che |
| 2 | gaze_zone | road, mirror_l/r/c, cluster, center, lap, other | Phát hiện mất tập trung (nhìn xuống đùi, nhìn màn hình quá lâu) và kiểm tra tài xế có quan sát gương | Có, dựa vào hướng đầu và mắt; kém tin cậy khi mắt bị che |
| 3 | face13 (13 điểm mặt + cờ occluded/outside) | tọa độ + cờ | Ước lượng tư thế đầu (yaw/pitch) và độ mở mắt, miệng. Cờ cho biết điểm nào không đáng tin | Có phần lớn; điểm mắt có thể mất do phản xạ trên kính |
| 4 | glasses | none / clear / sun / unknown | Chọn nhánh model phù hợp (mắt qua kính, kính râm), và biết khi nào không nên tin trạng thái mắt | Một phần: trên NIR kính râm có thể trông trong suốt, nên cần `unknown` |
| 5 | hand (whose, side, on_wheel) | driver/passenger, left/right, yes/no/unknown | Kiểm tra tay trên vô lăng (cảnh báo sẵn sàng tiếp quản), phát hiện thao tác với đồ vật | Có (hình dạng); `on_wheel` có thể `unknown` khi tay bị che |
| 6 | phone (state) | held / mounted / lap | Phát hiện dùng điện thoại khi lái | Có nếu thấy hình dạng; không vẽ khi chỉ thấy tay áp tai mà không thấy máy |
| 7 | seatbelt (trên person) | worn_correct / worn_incorrect / not_worn / unknown | Nhắc thắt dây, phát hiện thắt sai | Khó trên IR khi dây tối hoặc áo tối; dùng `unknown` |

## OMS (6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | person + seat | seat theo xe: rear_left/middle/right… | Đếm người, biết ghế nào có người để nhắc dây an toàn, điều khiển túi khí | Có (hình dạng, vị trí) |
| 2 | child_seat (occupied) | no / unknown (coach cho phép thêm yes) | Phát hiện ghế trẻ em để tắt túi khí ghế trước và nhắc kiểm tra; `unknown` khi không chắc bên trong ghế | Có (hình dạng); bên trong ghế có thể không thấy |
| 3 | infant_seat (facing) | rear / front | Phát hiện nôi xách và hướng đặt (quay lưng với chiều xe là nguy hiểm nếu túi khí bật) | Có (hình dạng) |
| 4 | object (type) | bag / box / cup / other | Phát hiện vật bỏ quên và vật có thể thành vật bay trong va chạm | Có, nhưng không phân biệt vật bằng màu |
| 5 | face (OMS: chỉ box) | box theo người | Đếm số người nhìn thấy mặt, xác nhận người ngồi thật | Có phần lớn; mắt và kính thường `unknown` |
| 6 | frame_meta: camera_blocked | yes / no | Biết camera bị che hay không để không tin kết quả model | Có (ảnh tối hoặc gần như đồng nhất) |
| 7 | frame_meta: light | day / night / unknown | Chọn chế độ xử lý RGB hay IR | Với ảnh dựng của SVIRO luôn là `unknown` |

## 2 câu hỏi leo thang

1. Câu hỏi: Khi trong ghế trẻ em có hình giống trẻ em đang ngồi, guideline v1.0 nói "không gán" và `occupied` chưa có `yes`; coach sau đó cho phép `yes`. Khi nào dùng `yes`, khi nào `unknown`, và có cần lớp riêng cho trẻ em không?
   Khung ví dụ: G06 S06_ir.
   Bạn tạm gán thế nào và vì sao: Mình nộp bản `occupied=unknown` (không chắc bên trong ghế), box `child_seat` ôm cả ghế, và hỏi coach tiêu chí dùng `yes`.
2. Câu hỏi: Phân biệt `infant_seat` (nôi xách) và `child_seat` (ghế lưng cao) bằng tiêu chí hình dạng nào khi ảnh không rõ quai xách?
   Khung ví dụ: G06 S02_rgb, S07_rgb và S08_rgb (mình và bạn ghép gán khác lớp ghế ở các khung này).
   Bạn tạm gán thế nào và vì sao: Ở S02 mình gán `child_seat` (`occupied=no`) cho ghế bên phải ảnh, bạn gán `infant_seat`. Ở S07 mình gán `infant_seat` cho ghế giữa, bạn gán `child_seat`. Chưa thống nhất, cần tiêu chí hình dạng.

