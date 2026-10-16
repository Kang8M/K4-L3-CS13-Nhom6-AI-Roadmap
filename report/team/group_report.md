# Báo cáo nhóm — Nhóm 6 · CS13

## 1. Thông tin nhóm

- Tên nhóm: Nhóm 6
- Đề CS13: Đề 3 · Ra Viện — Trợ lý soạn nháp tóm tắt ra viện cho bác sĩ khoa nội
- Thành viên: xem [team/TEAM.md](../../team/TEAM.md).

## 2. Mục tiêu và cách tiếp cận

Ban lãnh đạo cần lộ trình 12 tháng trả lời ba câu: **làm gì trước, khi nào cho AI tự làm nhiều hơn, khi nào dừng**.

Căn cứ lấy từ hồ sơ tình huống (`CS13_HoSoTinhHuong.pdf`, Đề 3):

- 1 việc = 1 bản nháp tóm tắt ra viện cho 1 người bệnh; khoa nội ~40 người ra viện/ngày, bác sĩ mất 15–20 phút/bản.
- Kết quả bộ đề: tỷ lệ đạt 96,6% (≥ 95%), kappa 0,90, **nhưng 1 lỗi nghiêm trọng** (liều insulin tối ghi thành sáng) → **chưa phát hành**.
- "Một lỗi thuốc lọt đến người bệnh là dừng ngay" (BS. Phương). Bác sĩ luôn đọc, sửa, ký; người duyệt của công ty là dược sĩ kiểm phần thuốc.
- Số liệu kinh tế: 15 triệu/khoa/tháng cho 1.200 bản; AI 2.968 đ + hạ tầng 1.200 đ/bản; dược sĩ 3 phút × 150.000 đ/giờ; kịch bản xấu hết tiền tháng 9.

Nhóm viết mỗi việc thành giả thuyết "Ta tin rằng làm X cho Y sẽ đạt Z", gắn chỉ số có ngưỡng, rồi chấm ưu tiên bằng công thức của file.

## 3. Giải pháp

- **Làm trước — Việc 2: đối chiếu thuốc ra viện với y lệnh cuối** (điểm 9,56, hạng 1; `1_Danh sách việc` dòng 6). Đây là cách xử lý trực tiếp lỗi nghiêm trọng đang chặn phát hành, đồng thời là điều kiện để giảm chi phí duyệt về sau.
- Việc 1 (soạn nháp, hạng 2) chỉ chạy thật sau khi Việc 2 qua cổng. Nhóm thêm **Việc 7: đo tỷ lệ bản nháp bị sửa nhiều** (hạng 3) vì đó là biến nguy hiểm nhất và là căn cứ của điều kiện dừng.
- Việc 3 làm ở tầng Tiếp theo; Việc 4, 5 `Chờ` (xem lại tháng 6); Việc 6 `Không làm` vì bệnh viện đã có phần mềm mã hoá bệnh.
- **Mức tự động** (`2_Mức tự động`):
  - Mức 0 — chỉ chạy trên bộ đề, sửa lỗi insulin (tháng 1).
  - Mức 1 — Hỗ trợ có duyệt, thử nghiệm 3 tháng tại 1 khoa nội: bác sĩ ký 100%, dược sĩ kiểm thuốc 100%. Cổng: 0 lỗi nghiêm trọng trên 45 hồ sơ (40 + 5 ca insulin), tỷ lệ đạt ≥ 95%, 0 tầng tụt, kappa ≥ 0,8.
  - Mức 2 — Tự động một phần: dược sĩ kiểm ~10% (bản có cờ + mẫu ngẫu nhiên), bác sĩ vẫn ký 100%. Cổng: 0 lỗi thuốc nghiêm trọng trên ≥ 1.500 bản thật liên tiếp (quy tắc 3: lỗi < 0,2%, độ tin 95%), sửa nhiều ≤ 20%.
  - Mức 3 — máy tự gửi: **Không làm**.
