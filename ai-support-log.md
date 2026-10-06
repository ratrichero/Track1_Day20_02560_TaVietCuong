# NHẬT KÝ SỬ DỤNG VÀ PHẢN BIỆN AI (AI SUPPORT LOG)
## DỰ ÁN: PRICEPOLICY AI AGENT (BDSVLANDFUTURE-06)
**Học viên:** Tạ Việt Cường 
**Môn học:** Track 1 - Product Discovery & Growth Architecture  

---

### 1. AI đã giúp tôi ở đâu?

* **Brainstorm và phân tách ranh giới khái niệm:**  
  AI hỗ trợ rất tốt trong việc phản biện để bóc tách 4 khái niệm dễ nhầm lẫn (*Core Job* vs *Core Action* vs *Core Value* vs *Core Value Event*). Đặc biệt, AI giúp tôi làm rõ ranh giới: AI sinh ra kết quả tính toán (`scenario_simulated`) chỉ là *System Output*, chưa phải là hành vi nhận giá trị của người dùng; chỉ khi Sale bấm xuất Báo giá bảo chứng (`validated_quote_exported`) để đưa cho khách, giá trị thương mại mới chính thức kích hoạt.
* **Chuẩn hóa danh mục Event theo chuẩn `object_action`:**  
  AI đã gợi ý danh sách naming convention chuẩn cho 6 core events trong phễu tư vấn định giá, giúp việc ánh xạ giữa tầng giao diện, tầng nghiệp vụ và tầng dữ liệu trở nên trong sáng.
* **Gợi ý các ca bẫy kỹ thuật cho Tiêu chí nghiệm thu (Acceptance Criteria):**  
  AI đóng vai trò kỹ sư dữ liệu khó tính, nhắc nhở về 2 cạm bẫy tracking phổ biến: bẫy phát sinh event khi người dùng mới click nút nhưng backend chưa render xong file PDF, và bẫy nhân đôi số liệu khi người dùng reload trang hoặc mạng chập chờn gửi retry request.

---

### 2. AI sai, hời hợt hoặc đề xuất metric sai nature ở đâu?

* **Đề xuất đo DAU và ép thói quen hàng ngày (Daily Habit) một cách máy móc:**  
  Khi mới bắt đầu, AI có xu hướng áp dụng tư duy của ứng dụng B2C Social/Consumer App: đề xuất đo DAU/MAU, đề xuất tính năng nhắc nhở "Daily Login", streak điểm danh nhận huy hiệu cho Sale. Đây là sai lầm nghiêm trọng vi phạm Luật 2 & 3. Thực tế ngành BĐS, Sale không gặp khách mọi ngày trong tuần; giữa tuần là thời gian tìm kiếm data, cuối tuần mới là cao điểm tư vấn tại sự kiện mở bán. Ép Daily là bóp méo bản chất tự nhiên.
* **North Star Metric mang tính số lượng thuần túy (Vanity Metric):**  
  AI ban đầu gợi ý NSM là *"Tổng số lượt hỏi đáp chính sách thành công"* hoặc *"Số lượt người dùng hoạt động"*. Chỉ số này rất dễ bị "game" (Sale có thể spam hỏi AI linh tinh) và không có ngưỡng chất lượng (*Quality Threshold*), hoàn toàn không chứng minh được liệu câu trả lời đó có giúp chốt deal an toàn hay không.
* **Áp dụng Retention D1/D7/D30 rập khuôn:**  
  AI tự động vẽ bảng Retention theo ngày (Day 1, Day 7, Day 30) mà không đối chiếu với chu kỳ mua bán BĐS. Nếu Sale không có lịch tiếp khách vào ngày D7 thì việc họ không vào app không có nghĩa là họ đã rời bỏ sản phẩm (churn).

---

### 3. Tôi đã tự sửa hoặc quyết định lại điều gì?

1. **Quyết định chuyển đổi Persona mục tiêu sang Sales Executive:**  
   Tôi đã chủ động chọn Persona là Sale tuyến đầu thay vì cấp Quản lý (Sales Director). Persona Sale có tần suất giao dịch dày dặn hơn (Weekly), gắn trực tiếp với bàn tư vấn chốt khách, giúp Product Loop vận hành sinh động và tạo ra giá trị bảo chứng tức thì.
2. **Tự định nghĩa lại North Star Metric chuẩn 3 thành phần có rào chắn chất lượng:**  
   Tôi bác bỏ chỉ số số lượng của AI và thiết lập lại NSM: **Weekly Conflict-Free Validated Quotes** (Báo giá tài chính tối ưu được xuất thành công không xung đột chính sách hàng tuần). Trong đó, ép buộc điều kiện chất lượng ngặt nghèo: **Zero Policy Conflict + Zero Math Error + 100% Citation Linking**.
3. **Loại bỏ Notification cưỡng ép, thiết lập cơ chế Saved State trong Product Loop:**  
   Tôi bác bỏ các đề xuất notification spam của AI, thay vào đó thiết kế **Lý do quay lại tự nhiên (Reason to Return)** dựa trên **Ví hồ sơ Snapshot bất biến**. Khi khách cũ muốn đổi phương án thanh toán hoặc chốt cọc, Sale bắt buộc phải quay lại mở Snapshot để lấy mã đối soát.
4. **Chuẩn hóa Cadence theo chu kỳ Tuần (Weekly):**  
   Tôi kiên quyết kết luận Cadence theo nhịp Weekly (2–5 lần/tuần), đồng thời xây dựng Retention 6 thành phần hoàn toàn khớp với Weekly Bracket, bảo đảm tính nhất quán tuyệt đối từ Phase 2 sang Phase 4.

---
**Học viên ký xác nhận:**  
*Tạ Việt Cường*
