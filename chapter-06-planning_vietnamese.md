Chương 6: Lập Kế Hoạch

Hành vi thông minh thường không chỉ đơn thuần là phản ứng với đầu vào tức thì. Nó đòi hỏi sự nhìn xa trông rộng, khả năng chia nhỏ các tác vụ phức tạp thành các bước nhỏ hơn, dễ quản lý và hoạch định chiến lược để đạt được kết quả mong muốn. Đây chính là nơi mô hình Lập Kế Hoạch (Planning) phát huy tác dụng. Cốt lõi của lập kế hoạch là khả năng của một tác nhân (agent) hoặc một hệ thống tác nhân xây dựng một chuỗi hành động để di chuyển từ trạng thái ban đầu đến trạng thái mục tiêu.

Tổng quan về Mô hình Lập Kế Hoạch

Trong bối cảnh AI, hữu ích khi coi một tác nhân lập kế hoạch như một chuyên gia mà Sếp ủy thác một mục tiêu phức tạp. Khi Sếp yêu cầu nó "tổ chức một buổi họp nhóm bên ngoài (offsite)," Sếp đang xác định cái gì—mục tiêu và các ràng buộc của nó—chứ không phải cách nào. Nhiệm vụ cốt lõi của tác nhân là tự động vạch ra một lộ trình đến mục tiêu đó. Nó phải hiểu trước trạng thái ban đầu (ví dụ: ngân sách, số lượng người tham gia, ngày mong muốn) và trạng thái mục tiêu (một buổi offsite đã được đặt thành công), và sau đó khám phá chuỗi hành động tối ưu để kết nối chúng. Kế hoạch không được biết trước; nó được tạo ra để đáp ứng yêu cầu.

Một đặc điểm nổi bật của quy trình này là khả năng thích ứng. Một kế hoạch ban đầu chỉ đơn thuần là một điểm khởi đầu, không phải là một kịch bản cứng nhắc. Sức mạnh thực sự của tác nhân là khả năng kết hợp thông tin mới và điều hướng dự án vượt qua các chướng ngại vật. Ví dụ, nếu địa điểm ưa thích trở nên không khả dụng hoặc nhà cung cấp dịch vụ ăn uống đã kín lịch, một tác nhân có khả năng không chỉ đơn giản là thất bại. Nó thích ứng. Nó ghi nhận ràng buộc mới, đánh giá lại các lựa chọn của mình và xây dựng một kế hoạch mới, có lẽ bằng cách đề xuất các địa điểm hoặc ngày thay thế.

Tuy nhiên, điều quan trọng là phải nhận ra sự đánh đổi giữa tính linh hoạt và khả năng dự đoán. Lập kế hoạch động là một công cụ cụ thể, không phải là một giải pháp phổ quát. Khi giải pháp cho một vấn đề đã được hiểu rõ và có thể lặp lại, việc ràng buộc tác nhân vào một quy trình làm việc cố định, được xác định trước sẽ hiệu quả hơn. Cách tiếp cận này hạn chế quyền tự chủ của tác nhân để giảm sự không chắc chắn và rủi ro hành vi không thể đoán trước, đảm bảo kết quả đáng tin cậy và nhất quán. Do đó, quyết định sử dụng tác nhân lập kế hoạch so với tác nhân thực thi tác vụ đơn giản phụ thuộc vào một câu hỏi duy nhất: "cách nào" cần được khám phá, hay nó đã được biết rồi?

Các Ứng Dụng Thực tế & Trường hợp Sử dụng

Mô hình Lập Kế Hoạch là một quy trình tính toán cốt lõi trong các hệ thống tự trị, cho phép một tác nhân tổng hợp một chuỗi hành động để đạt được một mục tiêu cụ thể, đặc biệt trong các môi trường động hoặc phức tạp. Quá trình này chuyển đổi một mục tiêu cấp cao thành một kế hoạch có cấu trúc bao gồm các bước rời rạc, có thể thực thi được.

Trong các lĩnh vực như tự động hóa tác vụ theo thủ tục, lập kế hoạch được sử dụng để điều phối các quy trình làm việc phức tạp. Ví dụ, một quy trình kinh doanh như onboarding một nhân viên mới có thể được phân tách thành một chuỗi con các tác vụ theo thứ tự, chẳng hạn như tạo tài khoản hệ thống, giao các mô-đun đào tạo và phối hợp với các phòng ban khác nhau. Tác nhân tạo ra một kế hoạch để thực thi các bước này theo một trật tự logic, gọi ra các công cụ cần thiết hoặc tương tác với các hệ thống khác nhau để quản lý các phụ thuộc.

