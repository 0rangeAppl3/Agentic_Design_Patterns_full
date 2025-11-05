# Chương 7: Hợp tác Đa Tác nhân

Mặc dù kiến trúc tác nhân đơn khối (monolithic agent) có thể hiệu quả đối với các vấn đề được xác định rõ ràng, khả năng của nó thường bị hạn chế khi đối mặt với các nhiệm vụ phức tạp, đa lĩnh vực. Mẫu Hợp tác Đa Tác nhân (Multi-Agent Collaboration) giải quyết những hạn chế này bằng cách cấu trúc một hệ thống như một tập hợp hợp tác của các tác nhân riêng biệt, chuyên biệt hóa. Cách tiếp cận này dựa trên nguyên tắc phân rã nhiệm vụ (task decomposition), trong đó một mục tiêu cấp cao được chia thành các bài toán con riêng biệt. Mỗi bài toán con sau đó được giao cho một tác nhân sở hữu các công cụ, quyền truy cập dữ liệu hoặc khả năng suy luận cụ thể phù hợp nhất cho nhiệm vụ đó.

Ví dụ, một truy vấn nghiên cứu phức tạp có thể được phân rã và gán cho một Tác nhân Nghiên cứu (Research Agent) để truy xuất thông tin, một Tác nhân Phân tích Dữ liệu (Data Analysis Agent) để xử lý thống kê, và một Tác nhân Tổng hợp (Synthesis Agent) để tạo báo cáo cuối cùng. Hiệu quả của một hệ thống như vậy không chỉ đơn thuần là do sự phân công lao động mà còn phụ thuộc nghiêm trọng vào các cơ chế giao tiếp giữa các tác nhân. Điều này đòi hỏi một giao thức truyền thông chuẩn hóa và một bản thể luận (ontology) chung, cho phép các tác nhân trao đổi dữ liệu, ủy thác các nhiệm vụ con và phối hợp các hành động của chúng để đảm bảo đầu ra cuối cùng mạch lạc.

Kiến trúc phân tán này mang lại một số lợi thế, bao gồm tính mô-đun (modularity) nâng cao, khả năng mở rộng (scalability) và tính bền vững (robustness), vì sự thất bại của một tác nhân đơn lẻ không nhất thiết gây ra lỗi hệ thống toàn bộ. Sự hợp tác cho phép tạo ra một kết quả mang tính tổng hợp, nơi hiệu suất tập thể của hệ thống đa tác nhân vượt qua khả năng tiềm ẩn của bất kỳ tác nhân đơn lẻ nào trong tập hợp đó.# Tổng quan về Mẫu Hợp tác Đa Tác nhân

Mẫu Hợp tác Đa Tác nhân liên quan đến việc thiết kế các hệ thống nơi nhiều tác nhân độc lập hoặc bán độc lập làm việc cùng nhau để đạt được một mục tiêu chung. Mỗi tác nhân thường có một vai trò xác định, các mục tiêu cụ thể phù hợp với mục tiêu tổng thể và có khả năng truy cập vào các công cụ hoặc cơ sở tri thức khác nhau. Sức mạnh của mẫu này nằm ở sự tương tác và sức mạnh tổng hợp giữa các tác nhân này.

Sự hợp tác có thể diễn ra dưới nhiều hình thức khác nhau:* **Chuyển giao tuần tự (Sequential Handoffs):** Một tác nhân hoàn thành nhiệm vụ và chuyển đầu ra của mình cho tác nhân khác cho bước tiếp theo trong một quy trình (tương tự như mẫu Lập kế hoạch, nhưng liên quan rõ ràng đến các tác nhân khác nhau).
* **Xử lý song song (Parallel Processing):** Nhiều tác nhân làm việc đồng thời trên các phần khác nhau của một vấn đề, và kết quả của chúng sau đó được kết hợp lại.
* **Tranh luận và Đồng thuận (Debate and Consensus):** Hợp tác Đa Tác nhân nơi các Tác nhân với các quan điểm và nguồn thông tin đa dạng tham gia vào các cuộc thảo luận để đánh giá các lựa chọn, cuối cùng đi đến một sự đồng thuận hoặc một quyết định sáng suốt hơn.
* **Cấu trúc phân cấp (Hierarchical Structures):** Một tác nhân quản lý (manager agent) có thể ủy thác nhiệm vụ cho các tác nhân công nhân (worker agents) một cách linh hoạt dựa trên quyền truy cập công cụ hoặc khả năng plugin của chúng và tổng hợp kết quả của chúng. Mỗi tác nhân cũng có thể xử lý các nhóm công cụ có liên quan, thay vì một tác nhân duy nhất xử lý tất cả các công cụ.
* **Đội ngũ chuyên gia (Expert Teams):** Các tác nhân có kiến thức chuyên môn về các lĩnh vực khác nhau (ví dụ: một nhà nghiên cứu, một người viết, một biên tập viên) hợp tác để tạo ra một đầu ra phức tạp.

* ### **Người phê bình-Người đánh giá (Critic-Reviewer):** Các tác nhân tạo ra các kết quả ban đầu như kế hoạch, bản nháp hoặc câu trả lời. Một nhóm tác nhân thứ hai sau đó đánh giá nghiêm ngặt đầu ra này về việc tuân thủ các chính sách, bảo mật, tuân thủ quy định, tính chính xác, chất lượng và sự phù hợp với các mục tiêu của tổ chức. Người tạo ban đầu hoặc một tác nhân cuối cùng sẽ sửa đổi đầu ra dựa trên phản hồi này. Mẫu này đặc biệt hiệu quả cho việc tạo mã, viết nghiên cứu, kiểm tra logic và đảm bảo sự phù hợp về mặt đạo đức. Ưu điểm của phương pháp này bao gồm tăng tính bền vững, cải thiện chất lượng và giảm khả năng xảy ra ảo giác (hallucinations) hoặc lỗi).

