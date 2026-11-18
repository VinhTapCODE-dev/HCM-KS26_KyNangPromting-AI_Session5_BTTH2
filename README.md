> Quy ước dữ liệu truyền (Data Handoff): chỉ truyền JSON sạch, không kèm câu chào hay giải thích. 
Bước 1 xuất target_audience, pain_points, keywords, tone. Bước 2 xuất headline, lead_summary, sections, cta, keywords, tone. Hai trường tone và keywords được giữ nguyên ở mọi bước.

### PROMPT 1: Nghiên cứu khách hàng và xây dựng danh sách các nỗi đau (pain points) mà sản phẩm giải quyết.

**Context:**

Bạn là chuyên gia nghiên cứu thị trường B2B. Phòng Marketing đang chuẩn bị bài PR chuyên sâu (1000-1500 từ) giới thiệu giải pháp AI Chatbot mới cho doanh nghiệp.

**Request**

Xác định nhóm khách hàng mục tiêu và lập danh sách 5 nỗi đau (pain points) mà sản phẩm giải quyết.

**Explanation:**

- Mỗi pain point gồm: tên, mô tả 1 câu, giải pháp chatbot tương ứng.
- Chỉ nêu nỗi đau có thật của doanh nghiệp, không bịa số liệu.
- Không viết bài, không lập dàn ý ở bước này.

**Action:**

Bước 1: Mô tả khách hàng mục tiêu.
Bước 2: Liệt kê 5 pain points kèm giải pháp.
Bước 3: Đề xuất 5-7 từ khóa SEO chính.

**Tone**

Chuyên nghiệp, tin cậy (ghi vào trường "tone" để các bước sau giữ nguyên).

**Extras:**

CHỈ trả về JSON thuần, không chào hỏi, không giải thích:
```
{"target_audience": "...", "pain_points": [{"name": "...", "description": "...", "solution": "..."}], "keywords": ["..."], "tone": "chuyên nghiệp, tin cậy"}
```
### PROMPT 2: Lập dàn ý (bắt buộc dùng output Prompt 1)

**Context:**

Bạn là biên tập viên nội dung SEO. Dữ liệu đầu vào là output của Prompt 1 (không được tự thêm hoặc bỏ):
[DÁN JSON CỦA PROMPT 1]

**Request**

Lập dàn ý chi tiết cho bài PR 1000-1500 từ về AI Chatbot, bám sát JSON trên.

**Explanation:**

- Mỗi H2/H3 phải tương ứng với một pain point trong JSON.
- Giữ nguyên trường tone và keywords từ Prompt 1.
- Không viết nội dung bài ở bước này, chỉ lập dàn ý.

**Action**:

Bước 1: Đặt Headline thu hút, chứa từ khóa chính.
Bước 2: Viết tóm tắt Lead nêu các pain points.
Bước 3: Lập các mục H2/H3, ghi ý chính và số từ dự kiến (tổng 1000-1500 từ).
Bước 4: Soạn CTA kết bài.

**Tone:**

Chuyên nghiệp, tin cậy, đúng với trường "tone" của Prompt 1.

**Extras:**
CHỈ trả về JSON thuần, không chào hỏi:
```
{"headline": "...", "lead_summary": "...", "sections": [{"h2": "...", "h3": ["..."], "main_points": "...", "word_count": 0}], "cta": "...", "keywords": ["..."], "tone": "..."}
```

### PROMPT 3: Viết bài và tối ưu SEO (bắt buộc dùng output Prompt 2)

**Context:**

Bạn là copywriter PR chuyên nghiệp. Dữ liệu đầu vào là output của Prompt 2 (dàn ý):
[DÁN JSON CỦA PROMPT 2]

**Request:**

Viết hoàn chỉnh bài PR chuẩn SEO dài 1000-1500 từ theo đúng dàn ý, từng phần một.

**Explanation:**

- Viết đúng thứ tự và đúng số từ dự kiến của từng phần, không lặp ý giữa các phần.
- Từ khóa chính xuất hiện ở Headline, Lead và ít nhất 1 tiêu đề H2; từ khóa phụ chèn tự nhiên, không nhồi nhét.
- Không đổi giọng điệu giữa các phần.

**Action:**

Bước 1: Viết Headline (H1) thu hút, chứa từ khóa chính, và Lead hấp dẫn giải quyết pain points.
Bước 2: Viết lần lượt các mục H2/H3 theo dàn ý.
Bước 3: Viết CTA rõ ràng ở cuối bài.

**Tone:**

Chuyên nghiệp, tin cậy, giữ nguyên từ đầu đến cuối bài.

**Extras:**

Trình bày bằng Markdown: # cho Headline, ## cho H2, ### cho H3, CTA in đậm ở cuối.

**Quy tắc xử lý nếu AI bị ngắt quãng (Max Output Tokens), theo khung CREATE**:

Bước 1: Copy chính xác 3-5 từ cuối cùng trước điểm bị ngắt, rồi gửi câu lệnh sau:

**Context:**

Bài PR ở Prompt 3 bị ngắt quãng do đạt giới hạn token. Phần đã viết nằm ngay phía trên.

**Request:**

Viết tiếp NGAY SAU cụm từ: "[3-5 từ cuối]".

**Explanation:**

Không lặp lại nội dung đã viết, không chào hỏi hay giải thích, câu đầu tiên phải nối khớp với cụm từ trên.

**Action:**

Bước 1: Viết tiếp từ đúng điểm ngắt.
Bước 2: Hoàn thành các mục còn lại theo dàn ý.
Bước 3: Kết thúc bằng CTA.

**Tone:**

Chuyên nghiệp, tin cậy, giống phần đã viết.

**Extras:**

Giữ nguyên định dạng Markdow như phần trước.

Bước 2: Nối phần mới vào phần cũ, kiểm tra câu nối liền mạch và không bị lặp.