Trong lĩnh vực robot và điều hướng tự hành, lập kế hoạch là nền tảng cho việc di chuyển trạng thái không gian. Một hệ thống, dù là robot vật lý hay thực thể ảo, phải tạo ra một đường dẫn hoặc chuỗi hành động để chuyển từ trạng thái ban đầu sang trạng thái mục tiêu. Điều này liên quan đến việc tối ưu hóa các số liệu như thời gian hoặc mức tiêu thụ năng lượng trong khi tuân thủ các ràng buộc môi trường, như tránh chướng ngại vật hoặc tuân theo các quy tắc giao thông.

Mô hình này cũng rất quan trọng đối với tổng hợp thông tin có cấu trúc. Khi được giao nhiệm vụ tạo ra một đầu ra phức tạp như một báo cáo nghiên cứu, một tác nhân có thể xây dựng một kế hoạch bao gồm các giai đoạn riêng biệt để thu thập thông tin, tóm tắt dữ liệu, cấu trúc nội dung và tinh chỉnh lặp đi lặp lại. Tương tự, trong các tình huống hỗ trợ khách hàng liên quan đến giải quyết vấn đề nhiều bước, một tác nhân có thể tạo và tuân theo một kế hoạch hệ thống để chẩn đoán, thực hiện giải pháp và leo thang vấn đề.

Về bản chất, mô hình Lập Kế Hoạch cho phép một tác nhân vượt ra ngoài các hành động đơn giản, phản ứng để hướng tới hành vi hướng mục tiêu. Nó cung cấp khuôn khổ logic cần thiết để giải quyết các vấn đề đòi hỏi một chuỗi hoạt động phụ thuộc lẫn nhau một cách mạch lạc.

Mã thực hành (Crew AI)

Phần sau đây sẽ trình bày cách triển khai mô hình Planner bằng cách sử dụng khuôn khổ Crew AI. Mô hình này liên quan đến một tác nhân mà trước tiên xây dựng một kế hoạch nhiều bước để giải quyết một truy vấn phức tạp và sau đó thực thi kế hoạch đó một cách tuần tự.

Google DeepResearch

Google Gemini DeepResearch (xem Hình 1) là một hệ thống dựa trên tác nhân được thiết kế để truy xuất và tổng hợp thông tin tự động. Nó hoạt động thông qua một pipeline tác nhân nhiều bước, liên tục và linh hoạt truy vấn Google Search để khám phá có hệ thống các chủ đề phức tạp. Hệ thống được thiết kế để xử lý một kho dữ liệu lớn từ các nguồn dựa trên web, đánh giá dữ liệu đã thu thập về mức độ liên quan và khoảng trống kiến thức, đồng thời thực hiện các tìm kiếm tiếp theo để giải quyết chúng. Đầu ra cuối cùng hợp nhất thông tin đã được kiểm duyệt thành một bản tóm tắt có cấu trúc, nhiều trang với các trích dẫn đến các nguồn gốc.

Mở rộng thêm, hoạt động của hệ thống không phải là một sự kiện truy vấn-phản hồi đơn lẻ mà là một quy trình dài hạn, được quản lý. Nó bắt đầu bằng cách phân tích cú pháp lệnh nhắc của người dùng thành một kế hoạch nghiên cứu nhiều điểm (xem Hình 1), sau đó được trình bày cho người dùng để xem xét và sửa đổi. Điều này cho phép định hình quỹ đạo nghiên cứu một cách hợp tác trước khi thực thi. Khi kế hoạch được phê duyệt, pipeline tác nhân bắt đầu vòng lặp tìm kiếm-và-phân tích lặp đi lặp lại. Điều này liên quan đến nhiều hơn là chỉ thực hiện một loạt các tìm kiếm được xác định trước; tác nhân tự động xây dựng và tinh chỉnh các truy vấn của mình dựa trên thông tin nó thu thập, tích cực xác định các khoảng trống kiến thức, xác nhận các điểm dữ liệu và giải quyết các khác biệt.

Hình 1: Tác nhân Google Deep Research tạo ra một kế hoạch thực thi để sử dụng Google Search làm công cụ.