Một hệ thống đa tác nhân (xem Hình 1) về cơ bản bao gồm việc phân định vai trò và trách nhiệm của tác nhân, thiết lập các kênh liên lạc qua đó các tác nhân trao đổi thông tin, và xây dựng một quy trình công việc hoặc giao thức tương tác chỉ đạo các nỗ lực hợp tác của chúng.

<figure>
<img src="../imgs/fig.7.1.Example_of_multi-agent_system.png" alt="Hình 1: Ví dụ về hệ thống đa tác nhân">
<figcaption>
Hình 1: Ví dụ về hệ thống đa tác nhân
</figcaption>
</figure>

Các framework như Crew AI và Google ADK được thiết kế để tạo điều kiện thuận lợi cho mô hình này bằng cách cung cấp các cấu trúc để đặc tả các tác nhân, nhiệm vụ và các quy trình tương tác của chúng. Cách tiếp cận này đặc biệt hiệu quả đối với những thách thức đòi hỏi nhiều kiến thức chuyên môn khác nhau, bao gồm nhiều giai đoạn riêng biệt, hoặc tận dụng lợi thế của việc xử lý đồng thời và xác thực thông tin giữa các tác nhân.# Practical Applications & Use Cases

Multi-Agent Collaboration là một mẫu mạnh mẽ có thể áp dụng trên nhiều lĩnh vực:

* **Nghiên cứu và Phân tích Phức tạp:** Một nhóm các tác nhân có thể hợp tác trong một dự án nghiên cứu. Một tác nhân có thể chuyên tìm kiếm cơ sở dữ liệu học thuật, một tác nhân khác chuyên tóm tắt các phát hiện, tác nhân thứ ba xác định các xu hướng và tác nhân thứ tư tổng hợp thông tin thành một báo cáo. Điều này phản ánh cách một nhóm nghiên cứu con người có thể hoạt động.
* **Phát triển Phần mềm:** Hãy tưởng tượng các tác nhân hợp tác xây dựng phần mềm. Một tác nhân có thể là nhà phân tích yêu cầu, một tác nhân khác là người tạo mã, tác nhân thứ ba là người kiểm thử và tác nhân thứ tư là người viết tài liệu. Chúng có thể chuyển giao kết quả cho nhau để xây dựng và xác minh các thành phần.
* **Tạo nội dung Sáng tạo:** Việc tạo một chiến dịch tiếp thị có thể liên quan đến một tác nhân nghiên cứu thị trường, một tác nhân viết nội dung quảng cáo (copywriter), một tác nhân thiết kế đồ họa (sử dụng các công cụ tạo hình ảnh) và một tác nhân lập lịch truyền thông xã hội, tất cả cùng làm việc với nhau.Phân tích Tài chính: Một hệ thống đa tác nhân có thể phân tích thị trường tài chính.
* **Phân tích Tài chính:** Một hệ thống đa tác nhân có thể phân tích thị trường tài chính. Các tác nhân có thể chuyên lấy dữ liệu chứng khoán, phân tích tâm lý tin tức, thực hiện phân tích kỹ thuật và tạo ra các khuyến nghị đầu tư.
* **Leo thang Hỗ trợ Khách hàng:** Một tác nhân hỗ trợ tuyến đầu có thể xử lý các truy vấn ban đầu, leo thang các vấn đề phức tạp cho một tác nhân chuyên gia (ví dụ: chuyên gia kỹ thuật hoặc chuyên gia thanh toán) khi cần thiết, thể hiện sự chuyển giao tuần tự dựa trên độ phức tạp của vấn đề.Tối ưu hóa Chuỗi Cung ứng: Các tác nhân có thể đại diện cho các nút khác nhau trong chuỗi cung ứng (nhà cung cấp, nhà sản xuất, nhà phân phối) và hợp tác để tối ưu hóa mức tồn kho, hậu cần và lập lịch để ứng phó với nhu cầu thay đổi hoặc gián đoạn.
* **Tối ưu hóa Chuỗi Cung ứng:** Các tác nhân có thể đại diện cho các nút khác nhau trong chuỗi cung ứng (nhà cung cấp, nhà sản xuất, nhà phân phối) và hợp tác để tối ưu hóa mức tồn kho, hậu cần và lập lịch để ứng phó với nhu cầu thay đổi hoặc gián đoạn.* **Phân tích & Khắc phục sự cố Mạng:** Các hoạt động tự trị được hưởng lợi rất nhiều từ kiến trúc tác nhân, đặc biệt là trong việc xác định chính xác các lỗi. Nhiều tác nhân có thể hợp tác để phân loại và khắc phục sự cố, đề xuất các hành động tối ưu. Các tác nhân này cũng có thể tích hợp với các mô hình và công cụ học máy truyền thống, tận dụng các hệ thống hiện có đồng thời cung cấp các lợi thế của AI Tạo sinh.

Khả năng phân định các tác nhân chuyên biệt và điều phối tỉ mỉ các mối quan hệ qua lại của chúng cho phép các nhà phát triển xây dựng các hệ thống thể hiện tính mô-đun, khả năng mở rộng nâng cao và khả năng giải quyết các độ phức tạp mà một tác nhân đơn lẻ, tích hợp không thể vượt qua.# Multi-Agent Collaboration: Exploring Interrelationships and Communication Structures

Hiểu rõ các cách thức phức tạp mà các tác nhân tương tác và giao tiếp là nền tảng để thiết kế các hệ thống đa tác nhân hiệu quả. Như mô tả trong Hình 2, tồn tại một phổ các mô hình giao tiếp và mối quan hệ tương quan, từ kịch bản tác nhân đơn giản nhất đến các khung hợp tác phức tạp, được thiết kế tùy chỉnh. Mỗi mô hình đều có những ưu điểm và thách thức riêng, ảnh hưởng đến hiệu quả tổng thể, tính bền vững và khả năng thích ứng của hệ thống đa tác nhân.

