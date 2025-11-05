# Chương 3: Song song hóa

# Tổng quan về mẫu song song hóa

Trong các chương trước, chúng ta đã khám phá Chuỗi nhắc (Prompt Chaining) cho các quy trình làm việc tuần tự và Định tuyến (Routing) cho việc ra quyết định động và chuyển đổi giữa các đường dẫn khác nhau. Mặc dù các mẫu này rất cần thiết, nhiều tác vụ tác nhân phức tạp liên quan đến nhiều tác vụ con có thể được thực hiện *đồng thời* thay vì lần lượt. Đây là lúc mẫu **Song song hóa** trở nên quan trọng.

Song song hóa liên quan đến việc thực thi nhiều thành phần, chẳng hạn như các lệnh gọi LLM, việc sử dụng công cụ hoặc thậm chí toàn bộ tác nhân con, đồng thời (xem Hình 1). Thay vì chờ một bước hoàn thành trước khi bắt đầu bước tiếp theo, việc thực thi song song cho phép các tác vụ độc lập chạy cùng lúc, giảm đáng kể thời gian thực thi tổng thể cho các tác vụ có thể được chia thành các phần độc lập.

Hãy xem xét một tác nhân được thiết kế để nghiên cứu một chủ đề và tóm tắt các phát hiện của nó. Một cách tiếp cận tuần tự có thể là:

1. Tìm kiếm Nguồn A.  
2. Tóm tắt Nguồn A.  
3. Tìm kiếm Nguồn B.  
4. Tóm tắt Nguồn B.  
5. Tổng hợp câu trả lời cuối cùng từ các bản tóm tắt A và B.

Thay vào đó, một cách tiếp cận song song có thể là:

1. Tìm kiếm Nguồn A *và* Tìm kiếm Nguồn B đồng thời.  
2. Khi cả hai tìm kiếm hoàn tất, Tóm tắt Nguồn A *và* Tóm tắt Nguồn B đồng thời.  
3. Tổng hợp câu trả lời cuối cùng từ các bản tóm tắt A và B (bước này thường là tuần tự, chờ các bước song song hoàn tất).

Ý tưởng cốt lõi là xác định các phần của quy trình làm việc không phụ thuộc vào đầu ra của các phần khác và thực thi chúng song song. Điều này đặc biệt hiệu quả khi xử lý các dịch vụ bên ngoài (như API hoặc cơ sở dữ liệu) có độ trễ, vì bạn có thể đưa ra nhiều yêu cầu đồng thời.

Việc triển khai song song hóa thường yêu cầu các framework hỗ trợ thực thi không đồng bộ hoặc đa luồng/đa xử lý. Các framework tác nhân hiện đại được thiết kế với các hoạt động không đồng bộ, cho phép bạn dễ dàng xác định các bước có thể chạy song song.

<figure>
    <img src="../imgs/fig.3.1.Example_of_parallelization_with_sub-agents.png" alt="Ví dụ về song song hóa với các tác nhân con">
    <figcaption>Hình 1. Ví dụ về song song hóa với các tác nhân con</figcaption>
</figure>

Các framework như LangChain, LangGraph và Google ADK cung cấp các cơ chế để thực thi song song. Trong Ngôn ngữ biểu thức LangChain (LCEL), bạn có thể đạt được thực thi song song bằng cách kết hợp các đối tượng có thể chạy bằng các toán tử như | (cho tuần tự) và bằng cách cấu trúc các chuỗi hoặc đồ thị của bạn để có các nhánh thực thi đồng thời. LangGraph, với cấu trúc đồ thị của nó, cho phép bạn xác định nhiều nút có thể được thực thi từ một chuyển đổi trạng thái duy nhất, cho phép các nhánh song song trong quy trình làm việc một cách hiệu quả. Google ADK cung cấp các cơ chế gốc, mạnh mẽ để tạo điều kiện và quản lý việc thực thi song song các tác nhân, tăng cường đáng kể hiệu quả và khả năng mở rộng của các hệ thống đa tác nhân phức tạp. Khả năng vốn có này trong framework ADK cho phép các nhà phát triển thiết kế và triển khai các giải pháp trong đó nhiều tác nhân có thể hoạt động đồng thời, thay vì tuần tự.

