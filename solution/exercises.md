# K4 — Ngày 1: Bài Tập & Phản Ánh
## Khám Phá LLM API | Phiếu Thực Hành

**Thời lượng:** 14h00–18h00
**Cách làm:** Trả lời từng câu ngay sau khi hoàn thành block tương ứng —
đừng để dồn hết về cuối buổi. Thay dòng `*Câu trả lời của bạn*` bằng câu
trả lời thật (chấm tự động sẽ đếm số câu đã trả lời).

---

## Block 1 — API Cơ Bản (trả lời sau Checkpoint 1)

### Câu 1.1 — Độ nhạy của temperature
Gọi `call_openai` với temperature 0.0, 0.7, 1.2 và 1.8 dùng prompt
**"Hãy kể cho tôi một sự thật thú vị về Hà Nội."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi? Ở mức nào phản hồi bắt đầu
kém mạch lạc?** (2–3 câu)
> Qua 4 mức temperature, em nhận thấy: T=0.0: Phản hồi rất an toàn, cứng nhắc. (vd: "Hà Nội là thủ đô của nước Cộng hòa Xã hội chủ nghĩa Việt Nam, nằm ở đồng bằng sông Hồng.")  
> T=0.7: Văn phong tự nhiên và sáng tạo hơn. (vd: "Một sự thật thú vị là cầu Long Biên ở Hà Nội do công ty của kiến trúc sư Gustave Eiffel thiết kế.")  
> T=1.2: Từ ngữ bay bổng, có phần cường điệu. (vd: "Hà Nội ngập chìm trong hương hoa sữa nồng nàn quyện với sắc màu thời gian dĩ vãng rực rỡ.")  
> T=1.8: Văn bản bắt đầu kém mạch lạc và ngữ pháp lỗi nghiêm trọng. (vd: "Hoa sữa xe máy vù vù rồng bay thủ đô nước lóng lánh phố phường bát ngát!")  
> Số temperature càng cao thì AI càng dùng từ ngữ phong phú, nhưng từ mức 1.2 và đặc biệt là 1.8, phản hồi bị suy giảm chất lượng rõ rệt, trở nên kém mạch lạc và lỗi ngữ pháp nặng nề và có khả năng dẫn đến hallucination.

### Câu 1.2 — Chọn temperature cho sản phẩm
**Bạn sẽ đặt temperature bao nhiêu cho trợ lý soạn thảo hợp đồng pháp lý,
và bao nhiêu cho trợ lý viết slogan quảng cáo? Giải thích khác biệt.**
> Đối với trợ lý soạn thảo hợp đồng pháp lý, em sẽ đặt temperature ở mức rất thấp (0.0 - 0.2) vì tính chất công việc đòi hỏi sự chính xác tuyệt đối, nhất quán và không có tính ngẫu nhiên hay bịa đặt. Ngược lại, trợ lý viết slogan quảng cáo cần sự sáng tạo, mới mẻ và đột phá, nên em sẽ đặt temperature cao hơn (0.7 - 0.9) để có được nhiều ý tưởng đa dạng và hấp dẫn.

### Câu 1.3 — Đánh đổi chi phí
Kịch bản: 20.000 người dùng hoạt động mỗi ngày, mỗi người gọi API 2 lần,
mỗi lần trung bình ~500 token đầu ra.

**Ước tính chi phí mỗi ngày của model lớn so với model nhỏ cho workload này
(dựa trên bảng giá trong template). Nêu một trường hợp model lớn xứng đáng
với chi phí và một trường hợp model nhỏ là lựa chọn đúng:**
> Ước tính chi phí mỗi ngày (Giả định bài toán chỉ tính lượng token đầu ra, với 40.000 lượt gọi x 500 token = 20 triệu token): Mô hình lớn (gpt-4o: $0.01/1K token) tiêu tốn 200 USD/ngày. Mô hình nhỏ (gpt-4o-mini: $0.0006/1K token) chỉ tốn 12 USD/ngày.  
**Model lớn xứng đáng:** Khi ứng dụng yêu cầu suy luận phức tạp, phân tích dữ liệu chuyên sâu hoặc lập trình (vd: trợ lý y khoa, viết mã nguồn phức tạp).  
**Model nhỏ là lựa chọn đúng:** Khi thực hiện các tác vụ đơn giản, lặp đi lặp lại như phân loại văn bản, trích xuất thực thể, hoặc chatbot hỗ trợ người dùng có kịch bản cố định.