Một thành phần kiến trúc chính là khả năng của hệ thống để quản lý quy trình này một cách không đồng bộ (asynchronously). Thiết kế này đảm bảo rằng việc điều tra, có thể liên quan đến việc phân tích hàng trăm nguồn, có khả năng phục hồi trước các lỗi điểm đơn và cho phép người dùng thoát ra và được thông báo khi hoàn thành. Hệ thống cũng có thể tích hợp các tài liệu do người dùng cung cấp, kết hợp thông tin từ các nguồn riêng tư với nghiên cứu dựa trên web của nó. Đầu ra cuối cùng không chỉ là một danh sách các phát hiện được nối lại mà là một báo cáo có cấu trúc, nhiều trang. Trong giai đoạn tổng hợp, mô hình thực hiện đánh giá quan trọng thông tin đã thu thập, xác định các chủ đề chính và sắp xếp nội dung thành một câu chuyện mạch lạc với các phần logic. Báo cáo được thiết kế để tương tác, thường bao gồm các tính năng như tổng quan bằng âm thanh, biểu đồ và liên kết đến các nguồn được trích dẫn gốc, cho phép người dùng xác minh và khám phá thêm. Ngoài các kết quả được tổng hợp, mô hình còn trả về rõ ràng danh sách đầy đủ các nguồn mà nó đã tìm kiếm và tham khảo (xem Hình 2). Chúng được trình bày dưới dạng trích dẫn, cung cấp tính minh bạch hoàn toàn và quyền truy cập trực tiếp vào thông tin chính. Toàn bộ quá trình này biến một truy vấn đơn giản thành một lượng kiến thức toàn diện, được tổng hợp.

Hình 2: Một ví dụ về việc kế hoạch Deep Research đang được thực thi, dẫn đến việc Google Search được sử dụng như một công cụ để tìm kiếm nhiều nguồn web khác nhau.

Bằng cách giảm thiểu đáng kể thời gian và nguồn lực cần thiết cho việc thu thập và tổng hợp dữ liệu thủ công, Gemini DeepResearch cung cấp một phương pháp khám phá thông tin có cấu trúc và triệt để hơn. Giá trị của hệ thống đặc biệt rõ ràng trong các tác vụ nghiên cứu phức tạp, đa diện trên nhiều lĩnh vực khác nhau.

Ví dụ, trong phân tích cạnh tranh, tác nhân có thể được chỉ đạo để thu thập và đối chiếu dữ liệu một cách có hệ thống về xu hướng thị trường, thông số kỹ thuật sản phẩm của đối thủ cạnh tranh, tâm lý công chúng từ các nguồn trực tuyến đa dạng và chiến lược marketing. Quy trình tự động này thay thế nhiệm vụ tốn nhiều sức lực là theo dõi thủ công nhiều đối thủ cạnh tranh, cho phép các nhà phân tích tập trung vào việc diễn giải chiến lược cấp cao hơn thay vì thu thập dữ liệu (xem Hình 3).

Hình 3: Đầu ra cuối cùng được tạo ra bởi tác nhân Google Deep Research, phân tích các nguồn thu được bằng Google Search làm công cụ thay mặt chúng ta.

Tương tự, trong khám phá học thuật, hệ thống đóng vai trò là một công cụ mạnh mẽ để thực hiện các đánh giá tài liệu mở rộng. Nó có thể xác định và tóm tắt các bài báo nền tảng, theo dõi sự phát triển của các khái niệm qua nhiều ấn phẩm và lập bản đồ các mặt trận nghiên cứu mới nổi trong một lĩnh vực cụ thể, do đó đẩy nhanh giai đoạn ban đầu và tốn thời gian nhất của việc nghiên cứu học thuật.

Hiệu quả của cách tiếp cận này bắt nguồn từ việc tự động hóa chu trình tìm kiếm-và-lọc lặp đi lặp lại, vốn là một nút thắt cổ chai cốt lõi trong nghiên cứu thủ công. Tính toàn diện đạt được nhờ khả năng của hệ thống xử lý khối lượng và sự đa dạng của các nguồn thông tin lớn hơn mức thường khả thi đối với một nhà nghiên cứu con người trong một khung thời gian tương đương. Phạm vi phân tích rộng hơn này giúp giảm thiểu khả năng xảy ra thiên vị chọn lọc (selection bias) và tăng khả năng khám phá ra thông tin ít rõ ràng nhưng có khả năng quan trọng, dẫn đến sự hiểu biết mạnh mẽ và có cơ sở hơn về chủ đề.

OpenAI Deep Research API