Mẫu song song hóa rất quan trọng để cải thiện hiệu quả và khả năng phản hồi của các hệ thống tác nhân, đặc biệt khi xử lý các tác vụ liên quan đến nhiều tra cứu, tính toán hoặc tương tác độc lập với các dịch vụ bên ngoài. Đây là một kỹ thuật chính để tối ưu hóa hiệu suất của các quy trình làm việc tác nhân phức tạp.

# Ứng dụng thực tế & Trường hợp sử dụng

Song song hóa là một mẫu mạnh mẽ để tối ưu hóa hiệu suất tác nhân trên nhiều ứng dụng khác nhau:

1. Thu thập thông tin và Nghiên cứu:  
Thu thập thông tin từ nhiều nguồn đồng thời là một trường hợp sử dụng cổ điển.

* **Trường hợp sử dụng:** Một tác nhân nghiên cứu một công ty.  
  * **Các tác vụ song song:** Tìm kiếm các bài báo tin tức, lấy dữ liệu chứng khoán, kiểm tra các đề cập trên mạng xã hội và truy vấn cơ sở dữ liệu công ty, tất cả cùng một lúc.  
  * **Lợi ích:** Thu thập một cái nhìn toàn diện nhanh hơn nhiều so với các tra cứu tuần tự.

2. Xử lý và phân tích dữ liệu:  
Áp dụng các kỹ thuật phân tích khác nhau hoặc xử lý các phân đoạn dữ liệu khác nhau đồng thời.

* **Trường hợp sử dụng:** Một tác nhân phân tích phản hồi của khách hàng.  
  * **Các tác vụ song song:** Chạy phân tích cảm xúc, trích xuất từ khóa, phân loại phản hồi và xác định các vấn đề khẩn cấp đồng thời trên một loạt các mục phản hồi.  
  * **Lợi ích:** Cung cấp phân tích đa diện một cách nhanh chóng.

3. Tương tác đa API hoặc công cụ:  
Gọi nhiều API hoặc công cụ độc lập để thu thập các loại thông tin khác nhau hoặc thực hiện các hành động khác nhau.

* **Trường hợp sử dụng:** Một tác nhân lập kế hoạch du lịch.  
  * **Các tác vụ song song:** Kiểm tra giá vé máy bay, tìm kiếm phòng khách sạn, tra cứu các sự kiện địa phương và tìm các đề xuất nhà hàng đồng thời.  
  * **Lợi ích:** Trình bày một kế hoạch du lịch hoàn chỉnh nhanh hơn.

4. Tạo nội dung với nhiều thành phần:  
Tạo các phần khác nhau của một nội dung phức tạp song song.

* **Trường hợp sử dụng:** Một tác nhân tạo email tiếp thị.  
  * **Các tác vụ song song:** Tạo dòng tiêu đề, soạn thảo nội dung email, tìm hình ảnh liên quan và tạo văn bản nút kêu gọi hành động đồng thời.  
  * **Lợi ích:** Tập hợp email cuối cùng hiệu quả hơn.

5. Xác thực và Kiểm tra:  
Thực hiện nhiều kiểm tra hoặc xác thực độc lập đồng thời.

* **Trường hợp sử dụng:** Một tác nhân xác minh đầu vào của người dùng.  
  * **Các tác vụ song song:** Kiểm tra định dạng email, xác thực số điện thoại, xác minh địa chỉ với cơ sở dữ liệu và kiểm tra từ ngữ tục tĩu đồng thời.  
  * **Lợi ích:** Cung cấp phản hồi nhanh hơn về tính hợp lệ của đầu vào.

6. Xử lý đa phương thức:  
Xử lý các phương thức khác nhau (văn bản, hình ảnh, âm thanh) của cùng một đầu vào đồng thời.

* **Trường hợp sử dụng:** Một tác nhân phân tích một bài đăng trên mạng xã hội có văn bản và hình ảnh.  
  * **Các tác vụ song song:** Phân tích văn bản để tìm cảm xúc và từ khóa *và* phân tích hình ảnh để tìm đối tượng và mô tả cảnh đồng thời.  
  * **Lợi ích:** Tích hợp thông tin chi tiết từ các phương thức khác nhau nhanh hơn.