---

## Block 2 — System Prompt & Token (trả lời sau Checkpoint 2)

### Câu 2.1 — Sức mạnh của persona
Gọi `chat_with_system_prompt` hai lần với cùng câu hỏi
**"Giải thích máy học (machine learning) là gì?"** nhưng hai system prompt
khác nhau:
- "Bạn là một nhà thơ, trả lời mọi thứ bằng hình ảnh ví von, tránh thuật ngữ."
- "Bạn là kỹ sư phần mềm senior, trả lời chính xác, có ví dụ code khi phù hợp."

**Hai phản hồi khác nhau như thế nào (giọng văn, độ dài, mức kỹ thuật)?
Từ đó rút ra system prompt điều khiển được những khía cạnh nào của phản hồi?**
(3–4 câu)
> Phản hồi của "nhà thơ" có giọng văn bay bổng, dùng nhiều phép ẩn dụ và hoàn toàn không có thuật ngữ; trong khi phản hồi của "kỹ sư phần mềm" rất gãy gọn, tập trung vào khái niệm kỹ thuật và thường kèm theo đoạn code minh họa. Từ đó rút ra, system prompt không chỉ định hướng nội dung mà còn điều khiển được giọng điệu (tone), định dạng (format), mức độ chuyên sâu (technical depth), và cả hình thức trình bày của câu trả lời từ mô hình.

### Câu 2.2 — tiktoken vs đếm từ
Chọn một đoạn văn tiếng Việt ~150 từ. So sánh số token theo `count_tokens`
(tiktoken) với ước lượng `số từ / 0.75` mà Part 1 đã dùng.

**Hai con số chênh nhau bao nhiêu phần trăm? Nếu dùng ước lượng thô để dự
toán ngân sách API cho ứng dụng tiếng Việt, bạn sẽ dự toán thiếu hay thừa —
và vì sao?**
> Đo thật với một đoạn văn tiếng Việt có 202 từ:
> - Ước lượng thô (số từ / 0.75): 202 / 0.75 = **~269 token**.
> - Số token thực tế (đo bằng tiktoken): Lên tới **459 token** (với đa số các AI phổ biến hiện nay).
> - Độ chênh lệch: Khoảng **70%**.
> 
> Nếu dùng ước lượng thô, ngân sách dự toán cho ứng dụng tiếng Việt sẽ bị **THIẾU HỤT TRẦM TRỌNG**.
> **Vì sao:** Công thức `số từ / 0.75` được thiết lập dựa trên tiếng Anh. Đối với tiếng Việt, do có nhiều dấu thanh (á, ố, ữ...) và cấu trúc ngôn ngữ khác biệt, hệ thống AI thường không nhận diện được trọn vẹn từ mà phải "băm" một chữ tiếng Việt ra thành nhiều mảnh (token) nhỏ. Do đó, tiếng Việt thực tế tiêu tốn số token cao hơn tiếng Anh rất nhiều, dẫn đến ước lượng thô bị sai lệch nặng.
---

## Block 3 — Streaming & Độ Bền (trả lời sau Checkpoint 3)

### Câu 3.1 — Trải nghiệm người dùng với streaming
**Xét ba ứng dụng: (a) chatbot văn bản, (b) trợ lý giọng nói đọc to phản hồi,
(c) pipeline dịch tài liệu chạy ngầm ban đêm. Ứng dụng nào hưởng lợi nhiều
nhất từ streaming, ứng dụng nào không cần — và tại sao?** (1 đoạn văn)
> Chatbot văn bản (a) và trợ lý giọng nói (b) hưởng lợi nhiều nhất từ streaming (đặc biệt là b) vì nó cho phép hệ thống bắt đầu hiển thị hoặc đọc (TTS) ngay những từ đầu tiên trong khi chờ mô hình sinh ra phần còn lại, giảm thiểu độ trễ ban đầu (Time to First Token) và tăng trải nghiệm theo thời gian thực. Ngược lại, pipeline dịch tài liệu chạy ngầm (c) không cần streaming, vì nó không có người dùng đầu cuối chờ đợi trực tiếp; hệ thống ưu tiên xử lý batch để nhận kết quả hoàn chỉnh lưu vào cơ sở dữ liệu thay vì quan tâm độ trễ của token đầu tiên.

