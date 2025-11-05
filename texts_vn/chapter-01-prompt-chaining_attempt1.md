# Chương 1: Chuỗi Lời Nhắc (Prompt Chaining)

# Tổng quan về mẫu Chuỗi Lời Nhắc

Chuỗi lời nhắc, đôi khi được gọi là mẫu Pipeline, đại diện cho một mô hình mạnh mẽ để xử lý các tác vụ phức tạp khi tận dụng các mô hình ngôn ngữ lớn (LLM). Thay vì mong đợi một LLM giải quyết một vấn đề phức tạp trong một bước duy nhất, nguyên khối, chuỗi lời nhắc ủng hộ chiến lược chia để trị. Ý tưởng cốt lõi là chia nhỏ vấn đề ban đầu, khó khăn thành một chuỗi các vấn đề phụ nhỏ hơn, dễ quản lý hơn. Mỗi vấn đề phụ được giải quyết riêng lẻ thông qua một lời nhắc được thiết kế đặc biệt, và đầu ra được tạo ra từ một lời nhắc được đưa một cách chiến lược làm đầu vào cho lời nhắc tiếp theo trong chuỗi.

Kỹ thuật xử lý tuần tự này vốn dĩ đưa tính mô-đun và rõ ràng vào tương tác với LLM. Bằng cách phân tách một tác vụ phức tạp, việc hiểu và gỡ lỗi từng bước riêng lẻ trở nên dễ dàng hơn, làm cho quy trình tổng thể trở nên mạnh mẽ và dễ hiểu hơn. Mỗi bước trong chuỗi có thể được chế tạo và tối ưu hóa một cách tỉ mỉ để tập trung vào một khía cạnh cụ thể của vấn đề lớn hơn, dẫn đến các đầu ra chính xác và tập trung hơn.

Đầu ra của một bước hoạt động như đầu vào cho bước tiếp theo là rất quan trọng. Việc truyền thông tin này thiết lập một chuỗi phụ thuộc, do đó có tên gọi, nơi ngữ cảnh và kết quả của các hoạt động trước đó hướng dẫn quá trình xử lý tiếp theo. Điều này cho phép LLM xây dựng dựa trên công việc trước đó của nó, tinh chỉnh sự hiểu biết của nó và dần dần tiến gần hơn đến giải pháp mong muốn.

Hơn nữa, chuỗi lời nhắc không chỉ là việc chia nhỏ vấn đề; nó còn cho phép tích hợp kiến thức và công cụ bên ngoài. Ở mỗi bước, LLM có thể được hướng dẫn để tương tác với các hệ thống, API hoặc cơ sở dữ liệu bên ngoài, làm phong phú kiến thức và khả năng của nó vượt ra ngoài dữ liệu đào tạo nội bộ của nó. Khả năng này mở rộng đáng kể tiềm năng của LLM, cho phép chúng hoạt động không chỉ như các mô hình biệt lập mà còn như các thành phần không thể thiếu của các hệ thống rộng lớn hơn, thông minh hơn.

Tầm quan trọng của chuỗi lời nhắc mở rộng ra ngoài việc giải quyết vấn đề đơn giản. Nó đóng vai trò là một kỹ thuật nền tảng để xây dựng các tác nhân AI tinh vi. Các tác nhân này có thể sử dụng chuỗi lời nhắc để tự động lập kế hoạch, suy luận và hành động trong các môi trường động. Bằng cách cấu trúc chiến lược chuỗi lời nhắc, một tác nhân có thể tham gia vào các tác vụ yêu cầu suy luận nhiều bước, lập kế hoạch và ra quyết định. Các quy trình làm việc của tác nhân như vậy có thể bắt chước các quá trình tư duy của con người một cách chặt chẽ hơn, cho phép tương tác tự nhiên và hiệu quả hơn với các miền và hệ thống phức tạp.

**Hạn chế của các lời nhắc đơn lẻ:** Đối với các tác vụ đa diện, việc sử dụng một lời nhắc phức tạp, đơn lẻ cho một LLM có thể không hiệu quả, khiến mô hình gặp khó khăn với các ràng buộc và hướng dẫn, có khả năng dẫn đến việc bỏ qua hướng dẫn nơi các phần của lời nhắc bị bỏ qua, trôi dạt ngữ cảnh nơi mô hình mất dấu ngữ cảnh ban đầu, lan truyền lỗi nơi các lỗi ban đầu khuếch đại, các lời nhắc yêu cầu cửa sổ ngữ cảnh dài hơn nơi mô hình nhận được thông tin không đủ để phản hồi và ảo giác nơi tải nhận thức làm tăng khả năng thông tin không chính xác. Ví dụ, một truy vấn yêu cầu phân tích báo cáo nghiên cứu thị trường, tóm tắt các phát hiện, xác định xu hướng với các điểm dữ liệu và soạn thảo một email có nguy cơ thất bại vì mô hình có thể tóm tắt tốt nhưng không trích xuất dữ liệu hoặc soạn thảo email đúng cách.