7. Kiểm thử A/B hoặc Tạo nhiều tùy chọn:  
Tạo nhiều biến thể của phản hồi hoặc đầu ra song song để chọn ra cái tốt nhất.

* **Trường hợp sử dụng:** Một tác nhân tạo các tùy chọn văn bản sáng tạo khác nhau.  
  * **Các tác vụ song song:** Tạo ba tiêu đề khác nhau cho một bài báo đồng thời bằng cách sử dụng các lời nhắc hoặc mô hình hơi khác nhau.  
  * **Lợi ích:** Cho phép so sánh và lựa chọn tùy chọn tốt nhất một cách nhanh chóng.

Song song hóa là một kỹ thuật tối ưu hóa cơ bản trong thiết kế tác nhân, cho phép các nhà phát triển xây dựng các ứng dụng hiệu quả và phản hồi nhanh hơn bằng cách tận dụng việc thực thi đồng thời cho các tác vụ độc lập.

# Ví dụ mã thực hành (LangChain)

Việc thực thi song song trong framework LangChain được hỗ trợ bởi Ngôn ngữ biểu thức LangChain (LCEL). Phương pháp chính liên quan đến việc cấu trúc nhiều thành phần có thể chạy trong một cấu trúc từ điển hoặc danh sách. Khi tập hợp này được truyền làm đầu vào cho một thành phần tiếp theo trong chuỗi, thời gian chạy LCEL sẽ thực thi các thành phần có thể chạy chứa trong đó một cách đồng thời.

Trong ngữ cảnh của LangGraph, nguyên tắc này được áp dụng cho cấu trúc liên kết của đồ thị. Các quy trình làm việc song song được định nghĩa bằng cách kiến trúc đồ thị sao cho nhiều nút, thiếu các phụ thuộc tuần tự trực tiếp, có thể được khởi tạo từ một nút chung duy nhất. Các đường dẫn song song này thực thi độc lập trước khi kết quả của chúng có thể được tổng hợp tại một điểm hội tụ tiếp theo trong đồ thị.

Việc triển khai sau đây minh họa một quy trình làm việc xử lý song song được xây dựng bằng framework LangChain. Quy trình làm việc này được thiết kế để thực thi hai hoạt động độc lập đồng thời để phản hồi một truy vấn người dùng duy nhất. Các quy trình song song này được khởi tạo dưới dạng các chuỗi hoặc hàm riêng biệt, và các đầu ra tương ứng của chúng sau đó được tổng hợp thành một kết quả thống nhất.

Các điều kiện tiên quyết cho việc triển khai này bao gồm cài đặt các gói Python cần thiết, chẳng hạn như langchain, langchain-community và một thư viện nhà cung cấp mô hình như langchain-openai. Hơn nữa, một khóa API hợp lệ cho mô hình ngôn ngữ đã chọn phải được cấu hình trong môi trường cục bộ để xác thực.