**1. Tác nhân đơn (Single Agent):** Ở cấp độ cơ bản nhất, một "Tác nhân đơn" hoạt động tự chủ mà không có tương tác hoặc giao tiếp trực tiếp với các thực thể khác. Mặc dù mô hình này đơn giản để triển khai và quản lý, khả năng của nó vốn bị giới hạn bởi phạm vi và tài nguyên của từng tác nhân. Nó phù hợp cho các nhiệm vụ có thể phân rã thành các bài toán con độc lập, mỗi bài toán có thể giải quyết được bởi một tác nhân đơn lẻ, tự cung tự cấp.

**2. Mạng lưới (Network):** Mô hình "Mạng lưới" đại diện cho một bước tiến quan trọng hướng tới sự hợp tác, nơi nhiều tác nhân tương tác trực tiếp với nhau theo kiểu phi tập trung. Giao tiếp thường diễn ra theo kiểu ngang hàng (peer-to-peer), cho phép chia sẻ thông tin, tài nguyên và thậm chí cả nhiệm vụ. Mô hình này thúc đẩy khả năng phục hồi, vì sự thất bại của một tác nhân không nhất thiết làm tê liệt toàn bộ hệ thống. Tuy nhiên, việc quản lý chi phí giao tiếp và đảm bảo việc ra quyết định mạch lạc trong một mạng lưới lớn, không có cấu trúc có thể là một thách thức.

**3. Giám sát viên (Supervisor):** Trong mô hình "Giám sát viên", một tác nhân chuyên trách, "giám sát viên", giám sát và điều phối các hoạt động của một nhóm tác nhân cấp dưới. Giám sát viên hoạt động như một trung tâm giao tiếp, phân bổ nhiệm vụ và giải quyết xung đột. Cấu trúc phân cấp này cung cấp các tuyến quyền hạn rõ ràng và có thể đơn giản hóa việc quản lý và kiểm soát. Tuy nhiên, nó giới thiệu một điểm thất bại duy nhất (single point of failure) (người giám sát) và có thể trở thành điểm nghẽn nếu người giám sát bị quá tải bởi số lượng lớn cấp dưới hoặc các nhiệm vụ phức tạp.

**4. Giám sát viên như một Công cụ (Supervisor as a Tool):** Mô hình này là một phần mở rộng tinh tế của khái niệm "Giám sát viên", trong đó vai trò của giám sát viên ít mang tính chỉ huy và kiểm soát trực tiếp hơn mà thiên về cung cấp tài nguyên, hướng dẫn hoặc hỗ trợ phân tích cho các tác nhân khác. Giám sát viên có thể cung cấp các công cụ, dữ liệu hoặc dịch vụ tính toán cho phép các tác nhân khác thực hiện nhiệm vụ của họ hiệu quả hơn mà không nhất thiết phải ra lệnh cho mọi hành động của họ. Cách tiếp cận này nhằm tận dụng khả năng của giám sát viên mà không áp đặt kiểm soát cứng nhắc từ trên xuống.

**5. Phân cấp (Hierarchical):** Mô hình "Phân cấp" mở rộng dựa trên khái niệm giám sát viên để tạo ra một cấu trúc tổ chức nhiều lớp. Điều này liên quan đến nhiều cấp độ giám sát viên, với các giám sát viên cấp cao hơn giám sát các giám sát viên cấp thấp hơn, và cuối cùng, một tập hợp các tác nhân hoạt động ở cấp thấp nhất. Cấu trúc này rất phù hợp cho các vấn đề phức tạp có thể được phân rã thành các bài toán con, mỗi bài toán được quản lý bởi một lớp cụ thể của hệ thống phân cấp. Nó cung cấp một cách tiếp cận có cấu trúc để quản lý khả năng mở rộng và độ phức tạp, cho phép ra quyết định phân tán trong các ranh giới xác định.

<figure>
<img src="../imgs/fig.7.2.Agents_communicate_and_interact_in_various_ways.png" alt="Hình 2: Các tác nhân giao tiếp và tương tác theo nhiều cách khác nhau.">
<figcaption>
Hình 2: Các tác nhân giao tiếp và tương tác theo nhiều cách khác nhau.
</figcaption>
</figure>**6. Tùy chỉnh (Custom):** Mô hình "Tùy chỉnh" đại diện cho sự linh hoạt tối thượng trong thiết kế hệ thống đa tác nhân. Nó cho phép tạo ra các cấu trúc giao tiếp và mối quan hệ tương quan độc đáo được thiết kế chính xác theo các yêu cầu cụ thể của một vấn đề hoặc ứng dụng nhất định. Điều này có thể liên quan đến các phương pháp tiếp cận kết hợp (hybrid) kết hợp các yếu tố từ các mô hình đã đề cập trước đó, hoặc các thiết kế hoàn toàn mới lạ xuất phát từ các ràng buộc và cơ hội duy nhất của môi trường. Các mô hình tùy chỉnh thường phát sinh từ nhu cầu tối ưu hóa cho các số liệu hiệu suất cụ thể, xử lý các môi trường động cao, hoặc kết hợp kiến thức miền cụ thể vào kiến trúc của hệ thống. Việc thiết kế và triển khai các mô hình tùy chỉnh thường đòi hỏi sự hiểu biết sâu sắc về các nguyên tắc hệ thống đa tác nhân và xem xét cẩn thận các giao thức truyền thông, cơ chế phối hợp và các hành vi mới nổi.