- **Lộ trình** (`3_Bảng lộ trình`) chia Bây giờ / Tiếp theo / Sau này; **lịch rà soát** (`4_Rà soát`) ở ngày 30/60/90 và ba sự kiện (mô hình mới, đối thủ, quy định).

## 4. Kết quả

| Hạng mục | Kết quả |
| --- | --- |
| File Excel | [`Nhom6_CS13.xlsx`](../../Nhom6_CS13.xlsx) — làm từ `CS13_Roadmap_De3.xlsx` |
| Tự kiểm tra (`6_Tự kiểm tra`) | 8/8 Đạt: 7 việc đã chấm; 0 việc thiếu chỉ số; 3 mức có cổng bằng số; 8/8 ô Bây giờ; điều kiện dừng và căn cứ kinh tế có số; 5/5 ô slide; 1 mức biên ≥ 60% |
| Chi phí / biên gộp | Giá 12.500 đ/bản. Mức 0–1: 11.668 đ/bản, biên 6,7%. Mức 2: 4.918 đ/bản, biên **60,7%** |
| Slide lãnh đạo | [`Nhom6_CS13_Slide.pptx`](../../Nhom6_CS13_Slide.pptx) — 1 slide, kết luận trước, 5 ý khớp trang `5_Slide lãnh đạo` (mỗi ô ≤ 60 chữ) |

## 5. Khó khăn và cách xử lý

- **Biên lợi nhuận Mức 1 chỉ 6,7%** vì dược sĩ phải kiểm 100%. Nhóm không bỏ bước an toàn để có số đẹp; thay vào đó đặt cổng bằng dữ liệu thật (1.500 bản liên tiếp 0 lỗi) để giảm xuống 10% ở Mức 2, đạt 60,7%.
- **Điều kiện dừng "hết tháng 3 thử nghiệm" lệch với khung 0–3 tháng**: tháng 1 dành sửa lỗi, nên thử nghiệm kéo sang tháng 4. Nhóm để ngày 90 là mốc giữa thử nghiệm và quyết định cuối cùng rơi vào tầng Tiếp theo.
- **Chọn cỡ mẫu cho cổng Mức 2**: không thấy lỗi trên bộ đề nhỏ chưa chứng minh là không có lỗi; dùng quy tắc 3 để chọn 1.500 bản (đạt được trong ~1,3 tháng ở 1.200 bản/tháng).

## 6. Tổng hợp đóng góp

Điền đóng góp trong [team/TEAM.md](../../team/TEAM.md). Báo cáo cá nhân: [2A202602942_LuuManhHung.md](2A202602942_LuuManhHung.md), [2A202602705_TranVuGiaHuy.md](2A202602705_TranVuGiaHuy.md).

## 7. Hạn chế và hướng cải thiện

- Điểm F–L ở trang 1 là ước lượng của nhóm; cần kiểm chứng lại với BS. Phương và DS. Hải.
- Giả định "≤ 6 phút/bản" và "sửa nhiều > 30% nội dung" chưa đo thật — sẽ đo ở thử nghiệm, xem lại ngày 60 và 90.
- Tỷ lệ dược sĩ kiểm 10% ở Mức 2 là giả định; nếu cờ thuốc gắn nhiều hơn dự kiến, biên sẽ dưới 60%.
- Quy định áp dụng cho AI trong y tế (Luật AI 134/2025/QH15, dữ liệu sức khoẻ) cần đối chiếu văn bản gốc trước khi thử nghiệm.

## 8. Tài liệu tham khảo

- `CS13_HoSoTinhHuong.pdf` — Hồ sơ tình huống, Đề 3 (trang 6–7).
- `CS13_Roadmap_De3.xlsx` — file đề, số liệu kinh tế trang 2 dòng 12–20.
- Hướng dẫn lab CS13, `SUBMISSION.md`, `RUBRIC.md` (repo đề bài VinUni-AI20k/K4-L3-CS13-AI-Roadmap).