```
import os
import asyncio
from typing import Optional

from langchain_openai import ChatOpenAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser
from langchain_core.runnables import (
    Runnable,
    RunnableParallel,
    RunnablePassthrough,
)

# --- Configuration ---
# Ensure your API key environment variable is set (e.g., OPENAI_API_KEY)
try:
    llm: Optional[ChatOpenAI] = ChatOpenAI(model="gpt-4o-mini", temperature=0.7)
except Exception as e:
    print(f"Error initializing language model: {e}")
    llm = None

# --- Define Independent Chains ---
# These three chains represent distinct tasks that can be executed in parallel.
summarize_chain: Runnable = (
    ChatPromptTemplate.from_messages(
        [
            ("system", "Summarize the following topic concisely:"),
            ("user", "{topic}"),
        ]
    )
    | llm
    | StrOutputParser()
)

questions_chain: Runnable = (
    ChatPromptTemplate.from_messages(
        [
            ("system", "Generate three interesting questions about the following topic:"),
            ("user", "{topic}"),
        ]
    )
    | llm
    | StrOutputParser()
)

terms_chain: Runnable = (
    ChatPromptTemplate.from_messages(
        [
            (
                "system",
                "Identify 5-10 key terms from the following topic, separated by commas:",
            ),
            ("user", "{topic}"),
        ]
    )
    | llm
    | StrOutputParser()
)

# --- Build the Parallel + Synthesis Chain ---
# 1. Define the block of tasks to run in parallel. The results of these,
#    along with the original topic, will be fed into the next step.
map_chain: RunnableParallel = RunnableParallel(
    {
        "summary": summarize_chain,
        "questions": questions_chain,
        "key_terms": terms_chain,
        "topic": RunnablePassthrough(),  # Pass the original topic through
    }
)

# 2. Define the final synthesis prompt which will combine the parallel results.
synthesis_prompt: ChatPromptTemplate = ChatPromptTemplate.from_messages(
    [
        (
            "system",
            """Based on the following information:
    Summary: {summary}
    Related Questions: {questions}
    Key Terms: {key_terms}
    Synthesize a comprehensive answer.""",
        ),
        ("user", "Original topic: {topic}"),
    ]
)

# 3. Construct the full chain by piping the parallel results directly
#    into the synthesis prompt, followed by the LLM and output parser.
full_parallel_chain: Runnable = map_chain | synthesis_prompt | llm | StrOutputParser()

# --- Run the Chain ---
async def run_parallel_example(topic: str) -> None:
    """
    Asynchronously invokes the parallel processing chain with a specific topic
    and prints the synthesized result.

    Args:
        topic: The input topic to be processed by the LangChain chains.
    """
    if not llm:
        print("LLM not initialized. Cannot run example.")
        return

    print(f"\n--- Running Parallel LangChain Example for Topic: '{topic}' ---")
    try:
        # The input to `ainvoke` is the single 'topic' string,
        # then passed to each runnable in the `map_chain`.
        response = await full_parallel_chain.ainvoke(topic)
        print("\n--- Final Response ---")
        print(response)
    except Exception as e:
        print(f"\nAn error occurred during chain execution: {e}")


if __name__ == "__main__":
    test_topic = "The history of space exploration"
    # In Python 3.7+, asyncio.run is the standard way to run an async function.
    asyncio.run(run_parallel_example(test_topic))

```

Mã Python được cung cấp triển khai một ứng dụng LangChain được thiết kế để xử lý một chủ đề nhất định một cách hiệu quả bằng cách tận dụng việc thực thi song song. Lưu ý rằng asyncio cung cấp tính đồng thời (concurrency), không phải tính song song (parallelism). Nó đạt được điều này trên một luồng duy nhất bằng cách sử dụng một vòng lặp sự kiện chuyển đổi thông minh giữa các tác vụ khi một tác vụ không hoạt động (ví dụ: chờ yêu cầu mạng). Điều này tạo ra hiệu ứng nhiều tác vụ tiến hành cùng một lúc, nhưng bản thân mã vẫn đang được thực thi bởi chỉ một luồng, bị ràng buộc bởi Khóa trình thông dịch toàn cầu (GIL) của Python. 

Mã bắt đầu bằng cách nhập các mô-đun cần thiết từ langchain_openai và langchain_core, bao gồm các thành phần cho mô hình ngôn ngữ, lời nhắc, phân tích cú pháp đầu ra và cấu trúc có thể chạy. Mã cố gắng khởi tạo một phiên bản ChatOpenAI, đặc biệt sử dụng mô hình "gpt-4o-mini", với nhiệt độ được chỉ định để kiểm soát sự sáng tạo. Một khối try-except được sử dụng để tăng cường độ bền trong quá trình khởi tạo mô hình ngôn ngữ. Ba "chuỗi" LangChain độc lập sau đó được định nghĩa, mỗi chuỗi được thiết kế để thực hiện một tác vụ riêng biệt trên chủ đề đầu vào. Chuỗi đầu tiên dùng để tóm tắt chủ đề một cách ngắn gọn, sử dụng một thông báo hệ thống và một thông báo người dùng chứa phần giữ chỗ chủ đề. Chuỗi thứ hai được cấu hình để tạo ba câu hỏi thú vị liên quan đến chủ đề. Chuỗi thứ ba được thiết lập để xác định từ 5 đến 10 thuật ngữ chính từ chủ đề đầu vào, yêu cầu chúng được phân tách bằng dấu phẩy. Mỗi chuỗi độc lập này bao gồm một ChatPromptTemplate được điều chỉnh cho tác vụ cụ thể của nó, tiếp theo là mô hình ngôn ngữ đã khởi tạo và một StrOutputParser để định dạng đầu ra dưới dạng chuỗi. 