Tóm lại, việc lựa chọn mô hình giao tiếp và mối quan hệ tương quan cho một hệ thống đa tác nhân là một quyết định thiết kế quan trọng. Mỗi mô hình cung cấp những ưu điểm và nhược điểm riêng biệt, và sự lựa chọn tối ưu phụ thuộc vào các yếu tố như độ phức tạp của nhiệm vụ, số lượng tác nhân, mức độ tự chủ mong muốn, nhu cầu về tính bền vững và chi phí giao tiếp chấp nhận được. Những tiến bộ trong tương lai của hệ thống đa tác nhân có thể sẽ tiếp tục khám phá và tinh chỉnh các mô hình này, cũng như phát triển các mô hình mới cho trí tuệ hợp tác.# Hands-On code (Crew AI)

This Python code defines an AI-powered crew using the CrewAI framework to generate a blog post about AI trends. Nó bắt đầu bằng cách thiết lập môi trường, tải các khóa API từ tệp .env. Cốt lõi của ứng dụng liên quan đến việc định nghĩa hai tác nhân: một nhà nghiên cứu để tìm và tóm tắt các xu hướng AI, và một người viết để tạo một bài đăng blog dựa trên nghiên cứu.Hai nhiệm vụ được định nghĩa tương ứng: một cho việc nghiên cứu các xu hướng và một cho việc viết bài đăng blog, với nhiệm vụ viết phụ thuộc vào đầu ra của nhiệm vụ nghiên cứu. Các tác nhân và nhiệm vụ này sau đó được tập hợp thành một Nhóm (Crew), chỉ định một quy trình tuần tự (sequential process) nơi các nhiệm vụ được thực hiện theo thứ tự. Nhóm được khởi tạo với các tác nhân, nhiệm vụ và một mô hình ngôn ngữ (cụ thể là mô hình "gemini-2.0-flash"). Hàm main thực thi nhóm này bằng phương thức kickoff(), điều phối sự hợp tác giữa các tác nhân để tạo ra đầu ra mong muốn. Cuối cùng, mã in ra kết quả cuối cùng của việc thực thi nhóm, đó là bài đăng blog được tạo ra.