### Câu 3.2 — Vì sao backoff theo cấp số nhân?
**Khi API quá tải và hàng nghìn client cùng retry, exponential backoff giúp
gì so với delay cố định? Tra cứu thêm: kỹ thuật "jitter" (thêm độ trễ ngẫu
nhiên) giải quyết vấn đề gì còn sót lại?**
> Exponential backoff giúp giảm tải đột ngột cho máy chủ API bằng cách giãn cách dần thời gian giữa các lần thử lại, tránh việc hàng nghìn client liên tục "phá" server cùng lúc (Thundering Herd problem) như khi dùng delay cố định. Kỹ thuật "jitter" (thêm độ trễ ngẫu nhiên) giúp giải quyết vấn đề khi nhiều client vô tình bắt đầu đếm lùi backoff cùng một lúc; jitter làm phân tán thời điểm gửi request của chúng, dàn đều tải cho hệ thống phục hồi hiệu quả hơn.

---

## Block 4 — Mini-Project (trả lời sau Checkpoint 4)

### Câu 4.1 — Thiết kế persona
**Viết lại system prompt bạn dùng cho trợ lý của mình. Chỉ ra 2 chỗ trong
prompt mà nếu xóa đi, hành vi trợ lý sẽ thay đổi rõ rệt — và mô tả thay đổi
đó:**
> System prompt: *"Bạn là trợ giảng thân thiện của khóa AI, trả lời ngắn gọn bằng tiếng Việt."*  
> Xóa *"trợ giảng thân thiện của khóa AI"*: Trợ lý sẽ mất ngữ cảnh chuyên môn, có thể trả lời chung chung giống ChatGPT thông thường thay vì tập trung hỗ trợ sát sườn kiến thức của khóa học.  
> Xóa *"trả lời ngắn gọn bằng tiếng Việt"*: Trợ lý có thể sinh ra các đoạn văn rất dài dòng không cần thiết, hoặc phản hồi bằng tiếng Anh, làm giảm tính hiệu quả cho giao diện CLI command line.

### Câu 4.2 — Hạn chế & cải thiện
**Trợ lý của bạn giữ history 4 lượt cuối. Hãy mô tả một tình huống hội thoại
cụ thể mà giới hạn này khiến trợ lý trả lời sai/mất ngữ cảnh, và đề xuất một
cách khắc phục (ví dụ: tóm tắt các lượt cũ, tăng giới hạn có chọn lọc...):**  
> **Tình huống:** Người dùng yêu cầu phân tích một báo cáo dài ở lượt 1. Từ lượt 2 đến 5, người dùng hỏi lan man về các khái niệm khác. Ở lượt 6, người dùng nói "Hãy tóm tắt lại báo cáo lúc nãy". Do giới hạn 4 lượt (từ 2 đến 5), báo cáo ban đầu đã bị xóa khỏi lịch sử, dẫn đến mô hình không hiểu "báo cáo lúc nãy" là gì và trả lời sai.  
> **Cách khắc phục:** Tích hợp cơ chế **tóm tắt bộ nhớ** (memory summarization): thay vì xóa bỏ hoàn toàn, dùng một lệnh gọi LLM nhỏ ngầm tóm tắt nội dung chính của các lượt cũ bị đẩy ra và gắn phần tóm tắt đó vào đầu hội thoại. Hoặc lưu lịch sử dạng Vector Database (RAG) để truy xuất động ngữ cảnh liên quan.

---

## Danh Sách Kiểm Tra Nộp Bài

- [ ] `python grade.py` — xem điểm tự động, mục tiêu ≥ 75/100
- [ ] Cả 4 checkpoint pytest đều pass
- [ ] Tất cả 9 câu trong file này đã được trả lời
- [ ] Đã copy bài làm vào folder `solution/`, push lên GitHub cá nhân và nộp link repo vào vlearn (theo hướng dẫn README)