Một khối RunnableParallel sau đó được xây dựng để gói gọn ba chuỗi này, cho phép chúng thực thi đồng thời. Runnable song song này cũng bao gồm một RunnablePassthrough để đảm bảo chủ đề đầu vào ban đầu có sẵn cho các bước tiếp theo. Một ChatPromptTemplate riêng biệt được định nghĩa cho bước tổng hợp cuối cùng, lấy tóm tắt, câu hỏi, các thuật ngữ chính và chủ đề ban đầu làm đầu vào để tạo ra một câu trả lời toàn diện. Chuỗi xử lý đầu cuối hoàn chỉnh, được đặt tên là full_parallel_chain, được tạo bằng cách sắp xếp map_chain (khối song song) vào lời nhắc tổng hợp, tiếp theo là mô hình ngôn ngữ và trình phân tích cú pháp đầu ra. Một hàm không đồng bộ run_parallel_example được cung cấp để minh họa cách gọi full_parallel_chain này. Hàm này lấy chủ đề làm đầu vào và sử dụng invoke để chạy chuỗi không đồng bộ. Cuối cùng, khối Python tiêu chuẩn if __name__ == "__main__": cho thấy cách thực thi run_parallel_example với một chủ đề mẫu, trong trường hợp này, "Lịch sử khám phá không gian", sử dụng asyncio.run để quản lý việc thực thi không đồng bộ.

Về bản chất, mã này thiết lập một quy trình làm việc trong đó nhiều lệnh gọi LLM (để tóm tắt, đặt câu hỏi và xác định thuật ngữ) diễn ra đồng thời cho một chủ đề nhất định, và kết quả của chúng sau đó được kết hợp bởi một lệnh gọi LLM cuối cùng. Điều này thể hiện ý tưởng cốt lõi của song song hóa trong một quy trình làm việc tác nhân sử dụng LangChain.

# Ví dụ mã thực hành (Google ADK)

Bây giờ, chúng ta hãy chuyển sự chú ý sang một ví dụ cụ thể minh họa các khái niệm này trong framework Google ADK. Chúng ta sẽ xem xét cách các nguyên thủy của ADK, chẳng hạn như ParallelAgent và SequentialAgent, có thể được áp dụng để xây dựng một luồng tác nhân tận dụng việc thực thi đồng thời để cải thiện hiệu quả.

