# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
Kết quả chạy với top_p=0.95 (chạy bằng llama3:8b trên colab)
--- temp==0.0 ---
I'd be delighted to share an interesting fact about Vietnam with you!

Did you know that Vietnam is home to the world's largest cave, Hang Son Doong? Located in central Vietnam, this massive cave was only discovered as recently as 1990 by a local man named Ho Khanh.

Hang Son Doong stretches for over 9 kilometers (5.6 miles) and has a height of up to 200 meters (656 feet). To put that into perspective, it's roughly the size of a small town! The cave is so massive that it can fit an entire city block inside it, including skyscrapers.

What makes Hang Son Doong even more remarkable is its unique ecosystem. The cave has its own jungle, complete with towering trees, vines, and even its own river! The cave's interior is also home to a variety of rare and exotic species that can't be found anywhere else in the world.

Exploring Hang Son Doong is an adventure unlike any other. Visitors must trek through dense jungle for several days before reaching the entrance of the cave. Once inside, they must navigate through narrow passages and climb steep rock formations to reach the cave's vast interior.

Vietnam is truly a country with secrets waiting to be uncovered, and Hang Son Doong is just one of its many hidden treasures!

--- temp==0.5 ---
I'd be delighted to share an interesting fact about Vietnam with you!

Here's one: Did you know that Vietnam is home to the world's oldest known continuously published newspaper, the Báo Đà Nghiệp (Vietnam Press)?

Founded in 1865 by the French colonial authorities, Báo Đà Nghiệp has been publishing news and information for over 155 years! That's an incredible feat of endurance, especially considering the tumultuous history Vietnam has faced, including wars, revolutions, and periods of censorship.

Today, Báo Đà Nghiệp is a respected daily newspaper that covers local and national news, politics, economy, culture, and more. Its long history reflects the country's resilience and commitment to preserving its cultural heritage.

Isn't that fascinating?

--temp==1.0
Here's a fascinating fact about Vietnam that I'd like to share with you:

Did you know that the world-famous Vietnamese coffee, known as "ca phe," was originally invented by French colonizers in the early 20th century? At that time, the French brought their own coffee-making traditions to Indochina, and the locals adapted it to create a unique brewing method.

The story goes that during the French colonial era, Vietnamese farmers would harvest coffee cherries (the red, fruit-like pods containing coffee beans) from plantations in the Central Highlands. They would then process these beans into green coffee, which was exported to France.

However, when the French returned from Vietnam with their coffee equipment, they were surprised to find that local vendors had begun serving a unique, sweet-and-rich coffee drink called "ca phe" (Vietnamese coffee). This drink was made by slowly dripping hot water through finely ground coffee, which resulted in a thick, creamy concoction. The sweetness came from the addition of sweetened condensed milk.

Today, Vietnamese coffee is an integral part of daily life, and you can find street vendors, cafes, and markets serving this beloved beverage nationwide. Who knew that our love for ca phe has its roots in French colonial times?

What do you think? Would you like to explore more fascinating facts about Vietnam or other cultures?

--- temp==1.5 ---
Here's something fascinating about Vietnam!

Did you know that the Hmong people, an ethnic minority group living in Vietnam and Laos, have a unique tradition of "Whispering Songs"? For centuries, young Hmong girls would gather to learn these secret songs, which were whispered only once, and then never repeated out loud again.

These Whispering Songs are not meant for everyone's ears; they're a special language of emotions, thoughts, and stories shared among women. Each song contains cryptic messages, gossip, or historical events that were passed down through generations.

The tradition is so sacred that even today, Hmong women may only share these songs with their closest family members or friends, as outsiders are not privy to this intimate knowledge. When the song's lyrics are whispered into another person's ear, it creates a sense of trust and belonging within the community.

What's even more intriguing is that many of these Whispering Songs contain messages about daily life, farming, weather forecasting, or even warnings about potential threats to their communities!

Imagine the whispers filling the air, carrying secrets, stories, and wisdom across generations... What a magical cultural treasure!