**Độ tin cậy nâng cao thông qua phân tách tuần tự:** Chuỗi lời nhắc giải quyết những thách thức này bằng cách chia nhỏ tác vụ phức tạp thành một quy trình làm việc tuần tự, tập trung, giúp cải thiện đáng kể độ tin cậy và kiểm soát. Với ví dụ trên, một cách tiếp cận theo đường ống hoặc chuỗi có thể được mô tả như sau:

1. Lời nhắc ban đầu (Tóm tắt): "Tóm tắt các phát hiện chính của báo cáo nghiên cứu thị trường sau: [văn bản]." Trọng tâm duy nhất của mô hình là tóm tắt, tăng độ chính xác của bước ban đầu này.
2. Lời nhắc thứ hai (Xác định xu hướng): "Sử dụng bản tóm tắt, xác định ba xu hướng mới nổi hàng đầu và trích xuất các điểm dữ liệu cụ thể hỗ trợ mỗi xu hướng: [đầu ra từ bước 1]." Lời nhắc này hiện bị ràng buộc hơn và xây dựng trực tiếp dựa trên một đầu ra đã được xác thực.
3. Lời nhắc thứ ba (Soạn email): "Soạn một email ngắn gọn gửi cho nhóm tiếp thị nêu rõ các xu hướng sau và dữ liệu hỗ trợ của chúng: [đầu ra từ bước 2]."

Việc phân tách này cho phép kiểm soát chi tiết hơn đối với quy trình. Mỗi bước đơn giản hơn và ít mơ hồ hơn, giúp giảm tải nhận thức cho mô hình và dẫn đến đầu ra cuối cùng chính xác và đáng tin cậy hơn. Tính mô-đun này tương tự như một đường ống tính toán nơi mỗi hàm thực hiện một hoạt động cụ thể trước khi chuyển kết quả của nó cho hàm tiếp theo. Để đảm bảo phản hồi chính xác cho mỗi tác vụ cụ thể, mô hình có thể được gán một vai trò riêng biệt ở mỗi giai đoạn. Ví dụ, trong kịch bản đã cho, lời nhắc ban đầu có thể được chỉ định là "Nhà phân tích thị trường," lời nhắc tiếp theo là "Nhà phân tích thương mại," và lời nhắc thứ ba là "Người viết tài liệu chuyên nghiệp," v.v.

**Vai trò của đầu ra có cấu trúc:** Độ tin cậy của một chuỗi lời nhắc phụ thuộc rất nhiều vào tính toàn vẹn của dữ liệu được truyền giữa các bước. Nếu đầu ra của một lời nhắc mơ hồ hoặc được định dạng kém, lời nhắc tiếp theo có thể thất bại do đầu vào bị lỗi. Để giảm thiểu điều này, việc chỉ định một định dạng đầu ra có cấu trúc, chẳng hạn như JSON hoặc XML, là rất quan trọng.

Ví dụ, đầu ra từ bước xác định xu hướng có thể được định dạng dưới dạng đối tượng JSON:

| `{ "trends": [ { "trend_name": "Cá nhân hóa được hỗ trợ bởi AI", "supporting_data": "73% người tiêu dùng thích kinh doanh với các thương hiệu sử dụng thông tin cá nhân để làm cho trải nghiệm mua sắm của họ phù hợp hơn." }, { "trend_name": "Thương hiệu bền vững và đạo đức", "supporting_data": "Doanh số bán các sản phẩm có tuyên bố liên quan đến ESG đã tăng 28% trong năm năm qua, so với 20% đối với các sản phẩm không có." } ] }` |
| :---- |

Định dạng có cấu trúc này đảm bảo rằng dữ liệu có thể đọc được bằng máy và có thể được phân tích cú pháp chính xác và chèn vào lời nhắc tiếp theo mà không có sự mơ hồ. Thực hành này giảm thiểu lỗi có thể phát sinh từ việc diễn giải ngôn ngữ tự nhiên và là một thành phần quan trọng trong việc xây dựng các hệ thống dựa trên LLM nhiều bước, mạnh mẽ.

# Các ứng dụng thực tế & Trường hợp sử dụng

Chuỗi lời nhắc là một mẫu linh hoạt có thể áp dụng trong nhiều tình huống khi xây dựng các hệ thống tác nhân. Tiện ích cốt lõi của nó nằm ở việc chia nhỏ các vấn đề phức tạp thành các bước tuần tự, dễ quản lý. Dưới đây là một số ứng dụng và trường hợp sử dụng thực tế:

**1. Quy trình làm việc xử lý thông tin:** Nhiều tác vụ liên quan đến việc xử lý thông tin thô thông qua nhiều phép biến đổi. Ví dụ, tóm tắt một tài liệu, trích xuất các thực thể chính, và sau đó sử dụng các thực thể đó để truy vấn cơ sở dữ liệu hoặc tạo báo cáo. Một chuỗi lời nhắc có thể trông như sau:

* Lời nhắc 1: Trích xuất nội dung văn bản từ một URL hoặc tài liệu đã cho.
* Lời nhắc 2: Tóm tắt văn bản đã được làm sạch.
* Lời nhắc 3: Trích xuất các thực thể cụ thể (ví dụ: tên, ngày, địa điểm) từ bản tóm tắt hoặc văn bản gốc.
* Lời nhắc 4: Sử dụng các thực thể để tìm kiếm cơ sở kiến thức nội bộ.
* Lời nhắc 5: Tạo báo cáo cuối cùng kết hợp bản tóm tắt, các thực thể và kết quả tìm kiếm.

Phương pháp này được áp dụng trong các lĩnh vực như phân tích nội dung tự động, phát triển trợ lý nghiên cứu do AI điều khiển và tạo báo cáo phức tạp.

**2. Trả lời truy vấn phức tạp:** Trả lời các câu hỏi phức tạp yêu cầu nhiều bước suy luận hoặc truy xuất thông tin là một trường hợp sử dụng chính. Ví dụ: "Nguyên nhân chính của sự sụp đổ thị trường chứng khoán năm 1929 là gì, và chính sách của chính phủ đã phản ứng như thế nào?"

* Lời nhắc 1: Xác định các câu hỏi phụ cốt lõi trong truy vấn của người dùng (nguyên nhân sụp đổ, phản ứng của chính phủ).
* Lời nhắc 2: Nghiên cứu hoặc truy xuất thông tin cụ thể về nguyên nhân của sự sụp đổ năm 1929.
* Lời nhắc 3: Nghiên cứu hoặc truy xuất thông tin cụ thể về phản ứng chính sách của chính phủ đối với sự sụp đổ thị trường chứng khoán năm 1929.
* Lời nhắc 4: Tổng hợp thông tin từ bước 2 và 3 thành một câu trả lời mạch lạc cho truy vấn ban đầu.

Phương pháp xử lý tuần tự này là không thể thiếu để phát triển các hệ thống AI có khả năng suy luận nhiều bước và tổng hợp thông tin. Các hệ thống như vậy được yêu cầu khi một truy vấn không thể được trả lời từ một điểm dữ liệu duy nhất mà thay vào đó đòi hỏi một loạt các bước logic hoặc tích hợp thông tin từ các nguồn đa dạng.

Ví dụ, một tác nhân nghiên cứu tự động được thiết kế để tạo một báo cáo toàn diện về một chủ đề cụ thể thực hiện một quy trình làm việc tính toán lai. Ban đầu, hệ thống truy xuất nhiều bài viết liên quan. Nhiệm vụ tiếp theo là trích xuất thông tin chính từ mỗi bài viết có thể được thực hiện đồng thời cho mỗi nguồn. Giai đoạn này rất phù hợp cho xử lý song song, nơi các tác vụ phụ độc lập được chạy đồng thời để tối đa hóa hiệu quả.

Huy nhiên, một khi các trích xuất riêng lẻ hoàn tất, quá trình này trở nên tuần tự một cách cố hữu. Hệ thống phải thu thập dữ liệu đã trích xuất, sau đó tổng hợp nó thành một bản nháp mạch lạc, và cuối cùng xem xét và tinh chỉnh bản nháp này để tạo ra một báo cáo cuối cùng. Mỗi giai đoạn sau này phụ thuộc logic vào việc hoàn thành thành công giai đoạn trước đó. Đây là nơi chuỗi lời nhắc được áp dụng: dữ liệu đã thu thập đóng vai trò là đầu vào cho lời nhắc tổng hợp, và văn bản tổng hợp kết quả trở thành đầu vào cho lời nhắc xem xét cuối cùng. Do đó, các hoạt động phức tạp thường kết hợp xử lý song song để thu thập dữ liệu độc lập với chuỗi lời nhắc cho các bước tổng hợp và tinh chỉnh phụ thuộc.

**3. Trích xuất và chuyển đổi dữ liệu:** Việc chuyển đổi văn bản không có cấu trúc thành định dạng có cấu trúc thường đạt được thông qua một quy trình lặp đi lặp lại, yêu cầu các sửa đổi tuần tự để cải thiện độ chính xác và hoàn chỉnh của đầu ra.

* Lời nhắc 1: Cố gắng trích xuất các trường cụ thể (ví dụ: tên, địa chỉ, số tiền) từ tài liệu hóa đơn.
* Xử lý: Kiểm tra xem tất cả các trường bắt buộc đã được trích xuất chưa và liệu chúng có đáp ứng các yêu cầu định dạng không.
* Lời nhắc 2 (Có điều kiện): Nếu các trường bị thiếu hoặc bị định dạng sai, hãy tạo một lời nhắc mới yêu cầu mô hình cụ thể tìm thông tin bị thiếu/định dạng sai, có thể cung cấp ngữ cảnh từ lần thử thất bại.
* Xử lý: Xác thực lại kết quả. Lặp lại nếu cần.
* Đầu ra: Cung cấp dữ liệu có cấu trúc đã được trích xuất, xác thực.