```
from google.adk.agents import LlmAgent, ParallelAgent, SequentialAgent
from google.adk.tools import google_search

GEMINI_MODEL = "gemini-2.0-flash"

# --- 1. Define Researcher Sub-Agents (to run in parallel) ---

# Researcher 1: Renewable Energy
researcher_agent_1 = LlmAgent(
    name="RenewableEnergyResearcher",
    model=GEMINI_MODEL,
    instruction=(
        "You are an AI Research Assistant specializing in energy. "
        "Research the latest advancements in 'renewable energy sources'. "
        "Use the Google Search tool provided. "
        "Summarize your key findings concisely (1-2 sentences). "
        "Output *only* the summary. "
    ),
    description="Researches renewable energy sources.",
    tools=[google_search],
    # Store result in state for the merger agent
    output_key="renewable_energy_result",
)

# Researcher 2: Electric Vehicles
researcher_agent_2 = LlmAgent(
    name="EVResearcher",
    model=GEMINI_MODEL,
    instruction=(
        "You are an AI Research Assistant specializing in transportation. "
        "Research the latest developments in 'electric vehicle technology'. "
        "Use the Google Search tool provided. "
        "Summarize your key findings concisely (1-2 sentences). "
        "Output *only* the summary. "
    ),
    description="Researches electric vehicle technology.",
    tools=[google_search],
    # Store result in state for the merger agent
    output_key="ev_technology_result",
)

# Researcher 3: Carbon Capture
researcher_agent_3 = LlmAgent(
    name="CarbonCaptureResearcher",
    model=GEMINI_MODEL,
    instruction=(
        "You are an AI Research Assistant specializing in climate solutions. "
        "Research the current state of 'carbon capture methods'. "
        "Use the Google Search tool provided. "
        "Summarize your key findings concisely (1-2 sentences). "
        "Output *only* the summary. "
    ),
    description="Researches carbon capture methods.",
    tools=[google_search],
    # Store result in state for the merger agent
    output_key="carbon_capture_result",
)

# --- 2. Create the ParallelAgent (Runs researchers concurrently) ---
# This agent orchestrates the concurrent execution of the researchers.
# It finishes once all researchers have completed and stored their results in state.
parallel_research_agent = ParallelAgent(
    name="ParallelWebResearchAgent",
    sub_agents=[researcher_agent_1, researcher_agent_2, researcher_agent_3],
    description="Runs multiple research agents in parallel to gather information.",
)

# --- 3. Define the Merger Agent (Runs *after* the parallel agents) ---
# This agent takes the results stored in the session state by the parallel agents
# and synthesizes them into a single, structured response with attributions.
merger_agent = LlmAgent(
    name="SynthesisAgent",
    model=GEMINI_MODEL,  # Or potentially a more powerful model if needed for synthesis
    instruction=(
        "You are an AI Assistant responsible for combining research findings into a structured report. "
        "Your primary task is to synthesize the following research summaries, clearly attributing findings "
        "to their source areas. Structure your response using headings for each topic. Ensure the report is "
        "coherent and integrates the key points smoothly.\n\n"
        "**Crucially: Your entire response MUST be grounded *exclusively* on the information provided in the "
        "'Input Summaries' below. Do NOT add any external knowledge, facts, or details not present in these "
        "specific summaries.**\n\n"
        "**Input Summaries:**\n"
        "*   **Renewable Energy:**\n"
        "    {renewable_energy_result}\n"
        "*   **Electric Vehicles:**\n"
        "    {ev_technology_result}\n"
        "*   **Carbon Capture:**\n"
        "    {carbon_capture_result}\n\n"
        "**Output Format:**\n"
        "## Summary of Recent Sustainable Technology Advancements\n\n"
        "### Renewable Energy Findings (Based on RenewableEnergyResearcher's findings)\n"
        "[Synthesize and elaborate *only* on the renewable energy input summary provided above.]\n\n"
        "### Electric Vehicle Findings (Based on EVResearcher's findings)\n"
        "[Synthesize and elaborate *only* on the EV input summary provided above.]\n\n"
        "### Carbon Capture Findings (Based on CarbonCaptureResearcher's findings)\n"
        "[Synthesize and elaborate *only* on the carbon capture input summary provided above.]\n\n"
        "### Overall Conclusion\n"
        "[Provide a brief (1-2 sentence) concluding statement that connects *only* the findings presented above.]\n\n"
        "Output *only* the structured report following this format. Do not include introductory or concluding "
        "phrases outside this structure, and strictly adhere to using only the provided input summary content."
    ),
    description=(
        "Combines research findings from parallel agents into a structured, cited report, "
        "strictly grounded on provided inputs."
    ),
    # No tools needed for merging
    # No output_key needed here, as its direct response is the final output of the sequence
)

# --- 4. Create the SequentialAgent (Orchestrates the overall flow) ---
# This is the main agent that will be run. It first executes the ParallelAgent
# to populate the state, and then executes the MergerAgent to produce the final output.
sequential_pipeline_agent = SequentialAgent(
    name="ResearchAndSynthesisPipeline",
    # Run parallel research first, then merge
    sub_agents=[parallel_research_agent, merger_agent],
    description="Coordinates parallel research and synthesizes the results.",
)

root_agent = sequential_pipeline_agent

```