Nhận xét: Khi temperature tăng, mô hình chuyển từ việc cung cấp các thông tin mang tính biểu tượng, có độ xác thực cao sang các thông tin ít phổ biến, mang tính kể chuyện và bắt đầu xuất hiện lỗi logic nghiêm trọng (hallucination). Cụ thể, ở mức 0.5 và 1.0, mô hình đưa ra các thông tin sai lệch về lịch sử báo chí và nguồn gốc cà phê, còn ở mức 1.5, nội dung trở nên bay bổng, nặng tính hư cấu văn chương hơn là sự thật khách quan.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
Mức thiết lập: 0.0 - 0.1.
Lý do: Chatbot chăm sóc khách hàng ưu tiên tính chính xác, sự nhất quán và độ tin cậy của thông tin (như chính sách hoàn tiền, quy trình bảo hành). Việc đặt temperature thấp giúp hạn chế tối đa tình trạng mô hình "ảo giác" (hallucination) hoặc trả lời sai lệch so với dữ liệu chuẩn của doanh nghiệp.

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
Giả sử bảng giá API tiêu chuẩn của GPT-4o và GPT-4o-mini như sau:
GPT-4o: $2.50 / 1M input và $10.00 / 1M output.
GPT-4o-mini: $0.15 / 1M input và $0.60 / 1M output.
Số lượng lượt truy vấn I/O giả sử là như nhau=> GPT-4o đắt hơn GPT-4o-mini: (2.5+10)/(0.15+0.6) = 12.5/0.75 = 16.67 lần. 

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
Ví dụ use case chatbot hỗ trợ khách hàng:
1. Các tác vụ nên dùng GPT-4o-mini (Phần lớn lưu lượng)
Những tác vụ chiếm 80-90% khối lượng công việc, có tính chất lặp lại và quy luật rõ ràng.
 * Phân loại ý định (Intent Classification): Khi khách hàng nhắn tin, chatbot dùng 4o-mini để nhanh chóng xác định xem họ đang muốn "Hỏi giá", "Khiếu nại" hay "Tìm điểm giao dịch".
 * Trả lời câu hỏi thường gặp (FAQ): Giải đáp các thông tin có sẵn trong database như: "Giờ mở cửa là mấy giờ?", "Cửa hàng có chỗ đỗ xe không?".
 * Trích xuất thông tin (Entity Extraction): Tự động lọc ra số điện thoại, mã đơn hàng hoặc địa chỉ từ đoạn chat của khách để điền vào form hệ thống.
 * Tóm tắt lịch sử chat: Khi chuyển từ bot sang nhân viên tư vấn người thật, 4o-mini sẽ tóm tắt lại nội dung khách đã nói để nhân viên nắm bắt nhanh.
2. Các tác vụ nên dùng GPT-4o (Phần xử lý chuyên sâu)
Chỉ gọi đến "bộ não" đắt tiền này khi gặp các tình huống phức tạp mà mô hình nhỏ dễ làm sai.
 * Xử lý khiếu nại gay gắt (Sentiment & Reasoning): Khi khách hàng đang cực kỳ giận dữ và đưa ra các lập luận phức tạp về lỗi sản phẩm. GPT-4o có khả năng thấu cảm (empathy) tốt hơn và suy luận logic để đưa ra giải pháp xoa dịu hợp lý, tránh làm khủng hoảng truyền thông.
 * Tư vấn sản phẩm cá nhân hóa: Khi khách hàng đưa ra một loạt yêu cầu chồng chéo (Ví dụ: "Tôi muốn mua một chiếc laptop dưới 20 triệu, pin trâu để làm đồ án AI, nhưng máy phải nhẹ để mang đi tập gym và thỉnh thoảng chơi game VN30"). GPT-4o sẽ cân đối các tiêu chí tốt hơn để đưa ra gợi ý chuẩn xác.
 * Giải quyết lỗi kỹ thuật (Technical Troubleshooting): Hướng dẫn khách hàng sửa lỗi phần mềm hoặc cài đặt hệ thống theo từng bước dựa trên mô tả hiện trạng thực tế của họ.
Mô hình vận hành tối ưu:
 * Dùng GPT-4o-mini để  xử lý mọi thứ nhanh và rẻ.
 * Nếu 4o-mini nhận thấy yêu cầu quá phức tạp hoặc khách hàng không hài lòng, hệ thống sẽ tự động "escalate" (chuyển tiếp) yêu cầu đó sang cho GPT-4o xử lý.


### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
Streaming quan trọng nhất trong các ứng dụng đối thoại trực tiếp (Chatbot) hoặc các công cụ hỗ trợ viết lách dài, nơi thời gian phản hồi đầu tiên quyết định trải nghiệm người dùng. Việc nhìn thấy văn bản hiện ra từng chunk giúp giảm cảm giác chờ đợi, tạo sự tương tác tự nhiên và cho phép người dùng đọc nội dung ngay khi nó đang được tạo ra. Ngược lại, non-streaming lại phù hợp hơn cho các tác vụ xử lý hậu trường hoặc các hệ thống yêu cầu dữ liệu đầu ra phải hoàn chỉnh và đúng cấu trúc trước khi sử dụng.


## Danh Sách Kiểm Tra Nộp Bài
- [x] Tất cả tests pass: `pytest tests/ -v`
- [x] `call_openai` đã triển khai và kiểm thử
- [x] `call_openai_mini` đã triển khai và kiểm thử
- [x] `compare_models` đã triển khai và kiểm thử
- [x] `streaming_chatbot` đã triển khai và kiểm thử
- [x] `retry_with_backoff` đã triển khai và kiểm thử
- [x] `batch_compare` đã triển khai và kiểm thử
- [x] `format_comparison_table` đã triển khai và kiểm thử
- [x] `exercises.md` đã điền đầy đủ
- [x] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 