Phương pháp xử lý tuần tự này đặc biệt áp dụng cho việc trích xuất và phân tích dữ liệu từ các nguồn không có cấu trúc như biểu mẫu, hóa đơn hoặc email. Ví dụ, giải quyết các vấn đề Nhận dạng ký tự quang học (OCR) phức tạp, chẳng hạn như xử lý biểu mẫu PDF, được xử lý hiệu quả hơn thông qua cách tiếp cận phân tách, nhiều bước.

Ban đầu, một mô hình ngôn ngữ lớn được sử dụng để thực hiện trích xuất văn bản chính từ hình ảnh tài liệu. Sau đó, mô hình xử lý đầu ra thô để chuẩn hóa dữ liệu, một bước mà nó có thể chuyển đổi văn bản số, chẳng hạn như "một nghìn không trăm năm mươi," thành giá trị số tương đương, 1050. Một thách thức đáng kể đối với LLM là thực hiện các phép tính toán học chính xác. Do đó, trong một bước tiếp theo, hệ thống có thể ủy quyền bất kỳ phép toán số học nào cần thiết cho một công cụ máy tính bên ngoài. LLM xác định phép tính cần thiết, đưa các số đã chuẩn hóa vào công cụ, và sau đó kết hợp kết quả chính xác. Chuỗi tuần tự trích xuất văn bản, chuẩn hóa dữ liệu và sử dụng công cụ bên ngoài này đạt được kết quả cuối cùng, chính xác mà thường khó có thể đạt được một cách đáng tin cậy từ một truy vấn LLM duy nhất.

**4. Quy trình làm việc tạo nội dung:** Việc tạo nội dung phức tạp là một tác vụ thủ tục thường được phân tách thành các giai đoạn riêng biệt, bao gồm ý tưởng ban đầu, phác thảo cấu trúc, soạn thảo và sửa đổi sau đó.

* Lời nhắc 1: Tạo 5 ý tưởng chủ đề dựa trên sở thích chung của người dùng.
* Xử lý: Cho phép người dùng chọn một ý tưởng hoặc tự động chọn ý tưởng tốt nhất.
* Lời nhắc 2: Dựa trên chủ đề đã chọn, tạo một dàn ý chi tiết.
* Lời nhắc 3: Viết một phần bản nháp dựa trên điểm đầu tiên trong dàn ý.
* Lời nhắc 4: Viết một phần bản nháp dựa trên điểm thứ hai trong dàn ý, cung cấp phần trước đó để làm ngữ cảnh. Tiếp tục làm như vậy cho tất cả các điểm trong dàn ý.
* Lời nhắc 5: Xem xét và tinh chỉnh bản nháp hoàn chỉnh để đảm bảo tính mạch lạc, giọng điệu và ngữ pháp.

Phương pháp này được sử dụng cho một loạt các tác vụ tạo ngôn ngữ tự nhiên, bao gồm việc tự động tạo ra các câu chuyện sáng tạo, tài liệu kỹ thuật và các dạng nội dung văn bản có cấu trúc khác.

**5. Tác nhân đàm thoại có trạng thái:** Mặc dù các kiến trúc quản lý trạng thái toàn diện sử dụng các phương pháp phức tạp hơn liên kết tuần tự, chuỗi lời nhắc cung cấp một cơ chế nền tảng để duy trì tính liên tục của cuộc trò chuyện. Kỹ thuật này duy trì ngữ cảnh bằng cách xây dựng mỗi lượt trò chuyện như một lời nhắc mới kết hợp một cách có hệ thống thông tin hoặc các thực thể được trích xuất từ các tương tác trước đó trong chuỗi đối thoại.

* Lời nhắc 1: Xử lý Phát ngôn của người dùng 1, xác định ý định và các thực thể chính.
* Xử lý: Cập nhật trạng thái cuộc trò chuyện với ý định và các thực thể.
* Lời nhắc 2: Dựa trên trạng thái hiện tại, tạo phản hồi và/hoặc xác định thông tin cần thiết tiếp theo.
* Lặp lại cho các lượt tiếp theo, với mỗi phát ngôn mới của người dùng bắt đầu một chuỗi tận dụng lịch sử cuộc trò chuyện tích lũy (trạng thái).

Nguyên tắc này là nền tảng cho sự phát triển của các tác nhân đàm thoại, cho phép chúng duy trì ngữ cảnh và tính mạch lạc trong các cuộc đối thoại nhiều lượt, kéo dài. Bằng cách bảo toàn lịch sử cuộc trò chuyện, hệ thống có thể hiểu và phản hồi thích hợp với các đầu vào của người dùng phụ thuộc vào thông tin đã trao đổi trước đó.