```
import os
from typing import Optional

from dotenv import load_dotenv
from crewai import Agent, Task, Crew, Process
from langchain_google_genai import ChatGoogleGenerativeAI


def setup_environment() -> None:
    """Tải các biến môi trường và đảm bảo GOOGLE_API_KEY tồn tại."""
    load_dotenv()
    if not os.getenv("GOOGLE_API_KEY"):
        raise ValueError(
            "Không tìm thấy GOOGLE_API_KEY. Vui lòng đặt nó trong tệp .env của bạn."
        )


def main() -> None:
    """
    Khởi tạo và chạy nhóm AI để tạo nội dung bằng mô hình Gemini.
    """
    setup_environment()

    # Xác định mô hình ngôn ngữ sẽ sử dụng.
    # Cập nhật lên mô hình từ dòng Gemini 2.0 để có
    # hiệu suất và tính năng tốt hơn. Đối với các tính năng xem trước, hãy xem xét:
    #   "gemini-2.5-flash"
    llm = ChatGoogleGenerativeAI(model="gemini-2.0-flash")

    # ----- Tác nhân (Agents) -----------------------------------------------------------
    researcher = Agent(
        role="Nhà phân tích nghiên cứu cấp cao",
        goal="Tìm và tóm tắt các xu hướng mới nhất trong AI.",
        backstory=(
            "Bạn là một nhà phân tích nghiên cứu có kinh nghiệm với sở trường "
            "xác định các xu hướng chính và tổng hợp thông tin."
        ),
        verbose=True,
        allow_delegation=False,
    )

    writer = Agent(
        role="Người viết nội dung kỹ thuật",
        goal="Viết một bài đăng blog rõ ràng và hấp dẫn dựa trên các phát hiện nghiên cứu.",
        backstory=(
            "Bạn là một nhà văn lành nghề có thể chuyển các chủ đề kỹ thuật phức tạp "
            "thành nội dung dễ tiếp cận."
        ),
        verbose=True,
        allow_delegation=False,
    )

    # ----- Nhiệm vụ (Tasks) ------------------------------------------------------------
    research_task = Task(
        description=(
            "Nghiên cứu 3 xu hướng mới nổi hàng đầu trong Trí tuệ nhân tạo "
            "vào năm 2024-2025. Tập trung vào các ứng dụng thực tế và tác động tiềm tàng."
        ),
        expected_output=(
            "Một bản tóm tắt chi tiết về 3 xu hướng AI hàng đầu, bao gồm các điểm chính "
            "và nguồn."
        ),
        agent=researcher,
    )

    writing_task = Task(
        description=(
            "Viết một bài đăng blog 500 từ dựa trên các phát hiện nghiên cứu. "
            "Bài đăng phải hấp dẫn và dễ hiểu đối với khán giả phổ thông."
        ),
        expected_output="Một bài đăng blog 500 từ hoàn chỉnh về các xu hướng AI mới nhất.",
        agent=writer,
        context=[research_task],
    )

    # ----- Nhóm (Crew) -------------------------------------------------------------
    blog_creation_crew = Crew(
        agents=[researcher, writer],
        tasks=[research_task, writing_task],
        process=Process.sequential,
        llm=llm,
        verbose=2,  # Nhật ký thực thi nhóm chi tiết
    )

    # ----- Chạy (Run) --------------------------------------------------------------
    print("## Đang chạy nhóm tạo blog với Gemini 2.0 Flash... ##")
    try:
        result = blog_creation_crew.kickoff()
        print("\n------------------\n")
        print("## Đầu ra cuối cùng của Nhóm ##")
        print(result)
    except Exception as e:
        print(f"\nĐã xảy ra lỗi không mong muốn: {e}")


if __name__ == "__main__":
    main()

Bây giờ chúng ta sẽ đi sâu vào các ví dụ khác trong framework Google ADK, đặc biệt nhấn mạnh vào các mô hình phối hợp phân cấp, song song và tuần tự, cùng với việc triển khai một tác nhân như một công cụ hoạt động.

# Code thực hành (Google ADK)

Ví dụ mã sau đây minh họa việc thiết lập cấu trúc tác nhân phân cấp trong Google ADK thông qua việc tạo mối quan hệ cha-con. Đoạn mã định nghĩa hai loại tác nhân: LlmAgent và một tác nhân TaskExecutor tùy chỉnh được kế thừa từ BaseAgent. TaskExecutor được thiết kế cho các nhiệm vụ cụ thể, không phải LLM và trong ví dụ này, nó chỉ đơn giản là tạo ra một sự kiện "Task finished successfully" (Nhiệm vụ đã hoàn thành thành công). Một LlmAgent tên là greeter được khởi tạo với một mô hình và chỉ dẫn cụ thể để hoạt động như một người chào hỏi thân thiện. TaskExecutor tùy chỉnh được khởi tạo với tên task_doer. Một LlmAgent cha tên là coordinator được tạo ra, cũng với một mô hình và các chỉ dẫn. Các chỉ dẫn của coordinator hướng dẫn nó ủy thác việc chào hỏi cho greeter và thực hiện nhiệm vụ cho task_doer. greeter và task_doer được thêm vào làm tác nhân con (sub-agents) cho coordinator, thiết lập mối quan hệ cha-con. Sau đó, mã khẳng định rằng mối quan hệ này được thiết lập chính xác. Cuối cùng, nó in một thông báo cho biết hệ thống phân cấp tác nhân đã được tạo thành công.from typing import AsyncGenerator

from google.adk.agents import LlmAgent, BaseAgent
from google.adk.agents.invocation_context import InvocationContext
from google.adk.events import Event


# Thực hiện đúng một tác nhân tùy chỉnh bằng cách mở rộng BaseAgent
class TaskExecutor(BaseAgent):
    """Một tác nhân chuyên biệt với hành vi tùy chỉnh, không phải LLM."""

    name: str = "TaskExecutor"
    description: str = "Thực thi một nhiệm vụ được xác định trước."

    async def _run_async_impl(
        self, context: InvocationContext
    ) -> AsyncGenerator[Event, None]:
        """Logic triển khai tùy chỉnh cho nhiệm vụ."""
        # Đây là nơi logic tùy chỉnh của bạn sẽ được đặt.
        # Đối với ví dụ này, chúng ta sẽ chỉ tạo ra một sự kiện đơn giản.
        yield Event(author=self.name, content="Nhiệm vụ đã hoàn thành thành công.")


# Xác định các tác nhân riêng lẻ với khởi tạo phù hợp
# LlmAgent yêu cầu chỉ định một mô hình.
greeter = LlmAgent(
    name="Greeter",
    model="gemini-2.0-flash-exp",
    instruction="Bạn là một người chào hỏi thân thiện.",
)

# Khởi tạo tác nhân tùy chỉnh cụ thể của chúng ta
task_doer = TaskExecutor()

# Tạo một tác nhân cha và gán các tác nhân con của nó
# Mô tả và chỉ dẫn của tác nhân cha nên hướng dẫn logic ủy thác của nó.
coordinator = LlmAgent(
    name="Coordinator",
    model="gemini-2.0-flash-exp",
    description="Một điều phối viên có thể chào người dùng và thực hiện các nhiệm vụ.",
    instruction=(
        "Khi được yêu cầu chào, hãy ủy thác cho Greeter. "
        "Khi được yêu cầu thực hiện một nhiệm vụ, hãy ủy thác cho TaskExecutor."
    ),
    sub_agents=[greeter, task_doer],
)

# Framework ADK tự động thiết lập các mối quan hệ cha-con.
# Các khẳng định này sẽ vượt qua nếu được kiểm tra sau khi khởi tạo.
assert greeter.parent_agent == coordinator
assert task_doer.parent_agent == coordinator

print("Hệ thống phân cấp tác nhân được tạo thành công.")
Đoạn mã này minh họa việc sử dụng LoopAgent trong framework Google ADK để thiết lập các quy trình công việc lặp đi lặp lại. Đoạn mã định nghĩa hai tác nhân: ConditionChecker và ProcessingStep. ConditionChecker là một tác nhân tùy chỉnh kiểm tra giá trị "status" trong trạng thái phiên (session state). Nếu "status" là "completed" (đã hoàn thành), ConditionChecker sẽ leo thang một sự kiện để dừng vòng lặp. Nếu không, nó tạo ra một sự kiện để tiếp tục vòng lặp. ProcessingStep là một LlmAgent sử dụng mô hình "gemini-2.0-flash-exp". Chỉ dẫn của nó là thực hiện một nhiệm vụ và đặt "status" của phiên thành "completed" nếu đó là bước cuối cùng. Một LoopAgent tên là StatusPoller được tạo ra. StatusPoller được cấu hình với max_iterations=10 (tối đa 10 lần lặp). StatusPoller bao gồm cả ProcessingStep và một phiên bản của ConditionChecker làm tác nhân con. LoopAgent sẽ thực thi các tác nhân con một cách tuần tự tối đa 10 lần lặp, dừng lại nếu ConditionChecker thấy trạng thái là "completed".import asyncio
from typing import AsyncGenerator

from google.adk.agents import LoopAgent, LlmAgent, BaseAgent
from google.adk.events import Event, EventActions
from google.adk.agents.invocation_context import InvocationContext


# Thực hành tốt nhất: Định nghĩa các tác nhân tùy chỉnh dưới dạng các lớp hoàn chỉnh, tự mô tả.
class ConditionChecker(BaseAgent):
    """Một tác nhân tùy chỉnh kiểm tra trạng thái 'completed' trong trạng thái phiên."""

    name: str = "ConditionChecker"
    description: str = "Kiểm tra xem một quy trình đã hoàn tất chưa và báo hiệu cho vòng lặp dừng lại."

    async def _run_async_impl(
        self, context: InvocationContext
    ) -> AsyncGenerator[Event, None]:
        """Kiểm tra trạng thái và tạo ra một sự kiện để tiếp tục hoặc dừng vòng lặp."""
        status = context.session.state.get("status", "pending")
        is_done = (status == "completed")

        if is_done:
            # Leo thang để chấm dứt vòng lặp khi điều kiện được đáp ứng.
            yield Event(author=self.name, actions=EventActions(escalate=True))
        else:
            # Tạo ra một sự kiện đơn giản để tiếp tục vòng lặp.
            yield Event(
                author=self.name,
                content="Điều kiện chưa được đáp ứng, tiếp tục vòng lặp."
            )


# --------------------------------------------------------------------------
# Định nghĩa Tác nhân
# --------------------------------------------------------------------------

# Sửa lỗi: LlmAgent phải có một mô hình và các chỉ dẫn rõ ràng.
process_step = LlmAgent(
    name="ProcessingStep",
    model="gemini-2.0-flash-exp",
    instruction=(
        "Bạn là một bước trong một quy trình dài hơn. Hãy thực hiện nhiệm vụ của mình. "
        "Nếu bạn là bước cuối cùng, hãy cập nhật trạng thái phiên bằng cách "
        "đặt 'status' thành 'completed'."
    ),
)

# LoopAgent điều phối quy trình công việc.
poller = LoopAgent(
    name="StatusPoller",
    max_iterations=10,
    sub_agents=[
        process_step,
        ConditionChecker(),  # Khởi tạo tác nhân tùy chỉnh được xác định rõ ràng
    ],
)

# --------------------------------------------------------------------------
# Ghi chú thực thi:
# --------------------------------------------------------------------------
# Bộ thăm dò (poller) này bây giờ sẽ thực thi 'process_step'
# và sau đó là 'ConditionChecker'
# lặp đi lặp lại cho đến khi trạng thái là 'completed'
# hoặc đã qua 10 lần lặp.
Đoạn mã này làm sáng tỏ mẫu SequentialAgent trong Google ADK, được thiết kế để xây dựng các quy trình công việc tuyến tính. Đoạn mã này định nghĩa một quy trình tác nhân tuần tự bằng cách sử dụng thư viện google.adk.agents. Quy trình bao gồm hai tác nhân, step1 và step2. step1 có tên là "Step1_Fetch" và đầu ra của nó sẽ được lưu trữ trong trạng thái phiên dưới khóa "data". step2 có tên là "Step2_Process" và được hướng dẫn phân tích thông tin được lưu trữ trong session.state$$"data"$$ và cung cấp một bản tóm tắt. SequentialAgent có tên "MyPipeline" điều phối việc thực thi các tác nhân con này. Khi quy trình được chạy với một đầu vào ban đầu, step1 sẽ thực thi trước. Phản hồi từ step1 sẽ được lưu vào trạng thái phiên dưới khóa "data". Sau đó, step2 sẽ thực thi, sử dụng thông tin mà step1 đã đặt vào trạng thái theo chỉ dẫn của nó. Cấu trúc này cho phép xây dựng các quy trình công việc trong đó đầu ra của một tác nhân trở thành đầu vào cho tác nhân tiếp theo. Đây là một mẫu phổ biến trong việc tạo ra các quy trình xử lý dữ liệu hoặc AI nhiều bước.from google.adk.agents import SequentialAgent, Agent

# --------------------------------------------------------------------------
# Định nghĩa Tác nhân
# --------------------------------------------------------------------------

# Bước 1: Đầu ra của tác nhân này sẽ được lưu vào session.state["data"]
step1 = Agent(
    name="Step1_Fetch",
    output_key="data",
)

# Bước 2: Tác nhân này sẽ sử dụng dữ liệu từ bước trước.
# Chúng ta hướng dẫn nó cách tìm và sử dụng dữ liệu này.
step2 = Agent(
    name="Step2_Process",
    instruction="Phân tích thông tin được tìm thấy trong state['data'] và cung cấp một bản tóm tắt.",
)

# --------------------------------------------------------------------------
# Định nghĩa Quy trình (Pipeline)
# --------------------------------------------------------------------------

pipeline = SequentialAgent(
    name="MyPipeline",
    sub_agents=[step1, step2],
)

# --------------------------------------------------------------------------
# Ghi chú thực thi
# --------------------------------------------------------------------------
# Khi quy trình được chạy với một đầu vào ban đầu:
# 1. Step1 sẽ thực thi, và phản hồi của nó sẽ được lưu trữ trong session.state["data"].
# 2. Step2 sẽ thực thi tiếp theo, sử dụng thông tin từ trạng thái như đã được hướng dẫn.
Ví dụ mã sau đây minh họa mẫu ParallelAgent trong Google ADK, tạo điều kiện cho việc thực thi đồng thời nhiều nhiệm vụ của tác nhân. data_gatherer được thiết kế để chạy hai tác nhân con đồng thời: weather_fetcher và news_fetcher. Tác nhân weather_fetcher được hướng dẫn lấy thời tiết cho một vị trí nhất định và lưu trữ kết quả trong session.state$$"weather\_data"$$. Tương tự, tác nhân news_fetcher được hướng dẫn truy xuất tin bài hàng đầu cho một chủ đề nhất định và lưu trữ nó trong session.state$$"news\_data"$$. Mỗi tác nhân con được cấu hình để sử dụng mô hình "gemini-2.0-flash-exp". ParallelAgent điều phối việc thực thi các tác nhân con này, cho phép chúng hoạt động song song. Kết quả từ cả weather_fetcher và news_fetcher sẽ được thu thập và lưu trữ trong trạng thái phiên. Cuối cùng, ví dụ cho thấy cách truy cập dữ liệu thời tiết và tin tức đã thu thập từ final_state sau khi quá trình thực thi của tác nhân hoàn tất.from google.adk.agents import Agent, ParallelAgent

# --------------------------------------------------------------------------
# Định nghĩa các Tác nhân Riêng lẻ
# --------------------------------------------------------------------------

# Tốt hơn là định nghĩa logic tìm nạp (fetching) làm công cụ cho các tác nhân.
# Để đơn giản trong ví dụ này, chúng ta sẽ nhúng logic trực tiếp
# vào chỉ dẫn của tác nhân. Trong một kịch bản thực tế, bạn sẽ sử dụng các công cụ.

weather_fetcher = Agent(
    name="weather_fetcher",
    model="gemini-2.0-flash-exp",
    instruction=(
        "Tìm nạp thời tiết cho vị trí đã cho và chỉ trả về "
        "báo cáo thời tiết."
    ),
    output_key="weather_data",  # Được lưu trữ trong session.state["weather_data"]
)

news_fetcher = Agent(
    name="news_fetcher",
    model="gemini-2.0-flash-exp",
    instruction=(
        "Tìm nạp tin bài hàng đầu cho chủ đề đã cho và chỉ trả về tin bài đó."
    ),
    output_key="news_data",  # Được lưu trữ trong session.state["news_data"]
)

# --------------------------------------------------------------------------
# Tác nhân Điều phối
# --------------------------------------------------------------------------

# ParallelAgent sẽ chạy các tác nhân con song song.
data_gatherer = ParallelAgent(
    name="data_gatherer",
    sub_agents=[
        weather_fetcher,
        news_fetcher,
    ],
)

# --------------------------------------------------------------------------
# Ghi chú thực thi
# --------------------------------------------------------------------------
# Khi được thực thi, cả `weather_fetcher` và `news_fetcher` sẽ chạy song song.
# Đầu ra của chúng sẽ được lưu trữ trong trạng thái phiên dưới "weather_data"
# và "news_data". ParallelAgent quản lý việc đồng bộ hóa.
Đoạn mã được cung cấp minh họa mô hình "Tác nhân như một Công cụ" (Agent as a Tool) trong Google ADK, cho phép một tác nhân sử dụng khả năng của một tác nhân khác theo cách tương tự như lời gọi hàm. Cụ thể, mã định nghĩa một hệ thống tạo hình ảnh bằng cách sử dụng các lớp LlmAgent và AgentTool của Google. Nó bao gồm hai tác nhân: một artist_agent (tác nhân nghệ sĩ) cha và một image_generator_agent (tác nhân tạo hình ảnh) con. Hàm generate_image là một công cụ đơn giản mô phỏng việc tạo hình ảnh, trả về dữ liệu hình ảnh giả (mock). image_generator_agent chịu trách nhiệm sử dụng công cụ này dựa trên một lời nhắc văn bản (text prompt) mà nó nhận được. Vai trò của artist_agent là đầu tiên phát minh ra một lời nhắc hình ảnh sáng tạo. Sau đó, nó gọi image_generator_agent thông qua một trình bao (wrapper) AgentTool. AgentTool hoạt động như một cầu nối, cho phép một tác nhân sử dụng tác nhân khác như một công cụ. Khi artist_agent gọi image_tool, AgentTool sẽ gọi image_generator_agent với lời nhắc do nghệ sĩ phát minh. Sau đó, image_generator_agent sử dụng hàm generate_image với lời nhắc đó. Cuối cùng, hình ảnh được tạo (hoặc dữ liệu giả) được trả về ngược lên qua các tác nhân. Kiến trúc này minh họa một hệ thống tác nhân phân lớp, nơi một tác nhân cấp cao hơn điều phối một tác nhân cấp thấp hơn, chuyên biệt để thực hiện một nhiệm vụ.from typing import Any, Dict

from google.adk.agents import LlmAgent
from google.adk.tools import agent_tool
# from google.genai import types  # Import không được sử dụng đã bị xóa; giữ lại nếu bạn sử dụng Part/Blob sau này.

# -----------------------------------------------------------------------------
# 1) Công cụ hàm đơn giản (tách biệt hành động khỏi suy luận)
# -----------------------------------------------------------------------------
def generate_image(prompt: str) -> Dict[str, Any]:
    """
    Tạo hình ảnh dựa trên lời nhắc văn bản.

    Args:
        prompt: Mô tả chi tiết về hình ảnh cần tạo.

    Returns:
        Một từ điển với trạng thái và các byte hình ảnh được tạo.
    """
    print(f"CÔNG CỤ: Đang tạo hình ảnh cho lời nhắc: '{prompt}'")

    # Trong một triển khai thực tế, hãy gọi API tạo hình ảnh của bạn ở đây.
    # Đối với ví dụ này, chúng tôi trả về dữ liệu hình ảnh giả.
    mock_image_bytes = b"mock_image_data_for_a_cat_wearing_a_hat"

    return {
        "status": "success",
        # Công cụ trả về các byte thô; tác nhân sẽ xử lý việc tạo Part.
        "image_bytes": mock_image_bytes,
        "mime_type": "image/png",
    }


# -----------------------------------------------------------------------------
# 2) ImageGeneratorAgent là một LlmAgent sử dụng công cụ ở trên
# -----------------------------------------------------------------------------
image_generator_agent = LlmAgent(
    name="ImageGen",
    model="gemini-2.0-flash",
    description="Tạo hình ảnh dựa trên lời nhắc văn bản chi tiết.",
    instruction=(
        "Bạn là chuyên gia tạo hình ảnh. Nhiệm vụ của bạn là nhận yêu cầu của người dùng "
        "và sử dụng công cụ `generate_image` để tạo hình ảnh. Toàn bộ "
        "yêu cầu của người dùng nên được sử dụng làm đối số 'prompt' cho công cụ. "
        "Sau khi công cụ trả về các byte hình ảnh, bạn PHẢI xuất hình ảnh."
    ),
    tools=[generate_image],
)


# -----------------------------------------------------------------------------
# 3) Bao bọc tác nhân trong một AgentTool (thứ mà tác nhân cha sẽ gọi)
# -----------------------------------------------------------------------------
image_tool = agent_tool.AgentTool(
    agent=image_generator_agent,
    description=(
        "Sử dụng công cụ này để tạo hình ảnh. Đầu vào phải là một lời nhắc mô tả "
        "về hình ảnh mong muốn."
    ),
)


# -----------------------------------------------------------------------------
# 4) Tác nhân cha (điều phối viên) phát minh ra một lời nhắc và gọi ImageGen
# -----------------------------------------------------------------------------
artist_agent = LlmAgent(
    name="Artist",
    model="gemini-2.0-flash",
    instruction=(
        "Bạn là một nghệ sĩ sáng tạo. Đầu tiên, hãy phát minh ra một lời nhắc sáng tạo và mô tả "
        "cho một hình ảnh. Sau đó, sử dụng công cụ `ImageGen` để tạo "
        "hình ảnh bằng lời nhắc của bạn."
    ),
    tools=[image_tool],
)
# Sơ lược

**Cái gì:** Các vấn đề phức tạp thường vượt quá khả năng của một tác nhân dựa trên LLM đơn lẻ, nguyên khối. Một tác nhân đơn độc có thể thiếu các kỹ năng chuyên biệt, đa dạng hoặc quyền truy cập vào các công cụ cụ thể cần thiết để giải quyết tất cả các phần của một nhiệm vụ nhiều mặt. Hạn chế này tạo ra một điểm nghẽn, làm giảm hiệu quả tổng thể và khả năng mở rộng của hệ thống. Do đó, việc giải quyết các mục tiêu phức tạp, đa lĩnh vực trở nên không hiệu quả và có thể dẫn đến kết quả không đầy đủ hoặc dưới mức tối ưu.

**Tại sao:** Mẫu Hợp tác Đa Tác nhân cung cấp một giải pháp tiêu chuẩn hóa bằng cách tạo ra một hệ thống gồm nhiều tác nhân hợp tác. Một vấn đề phức tạp được chia thành các bài toán con nhỏ hơn, dễ quản lý hơn. Mỗi bài toán con sau đó được giao cho một tác nhân chuyên biệt với các công cụ và khả năng chính xác cần thiết để giải quyết nó. Các tác nhân này làm việc cùng nhau thông qua các giao thức truyền thông và mô hình tương tác được xác định như chuyển giao tuần tự, luồng công việc song song hoặc ủy thác phân cấp. Cách tiếp cận phân tán, mang tính tác nhân này tạo ra hiệu ứng tổng hợp, cho phép nhóm đạt được các kết quả mà bất kỳ tác nhân đơn lẻ nào cũng không thể thực hiện được.

**Quy tắc chung:** Sử dụng mẫu này khi một nhiệm vụ quá phức tạp đối với một tác nhân đơn lẻ và có thể được phân rã thành các nhiệm vụ con riêng biệt đòi hỏi các kỹ năng hoặc công cụ chuyên biệt. Nó lý tưởng cho các vấn đề được hưởng lợi từ chuyên môn đa dạng, xử lý song song hoặc một quy trình công việc có cấu trúc với nhiều giai đoạn, chẳng hạn như nghiên cứu và phân tích phức tạp, phát triển phần mềm hoặc tạo nội dung sáng tạo.

**Tóm tắt trực quan**

<figure>
<img src="../imgs/fig.7.3.Multi-Agent_design_pattern.png" alt="Hình 3: Mẫu thiết kế Đa Tác nhân">
<figcaption>
Hình 3: Mẫu thiết kế Đa Tác nhân
</figcaption>
</figure># Điểm mấu chốt

* Hợp tác đa tác nhân liên quan đến nhiều tác nhân làm việc cùng nhau để đạt được một mục tiêu chung.  
* Mẫu này tận dụng các vai trò chuyên biệt, các nhiệm vụ phân tán và giao tiếp giữa các tác nhân.  
* Sự hợp tác có thể diễn ra dưới các hình thức như chuyển giao tuần tự, xử lý song song, tranh luận hoặc cấu trúc phân cấp.  
* Mẫu này lý tưởng cho các vấn đề phức tạp đòi hỏi chuyên môn đa dạng hoặc nhiều giai đoạn riêng biệt.# Kết luận

Chương này đã khám phá mẫu Hợp tác Đa Tác nhân, chứng minh những lợi ích của việc điều phối nhiều tác nhân chuyên biệt trong các hệ thống. Chúng tôi đã kiểm tra các mô hình hợp tác khác nhau, nhấn mạnh vai trò thiết yếu của mẫu trong việc giải quyết các vấn đề phức tạp, nhiều mặt trên các lĩnh vực đa dạng. Hiểu biết về sự hợp tác của tác nhân một cách tự nhiên dẫn đến một cuộc điều tra về sự tương tác của chúng với môi trường bên ngoài.# Tài liệu tham khảo

1. Multi-Agent Collaboration Mechanisms: A Survey of LLMs, [https://arxiv.org/abs/2501.06322](https://arxiv.org/abs/2501.06322)   
2. Hệ thống Đa Tác nhân — Sức mạnh của sự Hợp tác, https://aravindakumar.medium.com/introducing-multi-agent-frameworks-the-power-of-collaboration-e9db31bba1b6