OpenAI Deep Research API là một công cụ chuyên biệt được thiết kế để tự động hóa các tác vụ nghiên cứu phức tạp. Nó sử dụng một mô hình tác nhân tiên tiến có thể tự động suy luận, lập kế hoạch và tổng hợp thông tin từ các nguồn thực tế. Không giống như một mô hình Hỏi & Đáp đơn giản, nó nhận một truy vấn cấp cao và tự chủ chia nó thành các câu hỏi phụ, thực hiện tìm kiếm trên web bằng cách sử dụng các công cụ tích hợp sẵn và cung cấp một báo cáo cuối cùng có cấu trúc, giàu trích dẫn. API cung cấp quyền truy cập lập trình trực tiếp vào toàn bộ quá trình này, sử dụng các mô hình như o3-deep-research-2025-06-26 tại thời điểm viết bài để tổng hợp chất lượng cao và mô hình nhanh hơn o4-mini-deep-research-2025-06-26 cho các ứng dụng nhạy cảm về độ trễ.

Deep Research API hữu ích vì nó tự động hóa những gì lẽ ra là hàng giờ nghiên cứu thủ công, cung cấp các báo cáo cấp độ chuyên nghiệp, dựa trên dữ liệu, phù hợp để cung cấp thông tin cho chiến lược kinh doanh, quyết định đầu tư hoặc khuyến nghị chính sách. Các lợi ích chính của nó bao gồm:

Đầu ra có cấu trúc, được trích dẫn: Nó tạo ra các báo cáo được tổ chức tốt với các trích dẫn nội tuyến được liên kết với siêu dữ liệu nguồn, đảm bảo các tuyên bố có thể kiểm chứng và được hỗ trợ bởi dữ liệu.

Tính minh bạch: Không giống như quy trình trừu tượng trong ChatGPT, API phơi bày tất cả các bước trung gian, bao gồm suy luận của tác nhân, các truy vấn tìm kiếm web cụ thể mà nó đã thực thi và bất kỳ mã nào nó đã chạy. Điều này cho phép gỡ lỗi chi tiết, phân tích và hiểu sâu hơn về cách câu trả lời cuối cùng được xây dựng.

Khả năng mở rộng: Nó hỗ trợ Giao thức Ngữ cảnh Mô hình (Model Context Protocol - MCP), cho phép các nhà phát triển kết nối tác nhân với các cơ sở kiến thức riêng tư và nguồn dữ liệu nội bộ, kết hợp nghiên cứu web công khai với thông tin độc quyền.

Để sử dụng API, Sếp gửi một yêu cầu đến điểm cuối client.responses.create, chỉ định một mô hình, một lệnh nhắc đầu vào và các công cụ mà tác nhân có thể sử dụng. Đầu vào thường bao gồm một system_message xác định persona của tác nhân và định dạng đầu ra mong muốn, cùng với user_query. Sếp cũng phải bao gồm công cụ web_search_preview và có thể tùy chọn thêm các công cụ khác như code_interpreter hoặc các công cụ MCP tùy chỉnh (xem Chương 10) cho dữ liệu nội bộ.

OpenAI Deep Research API Example

Đoạn mã này sử dụng OpenAI API để thực hiện một tác vụ "Nghiên cứu Sâu". Nó định nghĩa vai trò của tác nhân (nhà nghiên cứu chuyên nghiệp) và truy vấn nghiên cứu của người dùng. Sau đó, nó xây dựng một lời gọi API tới mô hình nghiên cứu sâu chuyên biệt, yêu cầu tổng hợp kết quả và bật công cụ tìm kiếm web. Mặc dù lời gọi API thực tế được bình luận để ngăn thực thi, các phần mã sau đó minh họa cách Sếp sẽ trích xuất và in báo cáo cuối cùng, cũng như cách kiểm tra các trích dẫn nội tuyến (bao gồm văn bản được trích dẫn, tiêu đề, URL) và các bước trung gian (suy luận, lời gọi tìm kiếm web, thực thi mã) để có được tính minh bạch và khả năng gỡ lỗi tối đa.

Tóm lược

Cái gì: Các vấn đề phức tạp thường không thể giải quyết bằng một hành động duy nhất và đòi hỏi sự nhìn xa trông rộng để đạt được kết quả mong muốn. Nếu không có cách tiếp cận có cấu trúc, một hệ thống tác nhân sẽ gặp khó khăn trong việc xử lý các yêu cầu đa diện liên quan đến nhiều bước và sự phụ thuộc. Điều này gây khó khăn trong việc chia nhỏ các mục tiêu cấp cao thành một chuỗi các tác vụ nhỏ hơn, có thể thực thi được. Do đó, hệ thống không thể hoạch định chiến lược hiệu quả, dẫn đến kết quả không đầy đủ hoặc không chính xác khi đối mặt với các mục tiêu phức tạp.