**6. Tạo và tinh chỉnh mã:** Việc tạo mã chức năng thường là một quy trình nhiều giai đoạn, yêu cầu một vấn đề phải được phân tách thành một chuỗi các hoạt động logic rời rạc được thực hiện dần dần.

* Lời nhắc 1: Hiểu yêu cầu của người dùng về một hàm mã. Tạo mã giả hoặc dàn ý.
* Lời nhắc 2: Viết bản nháp mã ban đầu dựa trên dàn ý.
* Lời nhắc 3: Xác định các lỗi tiềm ẩn hoặc các lĩnh vực cần cải thiện trong mã (có thể sử dụng công cụ phân tích tĩnh hoặc một lệnh gọi LLM khác).
* Lời nhắc 4: Viết lại hoặc tinh chỉnh mã dựa trên các vấn đề đã xác định.
* Lời nhắc 5: Thêm tài liệu hoặc trường hợp thử nghiệm.

Trong các ứng dụng như phát triển phần mềm được hỗ trợ bởi AI, tiện ích của chuỗi lời nhắc bắt nguồn từ khả năng phân tách các tác vụ mã hóa phức tạp thành một loạt các vấn đề phụ có thể quản lý được. Cấu trúc mô-đun này làm giảm độ phức tạp hoạt động cho mô hình ngôn ngữ lớn ở mỗi bước. Quan trọng là, cách tiếp cận này cũng cho phép chèn logic xác định giữa các lệnh gọi mô hình, cho phép xử lý dữ liệu trung gian, xác thực đầu ra và phân nhánh có điều kiện trong quy trình làm việc. Bằng phương pháp này, một yêu cầu đa diện duy nhất mà nếu không có thể dẫn đến kết quả không đáng tin cậy hoặc không đầy đủ được chuyển đổi thành một chuỗi hoạt động có cấu trúc được quản lý bởi một khung thực thi cơ bản.

**7. Suy luận đa phương thức và nhiều bước:** Phân tích các tập dữ liệu với các phương thức đa dạng đòi hỏi phải chia nhỏ vấn đề thành các tác vụ dựa trên lời nhắc nhỏ hơn. Ví dụ, diễn giải một hình ảnh chứa một bức ảnh với văn bản nhúng, nhãn làm nổi bật các phân đoạn văn bản cụ thể và dữ liệu dạng bảng giải thích từng nhãn, yêu cầu một cách tiếp cận như vậy.

* Lời nhắc 1: Trích xuất và hiểu văn bản từ yêu cầu hình ảnh của người dùng.
* Lời nhắc 2: Liên kết văn bản hình ảnh đã trích xuất với các nhãn tương ứng của nó.
* Lời nhắc 3: Diễn giải thông tin đã thu thập bằng cách sử dụng một bảng để xác định đầu ra cần thiết.

# Ví dụ mã thực hành

Việc triển khai chuỗi lời nhắc bao gồm từ các lệnh gọi hàm tuần tự trực tiếp trong một tập lệnh đến việc sử dụng các khung chuyên biệt được thiết kế để quản lý luồng điều khiển, trạng thái và tích hợp thành phần. Các khung như LangChain, LangGraph, Crew AI và Google Agent Development Kit (ADK) cung cấp các môi trường có cấu trúc để xây dựng và thực thi các quy trình nhiều bước này, điều này đặc biệt thuận lợi cho các kiến trúc phức tạp.

Với mục đích minh họa, LangChain và LangGraph là những lựa chọn phù hợp vì các API cốt lõi của chúng được thiết kế rõ ràng để tạo chuỗi và đồ thị các hoạt động. LangChain cung cấp các trừu tượng cơ bản cho các chuỗi tuyến tính, trong khi LangGraph mở rộng các khả năng này để hỗ trợ các phép tính có trạng thái và theo chu kỳ, cần thiết để triển khai các hành vi tác nhân tinh vi hơn. Ví dụ này sẽ tập trung vào một chuỗi tuyến tính cơ bản.

Đoạn mã sau triển khai một chuỗi lời nhắc hai bước hoạt động như một đường ống xử lý dữ liệu. Giai đoạn ban đầu được thiết kế để phân tích văn bản không có cấu trúc và trích xuất thông tin cụ thể. Giai đoạn tiếp theo sau đó nhận đầu ra đã trích xuất này và chuyển đổi nó thành định dạng dữ liệu có cấu trúc.

Để tái tạo quy trình này, trước tiên phải cài đặt các thư viện cần thiết. Điều này có thể được thực hiện bằng lệnh sau:

| `pip install langchain langchain-community langchain-openai langgraph` |
| :---- |

Lưu ý rằng langchain-openai có thể được thay thế bằng gói thích hợp cho một nhà cung cấp mô hình khác. Sau đó, môi trường thực thi phải được cấu hình với các thông tin xác thực API cần thiết cho nhà cung cấp mô hình ngôn ngữ đã chọn, chẳng hạn như OpenAI, Google Gemini hoặc Anthropic.