Mã này định nghĩa một hệ thống đa tác nhân được sử dụng để nghiên cứu và tổng hợp thông tin về các tiến bộ công nghệ bền vững. Nó thiết lập ba phiên bản LlmAgent để hoạt động như các nhà nghiên cứu chuyên biệt. ResearcherAgent_1 tập trung vào các nguồn năng lượng tái tạo, ResearcherAgent_2 nghiên cứu công nghệ xe điện và ResearcherAgent_3 điều tra các phương pháp thu giữ carbon. Mỗi tác nhân nghiên cứu được cấu hình để sử dụng GEMINI_MODEL và công cụ google_search. Chúng được hướng dẫn tóm tắt các phát hiện của mình một cách ngắn gọn (1-2 câu) và lưu trữ các bản tóm tắt này trong trạng thái phiên bằng cách sử dụng output_key.

Một ParallelAgent có tên ParallelWebResearchAgent sau đó được tạo để chạy ba tác nhân nghiên cứu này đồng thời. Điều này cho phép nghiên cứu được thực hiện song song, có khả năng tiết kiệm thời gian. ParallelAgent hoàn thành việc thực thi của nó khi tất cả các tác nhân con của nó (các nhà nghiên cứu) đã hoàn thành và điền vào trạng thái.

Tiếp theo, một MergerAgent (cũng là một LlmAgent) được định nghĩa để tổng hợp các kết quả nghiên cứu. Tác nhân này lấy các bản tóm tắt được lưu trữ trong trạng thái phiên bởi các nhà nghiên cứu song song làm đầu vào. Hướng dẫn của nó nhấn mạnh rằng đầu ra phải hoàn toàn dựa trên các bản tóm tắt đầu vào được cung cấp, cấm bổ sung kiến thức bên ngoài. MergerAgent được thiết kế để cấu trúc các phát hiện kết hợp thành một báo cáo với các tiêu đề cho mỗi chủ đề và một kết luận tổng thể ngắn gọn.

Cuối cùng, một SequentialAgent có tên ResearchAndSynthesisPipeline được tạo để điều phối toàn bộ quy trình làm việc. Với tư cách là bộ điều khiển chính, tác nhân chính này trước tiên thực thi ParallelAgent để thực hiện nghiên cứu. Khi ParallelAgent hoàn tất, SequentialAgent sau đó thực thi MergerAgent để tổng hợp thông tin đã thu thập. sequential_pipeline_agent được đặt làm root_agent, đại diện cho điểm vào để chạy hệ thống đa tác nhân này. Quy trình tổng thể được thiết kế để thu thập thông tin hiệu quả từ nhiều nguồn song song và sau đó kết hợp nó thành một báo cáo duy nhất, có cấu trúc.

# Sơ lược

**Cái gì:** Nhiều quy trình làm việc tác nhân liên quan đến nhiều tác vụ con phải được hoàn thành để đạt được mục tiêu cuối cùng. Việc thực thi hoàn toàn tuần tự, trong đó mỗi tác vụ chờ tác vụ trước đó hoàn thành, thường không hiệu quả và chậm. Độ trễ này trở thành một nút thắt cổ chai đáng kể khi các tác vụ phụ thuộc vào các hoạt động I/O bên ngoài, chẳng hạn như gọi các API khác nhau hoặc truy vấn nhiều cơ sở dữ liệu. Nếu không có cơ chế thực thi đồng thời, tổng thời gian xử lý là tổng thời lượng của tất cả các tác vụ riêng lẻ, cản trở hiệu suất và khả năng phản hồi tổng thể của hệ thống.

**Tại sao:** Mẫu song song hóa cung cấp một giải pháp tiêu chuẩn hóa bằng cách cho phép thực thi đồng thời các tác vụ độc lập. Nó hoạt động bằng cách xác định các thành phần của một quy trình làm việc, như việc sử dụng công cụ hoặc các lệnh gọi LLM, không phụ thuộc vào đầu ra tức thì của nhau. Các framework tác nhân như LangChain và Google ADK cung cấp các cấu trúc tích hợp để định nghĩa và quản lý các hoạt động đồng thời này. Ví dụ, một quy trình chính có thể gọi một số tác vụ con chạy song song và chờ tất cả chúng hoàn thành trước khi chuyển sang bước tiếp theo. Bằng cách chạy các tác vụ độc lập này cùng một lúc thay vì lần lượt, mẫu này giảm đáng kể tổng thời gian thực thi.

