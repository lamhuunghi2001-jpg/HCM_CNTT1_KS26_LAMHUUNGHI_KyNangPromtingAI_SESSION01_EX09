# HỌ VÀ TÊN: LÂM HỮU NGHỊ
# LỚP: HCM_CNTT1_KS26_LAMHUUNGHI_KyNangPromtingAI

## Phần 1. Phân tích nguyên nhân AI trả lời sai (ảo giác thông tin)

Khi nhân viên Thu mua hỏi ChatGPT mà không cung cấp hợp đồng MartX, AI không có căn cứ để biết chính xác quy định riêng của công ty. Mô hình có thể dựa vào những mẫu thông tin đã học và dự đoán câu trả lời có vẻ hợp lý theo xác suất, nhưng điều đó không có nghĩa là thông tin đúng với hợp đồng thực tế.

Vì vậy, AI đã tự đưa ra mức phạt 20% và đình chỉ nhập hàng 30 ngày dù hợp đồng không có quy định này. Đây là hiện tượng ảo giác AI (Hallucination): AI tạo ra thông tin nghe có vẻ tự tin, hợp lý nhưng không được tài liệu nguồn xác nhận.

**Nguyên nhân chính:**

- Không có tài liệu hợp đồng để AI đối chiếu.
- AI suy đoán dựa trên kiến thức chung thay vì quy định riêng của MartX.
- Câu trả lời không bị giới hạn bởi yêu cầu chỉ sử dụng thông tin trong tài liệu.

## Phần 2. Cấu trúc Prompt RAG Grounding hoàn chỉnh

Có thể sử dụng Prompt sau để yêu cầu AI trả lời dựa trên đúng nội dung hợp đồng:

### PROMPT

Vai trò: Bạn là trợ lý hỗ trợ nhân viên Thu mua của MartX. Nhiệm vụ của bạn là đọc tài liệu được cung cấp và trả lời câu hỏi chỉ dựa trên nội dung tài liệu đó.

**1. VĂN BẢN HỢP ĐỒNG CHUẨN (CONTEXT)**
<hop_dong>
Hợp đồng MartX quy định: "Phạt 5% giá trị lô bị dập nát và yêu cầu đổi hàng trong 24h".
</hop_dong>


**2. CÂU HỎI NGHIỆP VỤ (QUESTION)**

Nhà cung cấp giao rau bị dập nát trên 10% thì theo hợp đồng MartX sẽ bị xử lý như thế nào? Hãy nêu mức phạt và yêu cầu đổi hàng.

**3. NEGATIVE CONSTRAINT – KHÓA AN TOÀN**

- Chỉ sử dụng thông tin có trong văn bản hợp đồng được cung cấp.
- Không sử dụng kiến thức bên ngoài để tự bổ sung điều khoản.
- Không tự suy đoán hoặc tạo ra mức phạt, thời hạn hay hình thức xử lý không có trong tài liệu.
- Nếu thông tin không có trong văn bản, tuyệt đối trả lời đúng câu: "Không có dữ liệu trong tài liệu".
- Trả lời ngắn gọn, đúng trọng tâm và không thêm thông tin ngoài căn cứ.

Định dạng đầu ra: Trả lời bằng tiếng Việt, nêu rõ mức phạt và yêu cầu đổi hàng. Nếu tài liệu không cung cấp thông tin cần thiết thì sử dụng câu trả lời bắt buộc ở trên.

### KẾT QUẢ MONG ĐỢI

Theo hợp đồng MartX được cung cấp, nhà cung cấp bị phạt 5% giá trị lô bị dập nát và phải đổi hàng trong vòng 24 giờ.

Lưu ý: Điều khoản được cung cấp không nêu rõ ngưỡng rau bị dập nát trên 10%, vì vậy không thể khẳng định ngưỡng này là điều kiện áp dụng mức phạt. Cần kiểm tra thêm hợp đồng đầy đủ để xác nhận.

## Kết luận

Hỏi LLM không kèm tài liệu có thể khiến AI suy đoán theo kiến thức chung và tạo ra thông tin không đúng với quy định riêng của doanh nghiệp. RAG Grounding giúp AI dựa vào tài liệu nguồn khi trả lời, còn Negative Constraint đặt ra giới hạn an toàn: không có thông tin thì phải nói rõ là không có dữ liệu, tuyệt đối không tự suy đoán. Nhờ đó, nhân viên MartX có thể giảm nguy cơ sử dụng thông tin sai khi xử lý nhà cung cấp.