| `import os from langchain_openai import ChatOpenAI from langchain_core.prompts import ChatPromptTemplate from langchain_core.output_parsers import StrOutputParser # Để bảo mật tốt hơn, tải các biến môi trường từ tệp .env # from dotenv import load_dotenv # load_dotenv() # Đảm bảo OPENAI_API_KEY của bạn được đặt trong tệp .env # Khởi tạo Mô hình ngôn ngữ (nên sử dụng ChatOpenAI) llm = ChatOpenAI(temperature=0) # --- Lời nhắc 1: Trích xuất thông tin --- prompt_extract = ChatPromptTemplate.from_template( "Trích xuất các thông số kỹ thuật từ văn bản sau:

{text_input}" ) # --- Lời nhắc 2: Chuyển đổi sang JSON --- prompt_transform = ChatPromptTemplate.from_template( "Chuyển đổi các thông số kỹ thuật sau thành một đối tượng JSON với 'cpu', 'memory', và 'storage' làm khóa:

{specifications}" ) # --- Xây dựng chuỗi bằng LCEL --- # StrOutputParser() chuyển đổi đầu ra tin nhắn của LLM thành một chuỗi đơn giản. extraction_chain = prompt_extract | llm | StrOutputParser() # Chuỗi đầy đủ chuyển đầu ra của chuỗi trích xuất vào biến 'specifications' # cho lời nhắc chuyển đổi. full_chain = ( {"specifications": extraction_chain} | prompt_transform | llm | StrOutputParser() ) # --- Chạy chuỗi --- input_text = "Mẫu máy tính xách tay mới có bộ xử lý octa-core 3.5 GHz, 16GB RAM và 1TB NVMe SSD." # Thực thi chuỗi với từ điển văn bản đầu vào. final_result = full_chain.invoke({"text_input": input_text}) print("\n--- Đầu ra JSON cuối cùng ---") print(final_result)` |
| :---- |

Đoạn mã Python này minh họa cách sử dụng thư viện LangChain để xử lý văn bản. Nó sử dụng hai lời nhắc riêng biệt: một để trích xuất các thông số kỹ thuật từ một chuỗi đầu vào và một lời nhắc khác để định dạng các thông số kỹ thuật này thành một đối tượng JSON. Mô hình ChatOpenAI được sử dụng cho các tương tác mô hình ngôn ngữ, và StrOutputParser đảm bảo đầu ra ở định dạng chuỗi có thể sử dụng được. Ngôn ngữ biểu thức LangChain (LCEL) được sử dụng để liên kết các lời nhắc này và mô hình ngôn ngữ một cách thanh lịch. Chuỗi đầu tiên, extraction_chain, trích xuất các thông số kỹ thuật. full_chain sau đó lấy đầu ra của quá trình trích xuất và sử dụng nó làm đầu vào cho lời nhắc chuyển đổi. Một văn bản đầu vào mẫu mô tả một máy tính xách tay được cung cấp. full_chain được gọi với văn bản này, xử lý nó qua cả hai bước. Kết quả cuối cùng, một chuỗi JSON chứa các thông số kỹ thuật đã được trích xuất và định dạng, sau đó được in ra.

# Kỹ thuật ngữ cảnh và Kỹ thuật lời nhắc

Kỹ thuật ngữ cảnh (xem Hình 1) là một ngành có hệ thống về thiết kế, xây dựng và cung cấp một môi trường thông tin hoàn chỉnh cho một mô hình AI trước khi tạo mã thông báo. Phương pháp này khẳng định rằng chất lượng đầu ra của mô hình ít phụ thuộc vào kiến trúc của mô hình mà phụ thuộc nhiều hơn vào sự phong phú của ngữ cảnh được cung cấp.

<figure>
<img style="display: block; margin: auto; center" src="../imgs/fig.1.png" alt="Kỹ thuật ngữ cảnh là ngành xây dựng một môi trường thông tin phong phú, toàn diện cho AI, vì chất lượng của ngữ cảnh này là yếu tố chính giúp đạt được hiệu suất tác nhân nâng cao">
<figcaption>Hình 1: Kỹ thuật ngữ cảnh là ngành xây dựng một môi trường thông tin phong phú, toàn diện cho AI, vì chất lượng của ngữ cảnh này là yếu tố chính giúp đạt được hiệu suất tác nhân nâng cao</figcaption>
</figure>

