# Khai báo dùng AI — Nguyễn Tuấn Dũng

Không đưa ảnh cabin hay ảnh tài xế (kể cả ảnh chụp màn hình) cho bất kỳ công cụ AI nào. Chỉ đưa file export `.zip` (tọa độ và thuộc tính) và các file markdown của repo.

| # | Công cụ | Bạn hỏi gì (tóm tắt) | Bạn dùng kết quả thế nào | Bạn có kiểm lại không? Bằng gì? |
|---|---|---|---|---|
| 1 | Claude Code | So sánh với repo mẫu để biết đang ở bước nào | Dùng để xác định các bước còn thiếu | Có, đối chiếu với SUBMISSION.md |
| 2 | Claude Code | Chạy `cabin_check` trên export của mình và của bạn ghép cặp | Dùng kết quả để biết lỗi cần sửa trên CVAT (child_seat, cờ điểm mắt, box face thiếu) | Có, chạy lại bằng script trong repo và `diff` giữa các bản export |
| 3 | Claude Code | Điền các dòng `disagreement_log.csv` mà guideline quyết định được | Dùng làm bản nháp, mình đối chiếu theo từng mục guideline | Có, đọc lại GUIDE.md 4.2, 4.5, 4.6, 4.8 |
| 4 | Claude Code | Viết bản nháp `class_list_v0.md`, `ir_log.csv`, `self_review.md`, `TEAM.md` | Dùng làm khung và chỉnh theo bản export thật của mình | Có, đối chiếu từng dòng với dữ liệu trong export_final_v2.zip |
| 5 | Claude Code | Điền đáp án `exit_ticket.md` | Chép đáp án vào file | Câu 2 tự tính lại: (314 − 240 + 1) / 30 = 2.50 s |
