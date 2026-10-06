# BÁO CÁO BÀI TẬP LAB 04: CORE ACTION, CADENCE & METRICS SYSTEM
## KHÓA HỌC: TRACK 1 - PRODUCT DISCOVERY & GROWTH ARCHITECTURE
**Mã nộp bài:** `Track1_Day20_02560_TaVietCuong`  

---

### 1. THÔNG TIN HỌC VIÊN & DỰ ÁN
* **Họ và tên:** **Tạ Việt Cường**
* **Mã học viên (MHV):** `2A2026002560`
* **Vai trò:** TechLead / Principal System Architect & Agentic Orchestrator
* **Dự án thực hiện:** **PricePolicy AI Agent – Nền tảng Định giá, Tối ưu hóa Phương án Tài chính & Bảo chứng Chính sách Bán hàng Bất động sản VLandFuture** (Mã sản phẩm: `BDSVLandFuture-06`)
* **Chân dung người dùng trọng tâm (Primary Persona):** **Nhân viên Kinh doanh BĐS Tuyến đầu (Sales Executive)** – Đại diện: *Hoàng Nam (27 tuổi)*.

---

### 2. LIÊN KẾT BÀI NỘP CHÍNH (METRICS PACK)
* 📄 **Tệp Metrics Pack hoàn chỉnh (Đã cấp quyền xem & đối soát):**  
  👉 [**metrics-pack.md**](metrics-pack.md)  
  *(Chứa đầy đủ 7 phân mục từ `00 — Phạm vi` đến `06 — Tracking nhanh`, kèm theo bảng tự kiểm 5 Gate và Rationale điều chỉnh thiết kế).*

* 📝 **Nhật ký sử dụng & phản biện AI:**  
  👉 [**ai-support-log.md**](ai-support-log.md)  
  *(Ghi nhận chi tiết các điểm AI hỗ trợ tốt, các điểm AI đề xuất sai bản chất nghiệp vụ và các quyết định học viên tự điều chỉnh).*

---

### 3. ĐIỀU TÔI MANG VỀ ÁP DỤNG CHO DỰ ÁN THẬT (KEY TAKEAWAYS)

Qua bài thực hành Lab 04, tôi đúc kết 4 bài học kiến trúc cốt tử để áp dụng trực tiếp vào việc phát triển nền tảng **PricePolicy AI Agent** cho sàn VLandFuture:

1. **Tư duy "Nature trước, Nurture sau" — Tuyệt đối không ép nhịp đo giả tạo:**  
   Trong sản phẩm B2B Bất động sản, nhịp làm việc của nhân viên kinh doanh gắn liền với lịch hẹn tư vấn và các đợt mở bán (Weekly/Campaign-based). Việc ép các chỉ số thói quen hàng ngày như DAU, streak đăng nhập hay spam notification chỉ tạo ra số liệu ảo và gây khó chịu cho người dùng. Thiết kế sản phẩm phải tôn trọng nhịp tự nhiên của nghiệp vụ.

2. **Core Action không phải là "Hỏi AI" — AI Output chưa phải là User Value:**  
   Một hệ thống AI chuyên sâu không được đo lường bằng số lượt gọi prompt hay độ dài câu trả lời. Giá trị thực sự chỉ xuất hiện khi kết quả của AI trở thành công cụ hành động của người dùng: khi Sale bấm xuất Báo giá bảo chứng (`validated_quote_exported`) với cam kết 100% không sai lệch dòng tiền và sạch bóng xung đột chính sách.

3. **Product Loop bền vững phải dựa trên "Tích lũy trạng thái" (Saved State):**  
   Lý do quay lại mạnh mẽ nhất của người dùng không phải là email hay notification nhắc nhở, mà là **Ví hồ sơ giao dịch (Snapshot)** được lưu trữ an toàn trong hệ thống. Khi khách hàng cũ muốn đối soát, đổi phương án hoặc chốt cọc, quy trình tự nhiên buộc Sale phải quay lại mở lại trạng thái đã lưu.

4. **Kỷ luật dữ liệu trong Tracking — Mọi Event đều phải có trách nhiệm giải trình:**  
   Không thu thập dữ liệu tràn lan theo kiểu "track mọi click". Mọi event gửi về kho dữ liệu đều phải map chính xác về một metric trong hệ thống, đồng thời bắt buộc phải có Acceptance Criteria chặt chẽ (chống bắn event sớm khi file chưa render xong, chống duplicate khi mạng gián đoạn) để bảo đảm độ tin cậy tuyệt đối của dữ liệu.

---
**Hà Nội, Ngày 06 Tháng 10 Năm 2026**  
*Tạ Việt Cường*