Tại sao: Mô hình Lập Kế Hoạch đưa ra một giải pháp tiêu chuẩn hóa bằng cách yêu cầu một hệ thống tác nhân trước tiên tạo ra một kế hoạch mạch lạc để giải quyết một mục tiêu. Nó liên quan đến việc phân tách một mục tiêu cấp cao thành một chuỗi các bước hoặc mục tiêu phụ nhỏ hơn, có thể hành động được. Điều này cho phép hệ thống quản lý các quy trình làm việc phức tạp, điều phối các công cụ khác nhau và xử lý các phụ thuộc theo một trật tự logic. LLMs đặc biệt phù hợp với việc này, vì chúng có thể tạo ra các kế hoạch hợp lý và hiệu quả dựa trên kho dữ liệu đào tạo rộng lớn của chúng. Cách tiếp cận có cấu trúc này biến một tác nhân phản ứng đơn giản thành một người thực thi chiến lược có thể chủ động hướng tới một mục tiêu phức tạp và thậm chí thích ứng với kế hoạch của mình nếu cần.

Quy tắc chung: Sử dụng mô hình này khi yêu cầu của người dùng quá phức tạp để được xử lý bằng một hành động hoặc công cụ duy nhất. Nó lý tưởng để tự động hóa các quy trình nhiều bước, chẳng hạn như tạo một báo cáo nghiên cứu chi tiết, onboarding một nhân viên mới hoặc thực hiện phân tích cạnh tranh. Áp dụng mô hình Lập Kế Hoạch bất cứ khi nào một tác vụ yêu cầu một chuỗi các hoạt động phụ thuộc lẫn nhau để đạt được kết quả cuối cùng, được tổng hợp.

Tóm tắt trực quan

<figcaption>Hình 4: Mô hình thiết kế Lập Kế Hoạch (Planning design pattern)</figcaption>

Các Điểm Chính

Lập Kế Hoạch cho phép các tác nhân chia nhỏ các mục tiêu phức tạp thành các bước tuần tự, có thể hành động được.

Nó rất cần thiết cho việc xử lý các tác vụ nhiều bước, tự động hóa quy trình làm việc và điều hướng các môi trường phức tạp.

LLMs có thể thực hiện lập kế hoạch bằng cách tạo ra các cách tiếp cận từng bước dựa trên mô tả tác vụ.

Việc nhắc nhở rõ ràng hoặc thiết kế các tác vụ để yêu cầu các bước lập kế hoạch sẽ khuyến khích hành vi này trong các khuôn khổ tác nhân.

Google Deep Research là một tác nhân phản ánh, lập kế hoạch và thực thi, phân tích các nguồn thu được bằng Google Search làm công cụ thay mặt chúng ta.

Kết luận

Tóm lại, mô hình Lập Kế Hoạch là một thành phần nền tảng giúp nâng tầm các hệ thống tác nhân từ những người phản hồi đơn giản sang những người thực thi chiến lược, hướng mục tiêu. Các mô hình ngôn ngữ lớn hiện đại cung cấp khả năng cốt lõi cho điều này, tự động phân tách các mục tiêu cấp cao thành các bước mạch lạc, có thể hành động được. Mô hình này mở rộng từ việc thực thi tác vụ tuần tự, đơn giản, như được minh họa bởi tác nhân CrewAI tạo và tuân theo một kế hoạch viết, đến các hệ thống phức tạp và năng động hơn. Tác nhân Google DeepResearch là một ví dụ về ứng dụng tiên tiến này, tạo ra các kế hoạch nghiên cứu lặp đi lặp lại thích ứng và phát triển dựa trên việc thu thập thông tin liên tục. Cuối cùng, lập kế hoạch cung cấp cầu nối thiết yếu giữa ý định của con người và việc thực thi tự động cho các vấn đề phức tạp. Bằng cách cấu trúc một cách tiếp cận giải quyết vấn đề, mô hình này cho phép các tác nhân quản lý các quy trình làm việc phức tạp và mang lại kết quả toàn diện, được tổng hợp.

Tài liệu tham khảo

Google DeepResearch (Tính năng của Gemini): gemini.google.com

OpenAI, Giới thiệu nghiên cứu sâu: https://openai.com/index/introducing-deep-research/

Perplexity, Giới thiệu Perplexity Deep Research, https://www.perplexity.ai/hub/blog/introducing-perplexity-deep-research

