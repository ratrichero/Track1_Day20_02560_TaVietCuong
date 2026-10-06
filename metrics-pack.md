# BỘ CHỈ SỐ SẢN PHẨM (METRICS PACK)
## DỰ ÁN: PRICEPOLICY AI AGENT – NỀN TẢNG ĐỊNH GIÁ & BẢO CHỨNG CHÍNH SÁCH BÁN HÀNG BẤT ĐỘNG SẢN VLANDFUTURE
**Mã dự án:** `BDSVLandFuture-06`  
**Học viên thực hiện:** Tạ Việt Cường 
Mã học viên: `2A202602560' 
  
---

## 00 — PHẠM VI (SCOPE)

1. **Dự án:**  
   **PricePolicy AI Agent** – Hệ thống AI Trợ lý Định giá, Tối ưu hóa Phương án Tài chính và Quản trị Tuân thủ Bán hàng Bất động sản (The Trust Layer for Real Estate Commercial Operations).
2. **Persona (Chân dung người dùng mục tiêu duy nhất):**  
   **Nhân viên Kinh doanh Tuyến đầu (Sales Executive)** – Đại diện: *Hoàng Nam (27 tuổi)*, chuyên viên tư vấn căn hộ cao cấp tại sàn giao dịch tập trung, nhà mẫu và kênh tư vấn số của VLandFuture.
3. **Core job:**  
   > *"Tôi mất quá nhiều thời gian vật lộn với bảng tính Excel và hàng chục trang văn bản chính sách nhiều tầng để tính lịch trả nợ/chiết khấu cho khách; tôi luôn nơm nớp lo tính nhầm làm mất khách hoặc bị trừ tiền hoa hồng đền bù do tư vấn vượt khung chính sách."*

---

## 01 — CORE ACTION CARD

### 1. Phân biệt 4 khái niệm cốt lõi

| Khái niệm | Câu hỏi trọng tâm | Định nghĩa cho Persona Sales Executive |
| :--- | :--- | :--- |
| **Core job** | User đang cố hoàn thành việc gì? | Cung cấp phương án thanh toán/giá chính xác và thuyết phục để chốt cọc nhanh, an toàn dòng tiền cho khách hàng mà không lo vi phạm chính sách. |
| **Core action** | User làm gì trong sản phẩm để tiến tới giá trị? | Lập và xuất Bảng so sánh phương án thanh toán tối ưu có bảo chứng căn cứ điều khoản (`Generate & Export Validated Pricing Proposal`). |
| **Core value** | User nhận được lợi ích gì? | Có ngay phương án tài chính tối ưu trong 10 giây; 100% chuẩn xác số học và pháp lý; tự tin tư vấn chốt deal; triệt tiêu rủi ro đền tiền do tư vấn sai. |
| **Core value event** | Sự kiện nào chứng minh value đã xảy ra? | `validated_quote_exported` (Kèm mã băm bất biến Snapshot SHA-256 xác nhận không có xung đột chính sách). |

> **Ghi chú tư duy:**  
> Core action không phải là "Hỏi AI" hay "Mở app". Hành vi AI sinh câu trả lời mới chỉ là output hệ thống. Chỉ khi Sale **chọn chốt phương án và xuất Báo giá bảo chứng (Quote Dossier)** để sử dụng cho khách hàng hoặc trình duyệt, giá trị thương mại mới chính thức được chuyển giao.

---

### 2. Core Action Card

| Thành phần | Nội dung chuẩn hóa |
| :--- | :--- |
| **Target user** | Nhân viên Kinh doanh BĐS Tuyến đầu (Sales Executive) tại sàn và sự kiện mở bán. |
| **Core job** | Lập phương án tài chính chuẩn xác, thuyết phục khách hàng mà không lo tính sai chính sách. |
| **Core action** | **Lập và xuất Bảng so sánh phương án thanh toán tối ưu có bảo chứng chính sách** (`Generate & Export Validated Pricing Proposal`). |
| **Object** | Hồ sơ Báo giá tài chính căn hộ (`Pricing Quote / Scenario Dossier`) gắn với mã căn cụ thể và hồ sơ khách hàng. |
| **Preconditions** | (1) Căn hộ đã chọn có trong giỏ hàng hiệu lực; (2) Ngày giao dịch hợp lệ; (3) Tiêu chí tối ưu tài chính của khách hàng được chỉ định (Vốn tự có đợt 1, Dòng tiền hàng tháng, hoặc Tổng giá thu về tối thiểu). |
| **Completion rule** | Hệ thống tính toán tất định 100% không lỗi số học, rà quét sạch xung đột chính sách, gán đầy đủ tọa độ điều khoản trích dẫn, và Sales bấm xuất Báo giá thành công (nhận HTTP 200 kèm Snapshot Hash). |
| **Core value** | Rút ngắn thời gian lập bảng tính từ 45 phút xuống dưới 10 giây; 100% chính xác về dòng tiền; tự tin chốt deal, bảo toàn hoa hồng. |
| **Evidence of value** | File Báo giá/Dossier được sinh thành công kèm mã tra cứu Snapshot, khách hàng nhận được bảng đối sánh 3 kịch bản minh bạch hoặc chuyển trạng thái đặt cọc. |
| **Candidate event** | `validated_quote_exported` |

---

### 3. Tự kiểm 5 tiêu chí (Gate 1 Validation)

1. **Gần core value (ĐẠT - 5/5):** Báo giá bảo chứng được xuất ra là bằng chứng Sale đã có phương án tài chính chuẩn xác nhất để đưa cho khách, chạm trực tiếp vào cốt lõi chốt giao dịch.
2. **Có thể lặp lại (ĐẠT - 5/5):** Hành vi xuất hiện lặp lại mỗi khi Sale tiếp một khách hàng mới, khi khách đổi căn hộ, hoặc khi khách yêu cầu đổi kịch bản thanh toán (từ vay sang trả thẳng).
3. **Có thể quan sát (ĐẠT - 5/5):** Đo lường tất định tại backend khi file báo giá được render thành công và lưu vết Snapshot vào cơ sở dữ liệu (`quote_id` sinh ra kèm timestamp).
4. **Có ý nghĩa (ĐẠT - 5/5):** Số lượng báo giá bảo chứng tăng đồng nghĩa với việc Sale đang tích cực tư vấn bằng công cụ chuẩn hóa, giảm thiểu rủi ro sai lệch thương mại của toàn sàn.
5. **Có thể tác động (ĐẠT - 5/5):** Đội ngũ sản phẩm có thể tối ưu luồng nhập liệu căn hộ, tăng tốc độ xử lý của động cơ tính toán và cải thiện giao diện so sánh để tăng tỷ lệ hoàn tất action.

> **KẾT LUẬN GATE 1:** VƯỢT QUA (5/5 tiêu chí). Core action có đầy đủ Actor, Object, Completion Rule rõ ràng, không phải là thao tác giao diện ("click nút", "mở app") hay output thụ động của LLM.

---

## 02 — NATURE & CADENCE

### 1. Action Nature Card

| Thành phần | Câu hỏi & Phân tích thực tế |
| :--- | :--- |
| **Actor** | Nhân viên kinh doanh cá nhân (`Sales Executive`). |
| **Intent** | Cần giải pháp tài chính ngay lập tức để đàm phán, so sánh và thuyết phục khách hàng trong buổi tư vấn. |
| **Trigger** | **External Trigger (Kích hoạt từ bên ngoài):** Khách hàng liên hệ hỏi căn hộ, khách đến xem nhà mẫu, hoặc sự kiện mở bán tập trung cuối tuần của Chủ đầu tư. |
| **Effort** | Thấp đến Trung bình: 30–60 giây thao tác nhập mã căn, chọn nhu cầu khách hàng và xác nhận phương án. |
| **Value timing** | **Ngay lập tức (Immediate Value):** Dưới 10 giây để nhận bảng so sánh 3 phương án và tải báo giá PDF hoàn chỉnh. |
| **State** | Hồ sơ báo giá được lưu vĩnh viễn vào hệ thống (`Immutable Snapshot` kèm mã băm SHA-256), gán với ID của Sale để phục vụ đối soát hoa hồng và tiếp tục chăm sóc lead. |
| **Dependency** | Phụ thuộc vào dữ liệu giỏ hàng của Chủ đầu tư (bảng hàng còn mở) và chính sách bán hàng còn hiệu lực. |
| **Repeat condition** | Khách hàng hỏi thêm căn hộ khác, khách muốn thay đổi tiêu chí dòng tiền, hoặc có khách hàng mới tiếp theo trong phễu. |

---

### 2. Dạng hành vi & Kết luận Cadence

* **Dạng hành vi đã chọn:** **Hành vi theo sự kiện giao dịch & phễu tư vấn (Event-response / Transactional workflow)**.
* **Kết luận Cadence theo template chuẩn:**
  > *"Đối với **Nhân viên Kinh doanh BĐS Tuyến đầu (Sales Executive)**, core action **Lập và xuất Bảng so sánh phương án thanh toán tối ưu có bảo chứng** thường xuất hiện **2 đến 5 lần mỗi tuần** (và bùng nổ theo ngày trong các đợt mở bán cao điểm) vì **nhu cầu tư vấn phụ thuộc trực tiếp vào lịch hẹn tiếp khách và lượng khách hàng tiềm năng phát sinh trong phễu bán hàng**. Do đó, nhịp đo phù hợp là **Weekly (theo tuần)** ở cấp **Active Sales Consultant**."*

* **Lập luận bảo vệ nguyên tắc Nature-first (Luật số 2 & 3):**
  - **Không ép Daily Habit:** Sale không gặp khách mọi ngày trong tuần (giữa tuần thường tìm kiếm data, cuối tuần tập trung dẫn khách). Nếu ép nhịp đo Daily (DAU) sẽ dẫn đến việc Sale bị làm phiền bởi notification rác hoặc gian lận tự tạo báo giá ảo.
  - **Nurture chỉ khuếch đại Nature:** Hệ thống chỉ gửi thông báo khi có sự kiện tự nhiên: chính sách mới được ban hành cho dự án Sale đang bán, hoặc khi giỏ hàng căn hộ Sale đang theo dõi sắp hết.

> **KẾT LUẬN GATE 2:** VƯỢT QUA. Cadence được suy ra từ nhịp làm việc thực tế của Sale BĐS (Weekly), không chạy theo dashboard máy móc.

---

## 03 — METRIC SYSTEM

```
                        ┌──────────────────────────────────────────────┐
                        │              NORTH STAR METRIC               │
                        │     Weekly Conflict-Free Validated Quotes    │
                        │    (Báo giá bảo chứng không xung đột/tuần)   │
                        └──────────────────────┬───────────────────────┘
                                               │
             ┌─────────────────────────────────┴─────────────────────────────────┐
             ▼                                                                   ▼