**Quy tắc chung:** Sử dụng mẫu này khi một quy trình làm việc chứa nhiều hoạt động độc lập có thể chạy đồng thời, chẳng hạn như tìm nạp dữ liệu từ nhiều API, xử lý các khối dữ liệu khác nhau hoặc tạo nhiều phần nội dung để tổng hợp sau này.

**Tóm tắt trực quan**

<figure>
    <img src="../imgs/fig.3.2.Parallelization_design_pattern.png" alt="Mẫu thiết kế song song hóa">
    <figcaption>Hình 2: Mẫu thiết kế song song hóa</figcaption>
</figure>

# Các điểm chính

Dưới đây là các điểm chính:

* Song song hóa là một mẫu để thực thi các tác vụ độc lập đồng thời nhằm cải thiện hiệu quả.  
* Nó đặc biệt hữu ích khi các tác vụ liên quan đến việc chờ tài nguyên bên ngoài, chẳng hạn như các lệnh gọi API.  
* Việc áp dụng kiến trúc đồng thời hoặc song song mang lại sự phức tạp và chi phí đáng kể, ảnh hưởng đến các giai đoạn phát triển chính như thiết kế, gỡ lỗi và ghi nhật ký hệ thống.  
* Các framework như LangChain và Google ADK cung cấp hỗ trợ tích hợp để định nghĩa và quản lý việc thực thi song song.  
* Trong Ngôn ngữ biểu thức LangChain (LCEL), RunnableParallel là một cấu trúc chính để chạy nhiều runnable song song.  
* Google ADK có thể tạo điều kiện thực thi song song thông qua Ủy quyền do LLM điều khiển, trong đó LLM của tác nhân điều phối viên xác định các tác vụ con độc lập và kích hoạt việc xử lý đồng thời chúng bởi các tác nhân con chuyên biệt.  
* Song song hóa giúp giảm độ trễ tổng thể và làm cho các hệ thống tác nhân phản hồi nhanh hơn đối với các tác vụ phức tạp.

# Kết luận

Mẫu song song hóa là một phương pháp để tối ưu hóa các quy trình làm việc tính toán bằng cách thực thi đồng thời các tác vụ con độc lập. Cách tiếp cận này làm giảm độ trễ tổng thể, đặc biệt trong các hoạt động phức tạp liên quan đến nhiều suy luận mô hình hoặc lệnh gọi đến các dịch vụ bên ngoài.

Các framework cung cấp các cơ chế riêng biệt để triển khai mẫu này. Trong LangChain, các cấu trúc như RunnableParallel được sử dụng để định nghĩa và thực thi rõ ràng nhiều chuỗi xử lý đồng thời. Ngược lại, các framework như Google Agent Developer Kit (ADK) có thể đạt được song song hóa thông qua ủy quyền đa tác nhân, trong đó một mô hình điều phối viên chính gán các tác vụ con khác nhau cho các tác nhân chuyên biệt có thể hoạt động đồng thời.

Bằng cách tích hợp xử lý song song với các luồng điều khiển tuần tự (chuỗi) và có điều kiện (định tuyến), có thể xây dựng các hệ thống tính toán phức tạp, hiệu suất cao có khả năng quản lý hiệu quả các tác vụ đa dạng và phức tạp.

# Tài liệu tham khảo

Dưới đây là một số tài nguyên để đọc thêm về mẫu song song hóa và các khái niệm liên quan:

1. Tài liệu Ngôn ngữ biểu thức LangChain (LCEL) (Song song hóa): [https://python.langchain.com/docs/concepts/lcel/](https://python.langchain.com/docs/concepts/lcel/)   
2. Tài liệu Google Agent Developer Kit (ADK) (Hệ thống đa tác nhân): [https://google.github.io/adk-docs/agents/multi-agents/](https://google.github.io/adk-docs/agents/multi-agents/)  
3. Tài liệu Python asyncio: [https://docs.python.org/3/library/asyncio.html](https://docs.python.org/3/library/asyncio.html)
