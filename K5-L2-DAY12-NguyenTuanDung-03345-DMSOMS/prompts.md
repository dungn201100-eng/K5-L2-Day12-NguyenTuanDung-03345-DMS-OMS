# Khai báo dùng AI — Nguyễn Tuấn Dũng

Không đưa ảnh cabin hay ảnh tài xế (kể cả ảnh chụp màn hình) cho bất kỳ công cụ AI nào. Chỉ đưa file export `.zip` (tọa độ và thuộc tính) và các file markdown của repo.

| # | Công cụ | Bạn hỏi gì (tóm tắt) | Bạn dùng kết quả thế nào | Bạn có kiểm lại không? Bằng gì? |
|---|---|---|---|---|
| 1 | Claude Code | Check  đang ở bước nào | Dùng để xác định các bước còn thiếu | Có, đối chiếu với SUBMISSION.md |
| 2 | Claude Code | Chạy `cabin_check` trên export của mình và của bạn ghép cặp | Dùng kết quả để biết lỗi cần sửa trên CVAT (child_seat, cờ điểm mắt, box face thiếu) | Có, chạy lại bằng script trong repo và `diff` giữa các bản export |