┌─────────────────────────┐                                         ┌─────────────────────────┐
│   LEADING INDICATORS    │                                         │     COUNTER-METRIC      │
│ 1. Scenario Comp Rate   │                                         │ 1. Quote Rejection Rate │
│ 2. Compliance Pass Rate │                                         │    (Tỷ lệ từ chối ≤ 1.5%)│
│ 3. Time-to-Quote < 30s  │                                         │ 2. Token Cost / Quote   │
└─────────────────────────┘                                         └─────────────────────────┘
```

### 1. Activation Metric
* **Start event:** `sales_account_activated` (Tài khoản Sale được kích hoạt và cấp quyền truy cập giỏ hàng dự án).
* **Activation event:** `first_validated_quote_exported` (Lần đầu tiên xuất thành công 1 bảng báo giá bảo chứng có mã Snapshot).
* **Time window:** Trong vòng **48 giờ** kể từ start event (thời điểm vàng khi Sale vừa được tiếp cận giỏ hàng và chính sách mới).

### 2. Engagement Metric
* **Frequency:** `Weekly Validated Quotes per Active Sale` (Số lượng báo giá bảo chứng được xuất / Sale / tuần — mục tiêu: ≥ 3 báo giá/tuần).
* **Depth:** `Multi-Scenario Comparison Depth Rate` (Tỷ lệ báo giá có thực hiện so sánh đối đầu đủ 3 kịch bản: HTLS vs Tiến độ chuẩn vs Thanh toán sớm ≥ 80%).

### 3. North Star Metric (NSM)
* **Tên chỉ số:** **Weekly Conflict-Free Validated Quotes (Số lượng Báo giá tài chính tối ưu được xuất thành công không xung đột chính sách hàng tuần)**.
* **Bóc tách theo công thức chuẩn 3 thành phần:**
  1. **Unit of value:** Báo giá tài chính tối ưu (`Validated Pricing Quote / Dossier`).
  2. **Quality threshold:** **Zero Policy Conflict + Zero Math Error + 100% Citation Linking** (100% không vi phạm điều khoản loại trừ chính sách, sai số số học bằng 0, có đầy đủ tọa độ trích dẫn Điều khoản F4).
  3. **Frequency:** Hàng tuần (**Weekly**).
* **Ý nghĩa:** Chỉ số này phản ánh trực tiếp giá trị thực tế mà sàn giao dịch nhận được: số lượng cơ hội bán hàng được trang bị vũ khí tài chính an toàn, giúp tăng tỷ lệ chốt cọc mà không gây rủi ro pháp lý hay hao hụt biên lợi nhuận.

### 4. Leading Indicators (Tối đa 3 chỉ số dự báo)
1. **`scenario_comparison_completed_rate` (Tỷ lệ phiên tư vấn hoàn thành mô phỏng 3 kịch bản):**  
   *Lý do dự báo:* Sale xem đủ 3 phương án chứng tỏ họ đang tìm giải pháp tối ưu cho khách, xác suất bấm xuất báo giá cuối cùng cao hơn 3.5 lần so với phiên chỉ xem 1 phương án.
2. **`compliance_first_pass_rate` (Tỷ lệ phương án qua cửa kiểm soát tuân thủ ngay lần đầu):**  
   *Lý do dự báo:* Tỷ lệ này cao chứng tỏ Sale nắm chắc điều kiện chính sách, giảm thiểu thời gian sửa đổi và drop-off trước khi xuất báo giá.
3. **`time_to_quote_duration` (Thời gian từ khi chọn căn đến khi ra kết quả so sánh < 30 giây):**  
   *Lý do dự báo:* Tốc độ phản hồi dưới 30 giây giúp Sale tự tin sử dụng trực tiếp trước mặt khách hàng tại bàn tư vấn, thúc đẩy hành vi lặp lại thường xuyên.

### 5. Counter-metric (Chỉ số đối trọng)
1. **`quote_rejection_or_complaint_rate` (Tỷ lệ báo giá bị Quản lý từ chối duyệt hoặc Khách hàng khiếu nại sai thông tin ≤ 1.5%):**  
   *Mục đích đối trọng:* Ngăn chặn hành vi Sale bấm xuất hàng loạt báo giá rác hoặc nhập dữ liệu giả mạo để "cày" chỉ số NSM.
2. **`cost_per_quote_token_ratio` (Chi phí suy luận LLM trên mỗi báo giá xuất ra ≤ 0.04$):**  
   *Mục đích đối trọng:* Đảm bảo hệ thống tối ưu hóa việc phân tách giữa LLM (nhận diện) và Python Math Engine (tính toán), không làm phình chi phí hạ tầng khi quy mô sử dụng tăng vọt.

> **KẾT LUẬN GATE 3:** VƯỢT QUA. NSM đủ 3 thành phần, Activation có Time Window rõ ràng, có 2 Counter-metric kiểm soát chất lượng và chi phí.

---

## 04 — RETENTION DEFINITION

Bảng định nghĩa Retention chuẩn 6 thành phần:

| Thành phần | Định nghĩa chi tiết |
| :--- | :--- |
| **1. Unit** | Người dùng cá nhân: `Sales Executive` (Nhân viên kinh doanh). |
| **2. Cohort entry** | Tuần đầu tiên Sale phát sinh sự kiện `first_validated_quote_exported` (Kích hoạt thành công). |
| **3. Return event** | Sự kiện Core Action lặp lại: `validated_quote_exported`. |
| **4. Window** | **Weekly Bracket** (Tuần W1, W2, W3, W4, W8... tính theo 7 ngày liên tiếp). |
| **5. Threshold** | ≥ 2 lần xuất báo giá bảo chứng thành công trong tuần đánh giá. |
| **6. Segment** | Phân tách 2 nhóm: (A) Sales cơ hữu sàn VLandFuture; (B) Sales đối tác phân phối liên kết (Đại lý F1). |

* **Lập luận khớp với Cadence:**  
  Retention được đo theo tuần (Weekly) vì chu kỳ bán hàng BĐS vận hành theo tuần tiếp khách. Đo Retention D1/D7 (Daily) là sai lầm kinh điển vì Sale không có nghĩa vụ tạo báo giá vào các ngày không có lịch hẹn.

---

## 05 — PRODUCT LOOP

### 1. Sơ đồ Product Loop 2 chu kỳ hoàn chỉnh

```
[EXTERNAL TRIGGER: Khách hỏi căn hộ ZEN-A-1205]
                     │
                     ▼
       ┌───────────────────────────┐
       │   CORE ACTION (Chu kỳ 1)  │ ──► Nhập mã căn, chọn tiêu chí MIN_INITIAL_CASH,
       │  Lập & Xuất Báo giá HTLS  │     AI giải mã chính sách & tính toán trong 5s.
       └─────────────┬─────────────┘
                     ▼
       ┌───────────────────────────┐
       │      IMMEDIATE VALUE      │ ──► Nhận Bảng so sánh 3 kịch bản đối đầu;
       │   (Giá trị tức thì)       │     Tải Báo giá PDF bảo chứng gửi khách qua Zalo.
       └─────────────┬─────────────┘
                     ▼
       ┌───────────────────────────┐
       │  SAVED STATE / INVESTMENT │ ──► Snapshot báo giá được lưu vào ví hồ sơ của Sale;
       │  (Tích lũy trạng thái)    │     Tọa độ chính sách & thông tin căn được ghim lại.
       └─────────────┬─────────────┘
                     │
                     ▼