Nó đại diện cho một sự phát triển đáng kể từ kỹ thuật lời nhắc truyền thống, chủ yếu tập trung vào việc tối ưu hóa cách diễn đạt truy vấn tức thì của người dùng. Kỹ thuật ngữ cảnh mở rộng phạm vi này để bao gồm một số lớp thông tin, chẳng hạn như **lời nhắc hệ thống**, là một tập hợp các hướng dẫn cơ bản xác định các tham số hoạt động của AI — ví dụ, "Bạn là một người viết tài liệu kỹ thuật; giọng điệu của bạn phải trang trọng và chính xác." Ngữ cảnh được làm phong phú thêm với dữ liệu bên ngoài. Điều này bao gồm các tài liệu đã truy xuất, nơi AI chủ động tìm nạp thông tin từ cơ sở kiến thức để thông báo phản hồi của nó, chẳng hạn như kéo các thông số kỹ thuật cho một dự án. Nó cũng kết hợp các đầu ra công cụ, là kết quả từ việc AI sử dụng API bên ngoài để lấy dữ liệu thời gian thực, như truy vấn lịch để xác định tính khả dụng của người dùng. Dữ liệu rõ ràng này được kết hợp với dữ liệu ngầm quan trọng, chẳng hạn như danh tính người dùng, lịch sử tương tác và trạng thái môi trường. Nguyên tắc cốt lõi là ngay cả các mô hình tiên tiến cũng hoạt động kém khi được cung cấp một cái nhìn hạn chế hoặc được xây dựng kém về môi trường hoạt động.

Thực hành này, do đó, định hình lại nhiệm vụ từ việc chỉ trả lời một câu hỏi thành việc xây dựng một bức tranh hoạt động toàn diện cho tác nhân. Ví dụ, một tác nhân được thiết kế theo ngữ cảnh sẽ không chỉ phản hồi một truy vấn mà trước tiên sẽ tích hợp tính khả dụng của lịch của người dùng (đầu ra công cụ), mối quan hệ chuyên nghiệp với người nhận email (dữ liệu ngầm) và ghi chú từ các cuộc họp trước đó (tài liệu đã truy xuất). Điều này cho phép mô hình tạo ra các đầu ra có liên quan cao, được cá nhân hóa và hữu ích một cách thực tế. Thành phần "kỹ thuật" liên quan đến việc tạo ra các đường ống mạnh mẽ để tìm nạp và chuyển đổi dữ liệu này trong thời gian chạy và thiết lập các vòng phản hồi để liên tục cải thiện chất lượng ngữ cảnh.

Để triển khai điều này, các hệ thống điều chỉnh chuyên biệt có thể được sử dụng để tự động hóa quá trình cải thiện ở quy mô lớn. Ví dụ, các công cụ như trình tối ưu hóa lời nhắc Vertex AI của Google có thể nâng cao hiệu suất mô hình bằng cách đánh giá có hệ thống các phản hồi dựa trên một tập hợp các đầu vào mẫu và các số liệu đánh giá được xác định trước. Cách tiếp cận này hiệu quả để điều chỉnh các lời nhắc và hướng dẫn hệ thống trên các mô hình khác nhau mà không yêu cầu viết lại thủ công rộng rãi. Bằng cách cung cấp cho trình tối ưu hóa như vậy các lời nhắc mẫu, hướng dẫn hệ thống và một mẫu, nó có thể tinh chỉnh các đầu vào ngữ cảnh một cách có lập trình, cung cấp một phương pháp có cấu trúc để triển khai các vòng phản hồi cần thiết cho Kỹ thuật ngữ cảnh tinh vi.

Cách tiếp cận có cấu trúc này là điều tạo nên sự khác biệt giữa một công cụ AI thô sơ với một hệ thống tinh vi hơn và nhận biết ngữ cảnh. Nó coi bản thân ngữ cảnh là một thành phần chính, đặt tầm quan trọng lớn vào những gì tác nhân biết, khi nào nó biết và cách nó sử dụng thông tin đó. Thực hành này đảm bảo mô hình có sự hiểu biết toàn diện về ý định, lịch sử và môi trường hiện tại của người dùng. Cuối cùng, Kỹ thuật ngữ cảnh là một phương pháp quan trọng để biến các chatbot không trạng thái thành các hệ thống có khả năng cao, nhận biết tình huống.

# Sơ lược

**Cái gì:** Các tác vụ phức tạp thường làm quá tải LLM khi được xử lý trong một lời nhắc duy nhất, dẫn đến các vấn đề hiệu suất đáng kể. Tải nhận thức trên mô hình làm tăng khả năng xảy ra lỗi như bỏ qua hướng dẫn, mất ngữ cảnh và tạo ra thông tin không chính xác. Một lời nhắc nguyên khối gặp khó khăn trong việc quản lý nhiều ràng buộc và các bước suy luận tuần tự một cách hiệu quả. Điều này dẫn đến các đầu ra không đáng tin cậy và không chính xác, vì LLM không giải quyết được tất cả các khía cạnh của yêu cầu đa diện.

