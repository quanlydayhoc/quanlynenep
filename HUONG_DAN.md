# Sổ đầu bài điện tử — Trường THPT Bình Thạnh Đông (bản online)

Hệ thống gồm sổ đầu bài theo tuần vnEdu, sổ nề nếp, thi đua tuần các lớp và đánh giá hạnh kiểm tháng (100 điểm, trừ theo vi phạm).

| File | Đặt ở đâu | Vai trò |
|---|---|---|
| `index.html` | GitHub Pages | Trang web cho mọi người dùng |
| `Code.gs` | Apps Script của một Google Sheet | Máy chủ: đăng nhập, phân quyền, tính điểm, lưu dữ liệu |

Mọi dữ liệu nằm trong **một Google Sheet** của trường. Bảng tính có các trang dễ đọc, có thể mở xem hoặc sửa trực tiếp:

| Trang | Nội dung |
|---|---|
| `CauHinh` | Tên trường, hiệu trưởng, bí thư Đoàn, năm học, tuần 1, cách tính điểm |
| `DanhMuc` | Danh mục vi phạm và khen thưởng, kèm điểm học sinh và điểm thi đua lớp |
| `TaiKhoan` | Tài khoản, mật khẩu, môn, lớp giảng dạy, lớp chủ nhiệm, vai trò |
| `HocSinh` | Danh sách học sinh từng lớp |
| `SoDauBai` | Mỗi tiết một dòng: môn, bài, vi phạm, khen thưởng, xếp loại, GV ký, lịch sử sửa |
| `NeNep` | Ghi nhận của Đoàn trường, GVCN, BGH: ngày, lớp, học sinh, nội dung, điểm |

---

## 1. Cài máy chủ (khoảng 5 phút, làm một lần)

1. Vào sheets.google.com, tạo bảng tính mới, đặt tên **SoDauBai_BTD_2026-2027**.
2. Mở **Tiện ích mở rộng → Apps Script**, xoá nội dung mẫu, dán toàn bộ `Code.gs`, rồi bấm **Lưu**.
3. Mở **Cài đặt dự án** (biểu tượng bánh răng), chọn Múi giờ **(GMT+07:00) Ho Chi Minh**.
4. Chọn hàm **`setup`** rồi bấm **Chạy**. Khi Google hỏi quyền: chọn tài khoản → Nâng cao → Đi tới dự án → Cho phép.
5. Bấm **Triển khai → Tùy chọn triển khai mới**:
   - Loại: Ứng dụng web
   - Thực thi với tư cách: **Tôi**
   - Người có quyền truy cập: **Bất kỳ ai**
   - Chép URL có dạng `https://script.google.com/macros/s/…/exec`.

> Sau này nếu sửa `Code.gs`, vào **Triển khai → Quản lý triển khai → Chỉnh sửa → Phiên bản mới** để giữ nguyên URL.

## 2. Đưa trang lên GitHub Pages

1. Mở `index.html`, tìm dòng `const DEFAULT_API_URL = '';` và dán URL `/exec` vào giữa hai dấu nháy.
2. Trên GitHub, tạo repository **Public** (ví dụ `sodaubai-btd`) → **Add file → Upload files** → tải lên `index.html` và `.nojekyll`.
3. Vào **Settings → Pages**, chọn **Deploy from a branch**, nhánh **main**, thư mục **/(root)**, rồi bấm **Save**.
4. Sau 1–2 phút, trang chạy tại `https://<tên-github>.github.io/sodaubai-btd/`.

Nếu chưa dán URL vào file, trang chạy ở **chế độ dùng thử** (dữ liệu chỉ lưu trên máy đang dùng). Khi đó vẫn có thể bấm **Kết nối máy chủ** trên màn hình đăng nhập để dán URL.

## 3. Quản trị cấu hình (đăng nhập tab Quản trị, mật khẩu mặc định `admin123`)

Vào **Cấu hình** và làm lần lượt:

1. **Trường & năm học**
   - Tải **logo trường**: logo hiện trên đầu trang, trên bản in và trong file Excel. Nên dùng ảnh vuông, nền trong suốt; ảnh được tự thu nhỏ khi lưu.
   - Nhập tên trường, đơn vị chủ quản, địa chỉ, tên Hiệu trưởng, tên Bí thư Đoàn. Các thông tin này được in lên báo cáo.
   - Chọn thứ Hai đầu tuần 1 sao cho số tuần khớp với vnEdu.
   - **Đổi mật khẩu quản trị.**
2. **Điểm & xếp loại**
   - Điểm rèn luyện học sinh mỗi tháng (mặc định 100).
   - Ngưỡng hạnh kiểm: Tốt ≥ 90, Khá ≥ 70, Đạt ≥ 50, còn lại Chưa đạt.
   - Có cho điểm khen thưởng bù vào điểm đã trừ hay không.
   - Điểm thi đua lớp mỗi tuần (mặc định 100), và điểm cộng/trừ theo xếp loại tiết A/B/C/D.
3. **Danh mục vi phạm, khen thưởng** (có sẵn 29 nội dung mẫu). Mỗi nội dung có:
   - **Điểm học sinh**: trừ hoặc cộng vào điểm rèn luyện tháng.
   - **Điểm lớp**: trừ hoặc cộng vào thi đua tuần.
   - **Phạm vi "Cả lớp"**: dùng cho nề nếp do Đoàn trường chấm (vệ sinh, xếp hàng, trực nhật…), không trừ điểm cá nhân.
   - Có thể sửa, thêm, tắt, nhập hoặc xuất Excel.