[NEXT NATURAL TRIGGER: Khách muốn đổi phương án sang Trả thẳng để lấy chiết khấu tối đa]
                     │
                     ▼
       ┌───────────────────────────┐
       │   CORE ACTION (Chu kỳ 2)  │ ──► Mở lại Snapshot cũ trong 3 giây, đổi tiêu chí
       │ Xuất Báo giá Thanh toán sớm│    sang MIN_NET_PRICE; AI tính lại tức thì.
       └─────────────┬─────────────┘
                     ▼
       ┌───────────────────────────┐
       │       REPEAT VALUE        │ ──► Khách chốt cọc vì minh bạch phương án dòng tiền;
       │   (Giá trị củng cố)       │     Sale nhận hoa hồng, tin tưởng tuyệt đối vào tool.
       └───────────────────────────┘
```

* **Loại loop chính:** **Transactional Workflow Loop kết hợp Habit Loop**.
* **Reason to return nếu loại bỏ hoàn toàn Notification:**  
  Sale quay lại vì **toàn bộ lịch sử báo giá của khách hàng (Saved State) được lưu trữ an toàn trong ví hồ sơ**. Khi khách gọi lại hỏi phương án khác hoặc khi cần làm thủ tục ráp căn đặt cọc, Sale bắt buộc phải mở lại hệ thống để lấy mã Snapshot đối soát. Không cần bất kỳ notification nào, quy trình chốt deal tự nhiên buộc Sale phải quay lại.

### 2. Metric Hypothesis
> *"Nếu loop này hoạt động, metric **Weekly Conflict-Free Validated Quotes per Active Sale** sẽ tăng **40% trong vòng 4 tuần**, vì **Sale giảm thời gian lập bảng thanh toán từ 45 phút xuống dưới 30 giây, giúp họ tăng gấp 3 lần số lượng khách được tư vấn chuyên sâu trong mỗi phiên mở bán mà không sợ rủi ro đền tiền do tính sai**."*

> **KẾT LUẬN GATE 4A:** VƯỢT QUA. Loop đủ 2 chu kỳ logic, có lý do quay lại nội tại (Saved State), có Metric Hypothesis lượng hóa rõ ràng.

---

## 06 — TRACKING NHANH (FAST TRACKING PLAN)

### 1. Bảng 6 Core Events

| Tên Event (`object_action`) | Ý nghĩa nghiệp vụ | Thời điểm ghi nhận (Trigger Point) | Metric sử dụng ở Phase 3 |
| :--- | :--- | :--- | :--- |
| `sales_account_activated` | Tài khoản Sale được cấp quyền truy cập giỏ hàng | Ngay khi user đăng nhập lần đầu và hệ thống xác thực phân quyền thành công | Start event của **Activation Metric** |
| `property_selected` | Sale chọn một mã căn hộ để bắt đầu tư vấn | Khi mã căn hợp lệ được chọn và dữ liệu giá niêm yết được tải lên màn hình | Leading: Phễu bắt đầu tư vấn |
| `scenario_simulated` | Hệ thống hoàn tất tính toán so sánh 3 phương án | Khi Python Math Engine trả về kết quả tính toán thành công và render lên UI | Leading: `scenario_comparison_completed_rate` |
| `policy_conflict_cleared` | Hệ thống xác nhận không có xung đột điều khoản | Cửa kiểm soát F3/F8 quét xong và gán nhãn hợp lệ (`CONFLICT_FREE`) | Quality filter cho **NSM** |
| `validated_quote_exported` *(CORE ACTION)* | Báo giá bảo chứng được kết xuất thành công | **Backend tạo xong file PDF, lưu Snapshot DB và trả về HTTP 200 kèm Hash** | **Core Value Event, NSM, Activation, Retention** |
| `deal_deposit_submitted` | Giao dịch được chuyển sang bước đặt cọc chính thức | Khi Sale bấm chuyển hồ sơ báo giá sang bước ráp cọc thành công | Business Impact Metric (Tỷ lệ chuyển đổi giao dịch) |

---

### 2. Hai tiêu chí nghiệm thu bắt buộc (Acceptance Criteria)

#### Tiêu chí 1: Chỉ ghi nhận khi hành vi thực sự hoàn tất (Chống bắn event sớm)
* **Quy tắc:** Event `validated_quote_exported` **chỉ được phép phát đi khi và chỉ khi:**
  1. Python Math Engine đã hoàn tất tính toán dòng tiền không lỗi.
  2. Báo giá đã được gắn mã băm bất biến `snapshot_hash` (SHA-256) và lưu thành công vào cơ sở dữ liệu.
  3. Backend trả về HTTP status code `200 OK` kèm đường dẫn tải tài liệu hoàn chỉnh.
* **Nghiêm cấm:** Tuyệt đối không phát event khi người dùng mới chỉ click vào nút "Xuất báo giá" hoặc khi tiến trình tạo file PDF còn đang quay vòng loading.

#### Tiêu chí 2: Tính tất định & Chống ghi trùng lặp (Idempotency Key)
* **Quy tắc:** Với mỗi cặp định danh duy nhất `{quote_id, session_id}`, hệ thống chỉ ghi nhận **duy nhất 1 event `validated_quote_exported`**.
* **Xử lý ngoại lệ:** Nếu người dùng thực hiện tải lại trang (reload), bấm nút tải lại (retry download), hoặc gặp sự cố chập chờn mạng và gửi lại request trong vòng 10 phút, hệ thống backend phải nhận diện `quote_id` đã tồn tại và không được ghi nhận thêm bất kỳ event nào cho cùng một hành vi xuất báo giá đó.

> **KẾT LUẬN GATE 4B:** VƯỢT QUA. Đủ 6 event dạng `object_action`, 100% event map về metric cụ thể, có 2 Acceptance Criteria chặt chẽ chống gian lận dữ liệu.

---

## 07 — TỰ SOI LỖI & RATIONALE REVISION (GATE 5)

### 1. Bảng đối chiếu 7 câu hỏi tự soi lỗi kinh điển

| Câu hỏi kiểm tra | Trạng thái | Lập luận chứng minh |
| :--- | :---: | :--- |
| 1. Core action không phải thao tác UI hay output hệ thống? | **ĐẠT** | Core action là `validated_quote_exported` (xuất hồ sơ hoàn chỉnh có bảo chứng), không phải "mở app", "click xem" hay "hỏi AI". |
| 2. Activation không phải "xem hướng dẫn" hay "đăng nhập"? | **ĐẠT** | Activation đòi hỏi xuất thành công báo giá đầu tiên trong 48h (`first_validated_quote_exported`). |
| 3. Frequency không cao hơn nhu cầu thật? | **ĐẠT** | Cadence là Weekly (2–5 lần/tuần), không ép Daily thói quen giả tạo. |
| 4. Loop có reason to return ngoài notification? | **ĐẠT** | Reason to return là ví hồ sơ lưu trữ Snapshot và quy trình bắt buộc đối soát khi khách quay lại chốt cọc. |
| 5. Retention không dùng chung một window cho mọi cadence? | **ĐẠT** | Retention đo theo Weekly Bracket, hoàn toàn đồng nhất với nhịp Cadence tuần. |
| 6. Mọi event đều map về một metric? | **ĐẠT** | Cả 6 event trong bảng đều ánh xạ trực tiếp về Activation, NSM, Leading indicators hoặc Retention. |
| 7. Metric nào cũng có event để tính nó? | **ĐẠT** | NSM có `validated_quote_exported` + `policy_conflict_cleared`; Activation có `sales_account_activated`; Retention dùng chung return event. |

---

### 2. Ghi chú điều chỉnh thiết kế (Revision Rationale)

* **Nội dung điều chỉnh:** Ban đầu, nhóm cân nhắc lựa chọn Persona là **Giám đốc Kinh doanh (Sales Director / CCO)** với Core Action là *"Phê duyệt chính sách bán hàng"*. Tuy nhiên, sau khi đối chiếu thực tế nghiệp vụ sàn VLandFuture, quyết định đã được chuyển đổi dứt khoát sang **Nhân viên Kinh doanh Tuyến đầu (Sales Executive)**.
* **Lý do điều chỉnh (Rationale):**
  1. *Tính lặp lại và quy mô dữ liệu:* Giám đốc kinh doanh chỉ duyệt chính sách theo tháng/chiến dịch (nhịp quá thưa để xây dựng Product Loop và tối ưu sản phẩm liên tục). Trong khi đó, Sales Executive tương tác hàng tuần, tạo ra hàng nghìn hồ sơ tính giá mỗi đợt mở bán.
  2. *Nơi sinh ra giá trị thương mại:* Trận địa quyết định thành bại của dự án BĐS diễn ra tại bàn tư vấn giữa Sale và Khách mua nhà. Giải quyết được bài toán tự tin định giá và an toàn chiết khấu cho Sale chính là chìa khóa gốc rễ bảo vệ biên lợi nhuận cho Chủ đầu tư.

---
**NGƯỜI LẬP BỘ CHỈ SỐ**  
*Tạ Việt Cường (02560)*  
*TechLead & Principal System Architect*