**Tại sao:** Chuỗi lời nhắc cung cấp một giải pháp tiêu chuẩn hóa bằng cách chia nhỏ một vấn đề phức tạp thành một chuỗi các tác vụ phụ nhỏ hơn, được kết nối với nhau. Mỗi bước trong chuỗi sử dụng một lời nhắc tập trung để thực hiện một hoạt động cụ thể, cải thiện đáng kể độ tin cậy và kiểm soát. Đầu ra từ một lời nhắc được chuyển làm đầu vào cho lời nhắc tiếp theo, tạo ra một quy trình làm việc logic dần dần xây dựng giải pháp cuối cùng. Chiến lược mô-đun, chia để trị này làm cho quá trình dễ quản lý hơn, dễ gỡ lỗi hơn và cho phép tích hợp các công cụ bên ngoài hoặc các định dạng dữ liệu có cấu trúc giữa các bước. Mẫu này là nền tảng để phát triển các hệ thống tác nhân tinh vi, nhiều bước có thể lập kế hoạch, suy luận và thực hiện các quy trình làm việc phức tạp.

**Quy tắc chung:** Sử dụng mẫu này khi một tác vụ quá phức tạp đối với một lời nhắc duy nhất, liên quan đến nhiều giai đoạn xử lý riêng biệt, yêu cầu tương tác với các công cụ bên ngoài giữa các bước, hoặc khi xây dựng các hệ thống tác nhân cần thực hiện suy luận nhiều bước và duy trì trạng thái.

**Tóm tắt trực quan**

<figure>
<img style="display: block; margin: auto; center" src="../imgs/fig.2.png" alt="Mẫu Chuỗi Lời Nhắc: Các tác nhân nhận một loạt các lời nhắc từ người dùng, với đầu ra của mỗi tác nhân đóng vai trò là đầu vào cho tác nhân tiếp theo trong chuỗi">

<figcaption>Hình 2: Mẫu Chuỗi Lời Nhắc: Các tác nhân nhận một loạt các lời nhắc từ người dùng, với đầu ra của mỗi tác nhân đóng vai trò là đầu vào cho tác nhân tiếp theo trong chuỗi</figcaption>
</figure>

# Những điểm chính

Dưới đây là một số điểm chính:

* Chuỗi lời nhắc chia nhỏ các tác vụ phức tạp thành một chuỗi các bước nhỏ hơn, tập trung. Điều này đôi khi được gọi là mẫu Pipeline.
* Mỗi bước trong một chuỗi liên quan đến một lệnh gọi LLM hoặc logic xử lý, sử dụng đầu ra của bước trước đó làm đầu vào.
* Mẫu này cải thiện độ tin cậy và khả năng quản lý của các tương tác phức tạp với các mô hình ngôn ngữ.
* Các khung như LangChain/LangGraph và Google ADK cung cấp các công cụ mạnh mẽ để xác định, quản lý và thực thi các chuỗi nhiều bước này.

# Kết luận

Bằng cách phân tích các vấn đề phức tạp thành một chuỗi các tác vụ phụ đơn giản hơn, dễ quản lý hơn, chuỗi lời nhắc cung cấp một khung mạnh mẽ để hướng dẫn các mô hình ngôn ngữ lớn. Chiến lược "chia để trị" này tăng cường đáng kể độ tin cậy và kiểm soát đầu ra bằng cách tập trung mô hình vào một hoạt động cụ thể tại một thời điểm. Là một mẫu nền tảng, nó cho phép phát triển các tác nhân AI tinh vi có khả năng suy luận nhiều bước, tích hợp công cụ và quản lý trạng thái. Cuối cùng, việc nắm vững chuỗi lời nhắc là rất quan trọng để xây dựng các hệ thống mạnh mẽ, nhận biết ngữ cảnh có thể thực hiện các quy trình làm việc phức tạp vượt xa khả năng của một lời nhắc duy nhất.

# Tài liệu tham khảo

1. Tài liệu LangChain về LCEL: [https://python.langchain.com/v0.2/docs/core_modules/expression_language/](https://python.langchain.com/v0.2/docs/core_modules/expression_language/)
2. Tài liệu LangGraph: [https://langchain-ai.github.io/langgraph/](https://langchain-ai.github.io/langgraph/)
3. Hướng dẫn Kỹ thuật lời nhắc - Chuỗi lời nhắc: [https://www.promptingguide.ai/techniques/chaining](https://www.promptingguide.ai/techniques/chaining)
4. Tài liệu API OpenAI (Các khái niệm lời nhắc chung): [https://platform.openai.com/docs/guides/gpt/prompting](https://platform.openai.com/docs/guides/gpt/prompting)
5. Tài liệu Crew AI (Tác vụ và Quy trình): [https://docs.crewai.com/](https://docs.crewai.com/)
6. Google AI cho nhà phát triển (Hướng dẫn lời nhắc): [https://cloud.google.com/discover/what-is-prompt-engineering?hl=en](https://cloud.google.com/discover/what-is-prompt-engineering?hl=en)
7. Trình tối ưu hóa lời nhắc Vertex [https://cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/prompt-optimizer](https://cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/prompt-optimizer)
