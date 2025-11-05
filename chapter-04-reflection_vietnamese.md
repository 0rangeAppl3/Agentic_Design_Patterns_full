Dạ vâng sếp, dưới đây là bản dịch tiếng Việt của tài liệu sếp đã cung cấp ạ:
Chương 4: Phản tư (Reflection)
Tổng quan về Mẫu Phản tư
Trong các chương trước, chúng ta đã khám phá các mẫu tác nhân (agentic pattern) cơ bản: Nối chuỗi (Chaining) để thực thi tuần tự, Định tuyến (Routing) để lựa chọn đường dẫn động, và Song song hóa (Parallelization) để thực thi tác vụ đồng thời. Những mẫu này cho phép các tác nhân thực hiện các tác vụ phức tạp một cách hiệu quả và linh hoạt hơn. Tuy nhiên, ngay cả với các quy trình công việc phức tạp, đầu ra hoặc kế hoạch ban đầu của một tác nhân có thể không phải là tối ưu, chính xác hoặc hoàn chỉnh. Đây là lúc mẫu Phản tư (Reflection) phát huy tác dụng.
Mẫu Phản tư liên quan đến việc một tác nhân tự đánh giá công việc, đầu ra hoặc trạng thái nội tại của chính nó và sử dụng đánh giá đó để cải thiện hiệu suất hoặc tinh chỉnh phản hồi của mình. Đó là một hình thức tự điều chỉnh hoặc tự cải thiện, cho phép tác nhân tinh chỉnh lặp đi lặp lại đầu ra của mình hoặc điều chỉnh cách tiếp cận dựa trên phản hồi, phê bình nội bộ, hoặc so sánh với các tiêu chí mong muốn. Đôi khi, việc phản tư có thể được hỗ trợ bởi một tác nhân riêng biệt có vai trò cụ thể là phân tích đầu ra của tác nhân ban đầu.
Không giống như một chuỗi tuần tự đơn giản nơi đầu ra được chuyển trực tiếp đến bước tiếp theo, hoặc định tuyến lựa chọn một đường dẫn, phản tư giới thiệu một vòng lặp phản hồi. Tác nhân không chỉ tạo ra một đầu ra; nó sau đó kiểm tra đầu ra đó (hoặc quá trình tạo ra nó), xác định các vấn đề tiềm ẩn hoặc các lĩnh vực cần cải thiện, và sử dụng những hiểu biết đó để tạo ra một phiên bản tốt hơn hoặc sửa đổi các hành động trong tương lai của mình.
Quá trình này thường bao gồm:
1. Thực thi: Tác nhân thực hiện một tác vụ hoặc tạo ra một đầu ra ban đầu.
2. Đánh giá/Phê bình: Tác nhân (thường sử dụng một lệnh gọi LLM khác hoặc một bộ quy tắc) phân tích kết quả từ bước trước. Đánh giá này có thể kiểm tra tính chính xác của dữ kiện, sự mạch lạc, văn phong, tính đầy đủ, tuân thủ hướng dẫn, hoặc các tiêu chí liên quan khác.
3. Phản tư/Tinh chỉnh: Dựa trên sự phê bình, tác nhân xác định cách cải thiện. Điều này có thể bao gồm việc tạo ra một đầu ra đã được tinh chỉnh, điều chỉnh các tham số cho một bước tiếp theo, hoặc thậm chí sửa đổi kế hoạch tổng thể.
4. Lặp lại (Tùy chọn nhưng phổ biến): Đầu ra đã được tinh chỉnh hoặc cách tiếp cận đã được điều chỉnh sau đó có thể được thực thi, và quá trình phản tư có thể lặp lại cho đến khi đạt được kết quả thỏa đáng hoặc một điều kiện dừng được đáp ứng.
Một cách triển khai quan trọng và rất hiệu quả của mẫu Phản tư là tách quá trình thành hai vai trò logic riêng biệt: một Tác nhân Sản xuất (Producer) và một Tác nhân Phê bình (Critic). Điều này thường được gọi là mô hình "Tạo sinh-Phê bình" (Generator-Critic) hoặc "Sản xuất-Đánh giá" (Producer-Reviewer). Mặc dù một tác nhân duy nhất có thể tự phản tư, việc sử dụng hai tác nhân chuyên biệt (hoặc hai lệnh gọi LLM riêng biệt với các chỉ thị hệ thống (system prompt) khác nhau) thường mang lại kết quả mạnh mẽ và khách quan hơn.
1. Tác nhân Sản xuất (Producer Agent): Trách nhiệm chính của tác nhân này là thực hiện việc thực thi ban đầu của tác vụ. Nó hoàn toàn tập trung vào việc tạo ra nội dung, cho dù đó là viết mã, soạn thảo một bài đăng blog, hay tạo một kế hoạch. Nó nhận chỉ thị ban đầu và tạo ra phiên bản đầu tiên của đầu ra.
2. Tác nhân Phê bình (Critic Agent): Mục đích duy nhất của tác nhân này là đánh giá đầu ra do Tác nhân Sản xuất tạo ra. Nó được cung cấp một bộ hướng dẫn khác, thường là một vai trò (persona) riêng biệt (ví dụ: "Bạn là một kỹ sư phần mềm cấp cao," "Bạn là một người kiểm tra dữ kiện tỉ mỉ"). Hướng dẫn của Tác nhân Phê bình chỉ đạo nó phân tích công việc của Tác nhân Sản xuất dựa trên các tiêu chí cụ thể, chẳng hạn như tính chính xác của dữ kiện, chất lượng mã, yêu cầu về văn phong, hoặc tính đầy đủ. Nó được thiết kế để tìm ra các sai sót, đề xuất cải tiến, và cung cấp phản hồi có cấu trúc.
Việc tách biệt các mối quan tâm này rất mạnh mẽ vì nó ngăn chặn "thiên kiến nhận thức" (cognitive bias) của một tác nhân tự xem xét công việc của chính mình. Tác nhân Phê bình tiếp cận đầu ra với một góc nhìn mới, hoàn toàn chuyên tâm vào việc tìm kiếm lỗi và các lĩnh vực cần cải thiện. Phản hồi từ Tác nhân Phê bình sau đó được chuyển lại cho Tác nhân Sản xuất, tác nhân này sử dụng nó như một hướng dẫn để tạo ra một phiên bản mới, đã được tinh chỉnh của đầu ra. Các ví dụ mã nguồn LangChain và ADK được cung cấp đều triển khai mô hình hai tác nhân này: ví dụ LangChain sử dụng một "reflector_prompt" (chỉ thị cho tác nhân phản tư) cụ thể để tạo ra một vai trò phê bình, trong khi ví dụ ADK định nghĩa rõ ràng một tác nhân sản xuất và một tác nhân đánh giá.
Việc triển khai phản tư thường đòi hỏi cấu trúc quy trình làm việc của tác nhân để bao gồm các vòng lặp phản hồi này. Điều này có thể đạt được thông qua các vòng lặp lặp đi lặp lại trong mã, hoặc sử dụng các framework hỗ trợ quản lý trạng thái và chuyển đổi có điều kiện dựa trên kết quả đánh giá. Mặc dù một bước đánh giá và tinh chỉnh duy nhất có thể được triển khai bên trong một chuỗi LangChain/LangGraph, ADK, hoặc Crew.AI, việc phản tư lặp đi lặp lại thực sự thường liên quan đến sự phối hợp phức tạp hơn.
Mẫu Phản tư rất quan trọng để xây dựng các tác nhân có thể tạo ra các đầu ra chất lượng cao, xử lý các tác vụ phức tạp, và thể hiện một mức độ tự nhận thức và khả năng thích ứng. Nó đưa các tác nhân vượt ra ngoài việc chỉ đơn thuần thực thi hướng dẫn để hướng tới một hình thức giải quyết vấn đề và tạo nội dung tinh vi hơn.
Sự giao thoa của phản tư với việc thiết lập và giám sát mục tiêu (xem Chương 11) là điều đáng chú ý. Một mục tiêu cung cấp tiêu chuẩn cuối cùng cho việc tự đánh giá của tác nhân, trong khi việc giám sát theo dõi tiến trình của nó. Trong một số trường hợp thực tế, Phản tư sau đó có thể hoạt động như một cỗ máy điều chỉnh, sử dụng phản hồi được giám sát để phân tích các sai lệch và điều chỉnh chiến lược của mình. Sự phối hợp này biến đổi tác nhân từ một người thực thi thụ động thành một hệ thống có mục đích, hoạt động một cách thích ứng để đạt được các mục tiêu của mình.
Hơn nữa, hiệu quả của mẫu Phản tư được tăng cường đáng kể khi LLM giữ một bộ nhớ của cuộc hội thoại (xem Chương 8). Lịch sử hội thoại này cung cấp bối cảnh quan trọng cho giai đoạn đánh giá, cho phép tác nhân đánh giá đầu ra của mình không chỉ một cách biệt lập, mà còn trong bối cảnh của các tương tác trước đó, phản hồi của người dùng, và các mục tiêu đang phát triển. Nó cho phép tác nhân học hỏi từ những phê bình trong quá khứ và tránh lặp lại các lỗi. Không có bộ nhớ, mỗi lần phản tư là một sự kiện độc lập; với bộ nhớ, phản tư trở thành một quá trình tích lũy nơi mỗi chu kỳ xây dựng dựa trên chu kỳ trước, dẫn đến sự tinh chỉnh thông minh và nhận thức bối cảnh tốt hơn.
Ứng dụng Thực tế & Trường hợp Sử dụng
Mẫu Phản tư có giá trị trong các kịch bản mà chất lượng đầu ra, tính chính xác, hoặc tuân thủ các ràng buộc phức tạp là rất quan trọng:
1. Viết Sáng tạo và Tạo nội dung: Tinh chỉnh văn bản, câu chuyện, thơ, hoặc nội dung tiếp thị được tạo ra.
• Trường hợp Sử dụng: Một tác nhân viết một bài đăng blog.
• Phản tư: Tạo một bản nháp, phê bình nó về dòng chảy, giọng điệu, và sự rõ ràng, sau đó viết lại dựa trên sự phê bình. Lặp lại cho đến khi bài đăng đạt tiêu chuẩn chất lượng.
• Lợi ích: Tạo ra nội dung trau chuốt và hiệu quả hơn.
2. Tạo mã và Gỡ lỗi: Viết mã, xác định lỗi, và sửa chúng.
• Trường hợp Sử dụng: Một tác nhân viết một hàm Python.
• Phản tư: Viết mã ban đầu, chạy kiểm thử hoặc phân tích tĩnh, xác định lỗi hoặc sự thiếu hiệu quả, sau đó sửa đổi mã dựa trên các phát hiện.
• Lợi ích: Tạo ra mã mạnh mẽ và hoạt động tốt hơn.
3. Giải quyết Vấn đề Phức tạp: Đánh giá các bước trung gian hoặc các giải pháp được đề xuất trong các tác vụ suy luận nhiều bước.
• Trường hợp Sử dụng: Một tác nhân giải một câu đố logic.
• Phản tư: Đề xuất một bước, đánh giá xem nó có dẫn đến gần hơn với giải pháp hay gây ra mâu thuẫn không, quay lui hoặc chọn một bước khác nếu cần.
• Lợi ích: Cải thiện khả năng của tác nhân trong việc điều hướng các không gian vấn đề phức tạp.
4. Tóm tắt và Tổng hợp Thông tin: Tinh chỉnh các bản tóm tắt để đảm bảo tính chính xác, đầy đủ, và súc tích.
• Trường hợp Sử dụng: Một tác nhân tóm tắt một tài liệu dài.
• Phản tư: Tạo một bản tóm tắt ban đầu, so sánh nó với các điểm chính trong tài liệu gốc, tinh chỉnh bản tóm tắt để bao gồm thông tin còn thiếu hoặc cải thiện tính chính xác.
• Lợi ích: Tạo ra các bản tóm tắt chính xác và toàn diện hơn.
5. Lập kế hoạch và Chiến lược: Đánh giá một kế hoạch được đề xuất và xác định các sai sót hoặc cải tiến tiềm năng.
• Trường hợp Sử dụng: Một tác nhân lập kế hoạch một loạt các hành động để đạt được một mục tiêu.
• Phản tư: Tạo một kế hoạch, mô phỏng việc thực thi của nó hoặc đánh giá tính khả thi của nó so với các ràng buộc, sửa đổi kế hoạch dựa trên đánh giá.
• Lợi ích: Phát triển các kế hoạch hiệu quả và thực tế hơn.
6. Tác nhân Hội thoại: Xem xét các lượt nói trước đó trong một cuộc hội thoại để duy trì bối cảnh, sửa chữa hiểu lầm, hoặc cải thiện chất lượng phản hồi.
• Trường hợp Sử dụng: Một chatbot hỗ trợ khách hàng.
• Phản tư: Sau một phản hồi của người dùng, xem xét lịch sử hội thoại và tin nhắn được tạo ra cuối cùng để đảm bảo sự mạch lạc và giải quyết chính xác đầu vào mới nhất của người dùng.
• Lợi ích: Dẫn đến các cuộc hội thoại tự nhiên và hiệu quả hơn.
Phản tư thêm một lớp siêu nhận thức (meta-cognition) vào các hệ thống tác nhân, cho phép chúng học hỏi từ chính các đầu ra và quy trình của mình, dẫn đến các kết quả thông minh hơn, đáng tin cậy hơn, và chất lượng cao hơn.
Ví dụ Mã nguồn Thực hành (LangChain)
Việc triển khai một quy trình phản tư lặp đi lặp lại hoàn chỉnh đòi hỏi các cơ chế để quản lý trạng thái và thực thi theo chu kỳ. Mặc dù những điều này được xử lý tự nhiên trong các framework dựa trên đồ thị như LangGraph hoặc thông qua mã thủ tục tùy chỉnh, nguyên tắc cơ bản của một chu kỳ phản tư duy nhất có thể được minh họa một cách hiệu quả bằng cách sử dụng cú pháp kết hợp của LCEL (Ngôn ngữ Biểu thức LangChain).
Ví dụ này triển khai một vòng lặp phản tư bằng cách sử dụng thư viện Langchain và mô hình GPT-4o của OpenAI để tạo và tinh chỉnh lặp đi lặp lại một hàm Python tính giai thừa của một số. Quá trình bắt đầu với một chỉ thị tác vụ, tạo mã ban đầu, và sau đó liên tục phản tư về mã dựa trên các phê bình từ một vai trò kỹ sư phần mềm cấp cao mô phỏng, tinh chỉnh mã trong mỗi lần lặp cho đến khi giai đoạn phê bình xác định mã là hoàn hảo hoặc đạt đến số lần lặp tối đa. Cuối cùng, nó in ra mã đã được tinh chỉnh kết quả.
Đầu tiên, hãy đảm bảo bạn đã cài đặt các thư viện cần thiết:
pip install langchain langchain-community langchain-openai
Bạn cũng sẽ cần thiết lập môi trường của mình với khóa API cho mô hình ngôn ngữ bạn chọn (ví dụ: OpenAI, Google Gemini, Anthropic).
import os
from dotenv import load_dotenv
from langchain_openai import ChatOpenAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.messages import SystemMessage, HumanMessage