4. **Tài khoản & phân công**: nhập file Excel với các cột `Họ và tên | Tài khoản | Mật khẩu | Môn | Lớp giảng dạy | Lớp chủ nhiệm | Vai trò`.
   - Vai trò: `GV` (giáo viên), `BGH` (Ban giám hiệu), `DOAN` (Đoàn trường), `XUAT` (được xuất báo cáo). Một người có thể giữ nhiều vai trò, ví dụ `GV, DOAN`.
   - Ai có giá trị ở cột **Lớp chủ nhiệm** sẽ là GVCN của lớp đó.

## 4. Ai làm gì

| Người dùng | Việc được làm |
|---|---|
| **Giáo viên bộ môn** | Ký sổ các lớp mình dạy. Trong mỗi tiết: chọn học sinh và chọn vi phạm từ danh mục, ghi điểm hồng hoặc tuyên dương, nhận xét, xếp loại tiết. |
| **GVCN** | Mọi việc của giáo viên bộ môn, cộng thêm: nhập danh sách học sinh lớp mình (gõ hoặc nhập Excel), ghi nề nếp cho lớp mình, xem điểm rèn luyện tháng từng em, xuất hạnh kiểm lớp mình. |
| **Đoàn trường** | Ghi nề nếp và thi đua cho mọi lớp (trừ hoặc cộng cả lớp, hoặc từng học sinh), xem bảng xếp hạng tuần, xuất thi đua và danh sách vi phạm. |
| **Ban giám hiệu / Hiệu trưởng** | Xem toàn trường. Xuất **hạnh kiểm tháng**, **danh sách vi phạm**, **thi đua tuần**, **sổ đầu bài tổng kết**. |
| **Quản trị** | Toàn quyền cấu hình. Xoá tiết, sao lưu và khôi phục dữ liệu. |

Máy chủ tự kiểm tra các quyền này, nên không thể vượt qua bằng cách sửa giao diện. Cụ thể:

- Giáo viên không ký được lớp ngoài phân công.
- Tiết đã ký chỉ người ký (hoặc quản trị) mới sửa được.
- Mỗi lần sửa, tiết đó **tô đỏ** kèm tên người sửa và giờ sửa do máy chủ ghi.
- Học sinh phải có trong danh sách lớp.
- Nội dung vi phạm phải có trong danh mục, và điểm được ghi lại đúng tại thời điểm ghi nhận (sau này sửa danh mục không làm đổi các ghi nhận cũ).

## 5. Cách tính điểm

- **Điểm rèn luyện tháng của học sinh**
  = 100 − tổng điểm trừ của các vi phạm trong tháng (cả trong tiết học và sổ nề nếp)
  (+ điểm khen thưởng nếu bật tuỳ chọn bù, tối đa 100).
  Sau đó xếp loại hạnh kiểm theo các ngưỡng đã cấu hình.
- **Điểm thi đua tuần của lớp**
  = 100 + điểm theo xếp loại các tiết − điểm trừ lớp (vi phạm của học sinh và nề nếp Đoàn trường) + điểm cộng lớp.
  Lớp cao điểm hơn xếp hạng trên.

## 6. Báo cáo

**Ai được xuất báo cáo:**
- GVCN: xuất hạnh kiểm, vi phạm, sổ đầu bài của lớp mình, và bảng thi đua toàn trường.
- Đoàn trường, Ban giám hiệu, và tài khoản được quản trị tích **"Được xuất báo cáo"**: xuất toàn trường.
- Giáo viên bộ môn: không có mục Báo cáo.

**File hạnh kiểm tháng (Excel) gồm 3 sheet:**
1. **Tổng hợp**: cả lớp, có và không vi phạm. Gồm số lần vi phạm, điểm trừ, điểm hồng, tuyên dương, điểm tháng, xếp loại, ghi chú nội dung vi phạm, và dòng cộng.
2. **Tốt**: các học sinh không vi phạm trong tháng, kèm khen thưởng.
3. **Vi phạm**: mỗi lần vi phạm một dòng (ngày, nội dung, điểm trừ, ai ghi nhận). Các ô họ tên, tổng trừ, điểm tháng, xếp loại được gộp theo từng học sinh.

Mỗi sheet có tiêu đề hành chính (Sở, trường, logo, quốc hiệu), tên báo cáo, dòng thống kê, bảng tô màu, và phần ký **Hiệu trưởng** / **Giáo viên chủ nhiệm (Người lập bảng)**. Bảng ngắn được thu vừa một trang A4; bảng dài thì lặp tiêu đề cột ở mỗi trang.

Các báo cáo đều xuất được ra **Excel** và **bản in** (mở bằng trình duyệt, bấm Ctrl + P để in hoặc lưu PDF). Bản in có quốc hiệu và chỗ ký.

- **Hạnh kiểm tháng**:
  - Sheet tổng hợp toàn trường.
  - Mỗi lớp một sheet: STT, họ tên, số lần vi phạm, điểm trừ, điểm hồng, tuyên dương, điểm tháng, xếp loại.
  - Sheet chi tiết từng ghi nhận.
- **Danh sách vi phạm** theo khoảng ngày, kèm thống kê theo học sinh và theo nội dung.
- **Thi đua tuần**: bảng xếp hạng từng tuần và điểm trung bình nhiều tuần.
- **Sổ đầu bài tổng kết**: toàn bộ tiết đã ghi, các tiết đã sửa được tô đỏ.

## 7. Sao lưu

Định kỳ vào **Cấu hình → Dữ liệu → Tải file sao lưu**. Có thể làm thêm *Tệp → Tạo bản sao* của Google Sheet. Phiên đăng nhập hết hạn sau 6 giờ. Không chia sẻ Google Sheet cho người ngoài, vì trang `TaiKhoan` có mật khẩu.

---
Thiết kế: Lương Khánh Tường — Trường THPT Bình Thạnh Đông, An Giang · ĐT/Zalo 0916780807