# --- Cấu hình ---

# Tải các biến môi trường từ tệp .env (cho OPENAI_API_KEY)
load_dotenv()

# Kiểm tra xem khóa API đã được thiết lập chưa
if not os.getenv("OPENAI_API_KEY"):
    raise ValueError("Không tìm thấy OPENAI_API_KEY trong tệp .env. Vui lòng thêm nó.")

# Khởi tạo Chat LLM. Chúng ta sử dụng gpt-4o để suy luận tốt hơn.
# Sử dụng nhiệt độ (temperature) thấp hơn để có các đầu ra xác định hơn.
llm = ChatOpenAI(model="gpt-4o", temperature=0.1)


def run_reflection_loop():
    """
    Minh họa một vòng lặp phản tư AI nhiều bước để cải thiện dần dần một hàm Python.
    """

    # --- Tác vụ Cốt lõi ---
    task_prompt = """
    Nhiệm vụ của bạn là tạo một hàm Python tên là `calculate_factorial`.
    Hàm này nên thực hiện những điều sau:
    1. Chấp nhận một số nguyên `n` duy nhất làm đầu vào.
    2. Tính giai thừa của nó (n!).
    3. Bao gồm một docstring rõ ràng giải thích hàm làm gì.
    4. Xử lý các trường hợp biên: Giai thừa của 0 là 1.
    5. Xử lý đầu vào không hợp lệ: Ném ra một ValueError nếu đầu vào là một số âm.
    """

    # --- Vòng lặp Phản tư ---
    max_iterations = 3
    current_code = ""

    # Chúng ta sẽ xây dựng một lịch sử hội thoại để cung cấp bối cảnh trong mỗi bước.
    message_history = [HumanMessage(content=task_prompt)]

    for i in range(max_iterations):
        print("\n" + "=" * 25 + f" VÒNG LẶP PHẢN TƯ: LẦN LẶP {i + 1} " + "=" * 25)


        # --- 1. GIAI ĐOẠN TẠO / TINH CHỈNH ---
        # Trong lần lặp đầu tiên, nó tạo ra. Trong các lần lặp tiếp theo, nó tinh chỉnh.
        if i == 0:
            print("\n>>> GIAI ĐOẠN 1: TẠO mã ban đầu...")
            # Tin nhắn đầu tiên chỉ là chỉ thị tác vụ.
            response = llm.invoke(message_history)
            current_code = response.content
        else:
            print("\n>>> GIAI ĐOẠN 1: TINH CHỈNH mã dựa trên phê bình trước đó...")
            # Lịch sử tin nhắn bây giờ chứa tác vụ,
            # mã cuối cùng, và phê bình cuối cùng.
            # Chúng ta hướng dẫn mô hình áp dụng các phê bình.
            message_history.append(
                HumanMessage(content="Vui lòng tinh chỉnh mã bằng cách sử dụng các phê bình được cung cấp.")
            )
            response = llm.invoke(message_history)
            current_code = response.content

        print("\n--- Mã được tạo (v" + str(i + 1) + ") ---\n" + current_code)
        message_history.append(response)  # Thêm mã được tạo vào lịch sử


        # --- 2. GIAI ĐOẠN PHẢN TƯ ---
        print("\n>>> GIAI ĐOẠN 2: PHẢN TƯ về mã được tạo...")


        # Tạo một chỉ thị cụ thể cho tác nhân phản tư.
        # Điều này yêu cầu mô hình hoạt động như một người đánh giá mã cấp cao.
        reflector_prompt = [
            SystemMessage(
                content="""
                Bạn là một kỹ sư phần mềm cấp cao và là một chuyên gia
                về Python.
                Vai trò của bạn là thực hiện một đánh giá mã tỉ mỉ.
                Đánh giá một cách nghiêm túc mã Python được cung cấp dựa
                trên các yêu cầu tác vụ ban đầu.
                Tìm kiếm lỗi, vấn đề về văn phong, các trường hợp biên còn thiếu,
                và các lĩnh vực cần cải thiện.
                Nếu mã là hoàn hảo và đáp ứng tất cả các yêu cầu,
                hãy phản hồi bằng một cụm từ duy nhất 'CODE_IS_PERFECT'.
                Nếu không, hãy cung cấp một danh sách gạch đầu dòng về các phê bình của bạn.
                """
            ),
            HumanMessage(
                content=f"Tác vụ Gốc:
{task_prompt}

Mã cần Đánh giá:
{current_code}"
            ),
        ]

        critique_response = llm.invoke(reflector_prompt)
        critique = critique_response.content


        # --- 3. ĐIỀU KIỆN DỪNG ---
        if "CODE_IS_PERFECT" in critique:
            print("\n--- Phê bình ---\nKhông tìm thấy phê bình nào thêm. Mã đã đạt yêu cầu.")
            break


        print("\n--- Phê bình ---\n" + critique)


        # Thêm phê bình vào lịch sử cho vòng lặp tinh chỉnh tiếp theo.
        message_history.append(HumanMessage(content=f"Phê bình về mã trước đó:
{critique}"))

    print("\n" + "=" * 30 + " KẾT QUẢ CUỐI CÙNG " + "=" * 30)
    print("\nMã được tinh chỉnh cuối cùng sau quá trình phản tư:\n")
    print(current_code)


if __name__ == "__main__":
    run_reflection_loop()

