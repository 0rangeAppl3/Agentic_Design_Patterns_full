Chương 5: Sử dụng Công cụ (Gọi hàm)

Tổng quan về Mẫu hình Sử dụng Công cụ

Cho đến nay, chúng ta đã thảo luận về các mẫu hình agent (tác tử) chủ yếu liên quan đến việc điều phối các tương tác giữa các mô hình ngôn ngữ và quản lý luồng thông tin trong quy trình làm việc nội bộ của agent (Nối chuỗi, Định tuyến, Song song hóa, Phản tư). Tuy nhiên, để các agent thực sự hữu ích và tương tác với thế giới thực hoặc các hệ thống bên ngoài, chúng cần khả năng sử dụng Công cụ.

Mẫu hình Sử dụng Công cụ, thường được triển khai thông qua một cơ chế gọi là Gọi hàm (Function Calling), cho phép agent tương tác với các API, cơ sở dữ liệu, dịch vụ bên ngoài hoặc thậm chí thực thi mã. Nó cho phép LLM làm lõi của agent quyết định khi nào và làm thế nào để sử dụng một hàm bên ngoài cụ thể dựa trên yêu cầu của người dùng hoặc trạng thái hiện tại của tác vụ.

Quá trình này thường bao gồm:

Định nghĩa Công cụ:

Các hàm hoặc khả năng bên ngoài được định nghĩa và mô tả cho LLM. Mô tả này bao gồm mục đích, tên của hàm và các tham số mà nó chấp nhận, cùng với kiểu dữ liệu và mô tả của chúng.

Quyết định của LLM:

LLM nhận yêu cầu của người dùng và các định nghĩa công cụ có sẵn. Dựa trên sự hiểu biết về yêu cầu và các công cụ, LLM quyết định xem việc gọi một hoặc nhiều công cụ có cần thiết để hoàn thành yêu cầu hay không.

Tạo lệnh Gọi hàm:

Nếu LLM quyết định sử dụng một công cụ, nó sẽ tạo ra một đầu ra có cấu trúc (thường là một đối tượng JSON) chỉ định tên của công cụ cần gọi và các đối số (tham số) để truyền cho nó, được trích xuất từ yêu cầu của người dùng.

Thực thi Công cụ:

Framework của agent hoặc lớp điều phối sẽ chặn đầu ra có cấu trúc này. Nó xác định công cụ được yêu cầu và thực thi hàm bên ngoài thực tế với các đối số được cung cấp.

Quan sát/Kết quả:

Đầu ra hoặc kết quả từ việc thực thi công cụ được trả về cho agent.

Xử lý của LLM (Tùy chọn nhưng phổ biến):

LLM nhận đầu ra của công cụ làm ngữ cảnh và sử dụng nó để đưa ra phản hồi cuối cùng cho người dùng hoặc quyết định bước tiếp theo trong quy trình làm việc (có thể liên quan đến việc gọi một công cụ khác, phản tư hoặc cung cấp câu trả lời cuối cùng).

Mẫu hình này là nền tảng vì nó phá vỡ những hạn chế của dữ liệu huấn luyện của LLM và cho phép nó truy cập thông tin cập nhật, thực hiện các phép tính mà nó không thể tự làm, tương tác với dữ liệu cụ thể của người dùng hoặc kích hoạt các hành động trong thế giới thực. Gọi hàm là cơ chế kỹ thuật bắc cầu giữa khả năng suy luận của LLM và vô số các chức năng bên ngoài có sẵn.

Mặc dù "gọi hàm" (function calling) mô tả chính xác việc gọi các hàm mã cụ thể, được xác định trước, nhưng sẽ hữu ích hơn khi xem xét khái niệm mở rộng hơn về "gọi công cụ" (tool calling). Thuật ngữ rộng hơn này thừa nhận rằng các khả năng của một agent có thể vượt xa việc thực thi hàm đơn giản. Một "công cụ" có thể là một hàm truyền thống, nhưng nó cũng có thể là một điểm cuối API (API endpoint) phức tạp, một yêu cầu đến cơ sở dữ liệu, hoặc thậm chí là một chỉ thị hướng đến một agent chuyên biệt khác. Góc nhìn này cho phép chúng ta hình dung các hệ thống phức tạp hơn, nơi mà, ví dụ, một agent chính có thể ủy thác một tác vụ phân tích dữ liệu phức tạp cho một "agent phân tích" chuyên dụng hoặc truy vấn một cơ sở tri thức bên ngoài thông qua API của nó. Tư duy theo hướng "gọi công cụ" nắm bắt tốt hơn tiềm năng đầy đủ của các agent trong vai trò là người điều phối xuyên suốt một hệ sinh thái đa dạng gồm các tài nguyên kỹ thuật số và các thực thể thông minh khác.

Các framework như LangChain, LangGraph, và Google Agent Developer Kit (ADK) cung cấp hỗ trợ mạnh mẽ để định nghĩa các công cụ và tích hợp chúng vào quy trình làm việc của agent, thường tận dụng khả năng gọi hàm gốc của các LLM hiện đại như trong chuỗi Gemini hoặc OpenAI. Trên "khung sườn" (canvas) của các framework này, bạn định nghĩa các công cụ và sau đó cấu hình các agent (thường là LLM Agents) để nhận biết và có khả năng sử dụng các công cụ này.

Sử dụng Công cụ là một mẫu hình nền tảng để xây dựng các agent mạnh mẽ, có tính tương tác và nhận biết được môi trường bên ngoài.

Ứng dụng Thực tế & Trường hợp Sử dụng

Mẫu hình Sử dụng Công cụ có thể áp dụng trong hầu hết mọi tình huống mà agent cần vượt ra ngoài việc tạo văn bản để thực hiện một hành động hoặc truy xuất thông tin động, cụ thể:

1. Truy xuất thông tin từ các nguồn bên ngoài: Truy cập dữ liệu hoặc thông tin thời gian thực không có trong dữ liệu huấn luyện của LLM.

Trường hợp sử dụng:

Một agent thời tiết.

Công cụ:

Một API thời tiết nhận đầu vào là một vị trí và trả về điều kiện thời tiết hiện tại.

Luồng của Agent:

Người dùng hỏi, "Thời tiết ở London thế nào?", LLM xác định cần công cụ thời tiết, gọi công cụ với "London", công cụ trả về dữ liệu, LLM định dạng dữ liệu thành phản hồi thân thiện với người dùng.

2. Tương tác với Cơ sở dữ liệu và API: Thực hiện các truy vấn, cập nhật hoặc các hoạt động khác trên dữ liệu có cấu trúc.

Trường hợp sử dụng:

Một agent thương mại điện tử.

Công cụ:

Các lệnh gọi API để kiểm tra hàng tồn kho, lấy trạng thái đơn hàng hoặc xử lý thanh toán.

Luồng của Agent:

Người dùng hỏi "Sản phẩm X còn hàng không?", LLM gọi API hàng tồn kho, công cụ trả về số lượng tồn kho, LLM thông báo cho người dùng về tình trạng hàng.

3. Thực hiện các Phép tính và Phân tích Dữ liệu: Sử dụng máy tính bên ngoài, thư viện phân tích dữ liệu hoặc các công cụ thống kê.

Trường hợp sử dụng:

Một agent tài chính.

Công cụ:

Một hàm máy tính, một API dữ liệu thị trường chứng khoán, một công cụ bảng tính.

Luồng của Agent:

Người dùng hỏi "Giá hiện tại của AAPL là bao nhiêu và tính lợi nhuận tiềm năng nếu tôi mua 100 cổ phiếu ở mức 150 đô la?", LLM gọi API chứng khoán, lấy giá hiện tại, sau đó gọi công cụ máy tính, lấy kết quả, định dạng phản hồi.

4. Gửi Liên lạc: Gửi email, tin nhắn hoặc thực hiện các lệnh gọi API đến các dịch vụ liên lạc bên ngoài.

Trường hợp sử dụng:

Một agent trợ lý cá nhân.

Công cụ:

Một API gửi email.

Luồng của Agent:

Người dùng nói, "Gửi email cho John về cuộc họp ngày mai.", LLM gọi một công cụ email với người nhận, chủ đề và nội dung được trích xuất từ yêu cầu.

5. Thực thi Mã: Chạy các đoạn mã trong một môi trường an toàn để thực hiện các tác vụ cụ thể.

Trường hợp sử dụng:

Một agent trợ lý lập trình.

Công cụ:

Một trình thông dịch mã (code interpreter).

Luồng của Agent:

Người dùng cung cấp một đoạn mã Python và hỏi, "Đoạn mã này làm gì?", LLM sử dụng công cụ thông dịch để chạy mã và phân tích đầu ra của nó.

6. Điều khiển các Hệ thống hoặc Thiết bị khác: Tương tác với các thiết bị nhà thông minh, nền tảng IoT hoặc các hệ thống được kết nối khác.

Trường hợp sử dụng:

Một agent nhà thông minh.

Công cụ:

Một API để điều khiển đèn thông minh.

Luồng của Agent:

Người dùng nói, "Tắt đèn phòng khách." LLM gọi công cụ nhà thông minh với lệnh và thiết bị mục tiêu.

Sử dụng Công cụ là thứ biến đổi một mô hình ngôn ngữ từ một trình tạo văn bản thành một agent có khả năng cảm nhận, suy luận và hành động trong thế giới kỹ thuật số hoặc vật lý (xem Hình 1).

<figure> ![][../imgs/fig.5.1.Some_examples_of_an_Agent_using_Tools.png] <figcaption>Hình 1: Một số ví dụ về Agent sử dụng Công cụ</figcaption> </figure>

Ví dụ Mã thực hành (LangChain)

Việc triển khai sử dụng công cụ trong framework LangChain là một quy trình gồm hai giai đoạn. Ban đầu, một hoặc nhiều công cụ được định nghĩa, thường bằng cách đóng gói các hàm Python hiện có hoặc các thành phần có thể chạy khác. Sau đó, các công cụ này được liên kết (bound) với một mô hình ngôn ngữ, qua đó cấp cho mô hình khả năng tạo ra một yêu cầu sử dụng công cụ có cấu trúc khi nó xác định rằng cần phải gọi một hàm bên ngoài để đáp ứng truy vấn của người dùng.

Phần triển khai sau đây sẽ minh họa nguyên tắc này bằng cách trước tiên định nghĩa một hàm đơn giản để mô phỏng một công cụ truy xuất thông tin. Sau đó, một agent sẽ được xây dựng và cấu hình để tận dụng công cụ này nhằm phản hồi lại đầu vào của người dùng. Việc thực thi ví dụ này yêu cầu cài đặt các thư viện LangChain cốt lõi và một gói nhà cung cấp cụ thể cho mô hình. Hơn nữa, việc xác thực đúng cách với dịch vụ mô hình ngôn ngữ đã chọn, thường thông qua một khóa API được cấu hình trong môi trường cục bộ, là một điều kiện tiên quyết cần thiết.

import os
import getpass
import asyncio
import nest_asyncio
import logging
from typing import List
from dotenv import load_dotenv

from langchain_google_genai import ChatGoogleGenerativeAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.tools import tool as langchain_tool
from langchain.agents import create_tool_calling_agent, AgentExecutor


# BỎ CHÚ THÍCH
# Nhắc người dùng nhập khóa API một cách an toàn và đặt làm biến môi trường
os.environ["GOOGLE_API_KEY"] = getpass.getpass("Enter your Google API key: ")
os.environ["OPENAI_API_KEY"] = getpass.getpass("Enter your OpenAI API key: ")

try:
    # Cần một mô hình có khả năng gọi hàm/công cụ.
    llm = ChatGoogleGenerativeAI(model="gemini-2.0-flash", temperature=0)
    print(f"✅ Language model initialized: {llm.model}")
except Exception as e:
    print(f"🛑 Error initializing language model: {e}")
    llm = None


# --- Định nghĩa một Công cụ ---
@langchain_tool
def search_information(query: str) -> str:
    """
    Provides factual information on a given topic. Use this tool to find answers to phrases
    like 'capital of France' or 'weather in London?'.
    """
    print(f"\n--- 🛠️ Tool Called: search_information with query: '{query}' ---")

    # Mô phỏng một công cụ tìm kiếm với một từ điển chứa các kết quả được định nghĩa trước.
    simulated_results = {
        "weather in london": "The weather in London is currently cloudy with a temperature of 15°C.",
        "capital of france": "The capital of France is Paris.",
        "population of earth": "The estimated population of Earth is around 8 billion people.",
        "tallest mountain": "Mount Everest is the tallest mountain above sea level.",
        "default": (
            f"Simulated search result for '{query}': No specific information found, "
            "but the topic seems interesting."
        ),
    }

    result = simulated_results.get(query.lower(), simulated_results["default"])
    print(f"--- TOOL RESULT: {result} ---")
    return result


tools = [search_information]


# --- Tạo một Agent Gọi Công cụ ---
if llm:
    # Mẫu prompt này yêu cầu một chỗ giữ chỗ `agent_scratchpad` cho các bước nội bộ của agent.
    agent_prompt = ChatPromptTemplate.from_messages([
        ("system", "You are a helpful assistant."),
        ("human", "{input}"),
        ("placeholder", "{agent_scratchpad}"),
    ])

    # Tạo agent, liên kết LLM, các công cụ và prompt lại với nhau.
    agent = create_tool_calling_agent(llm, tools, agent_prompt)

    # AgentExecutor là trình thực thi (runtime) gọi agent và thực thi các công cụ đã chọn.
    # Đối số 'tools' không cần thiết ở đây vì chúng đã được liên kết với agent.
    agent_executor = AgentExecutor(agent=agent, verbose=True, tools=tools)


async def run_agent_with_tool(query: str):
    """Gọi agent executor với một truy vấn và in ra phản hồi cuối cùng."""
    print(f"\n--- 🏃 Running Agent with Query: '{query}' ---")
    try:
        response = await agent_executor.ainvoke({"input": query})
        print("\n--- ✅ Final Agent Response ---")
        print(response["output"])
    except Exception as e:
        print(f"\n🛑 An error occurred during agent execution: {e}")


async def main():
    """Chạy tất cả các truy vấn của agent đồng thời."""
    tasks = [
        run_agent_with_tool("What is the capital of France?"),
        run_agent_with_tool("What's the weather like in London?"),
        run_agent_with_tool("Tell me something about dogs.")  # Sẽ kích hoạt phản hồi mặc định của công cụ
    ]
    await asyncio.gather(*tasks)

nest_asyncio.apply()
asyncio.run(main())

"""
Đoạn mã này thiết lập một agent gọi công cụ bằng cách sử dụng thư viện LangChain và mô hình Google Gemini. Nó định nghĩa một công cụ "
search_information
" mô phỏng việc cung cấp câu trả lời thực tế cho các truy vấn cụ thể. Công cụ này có các phản hồi được định nghĩa trước cho "weather in london," "capital of france," và "population of earth," và một phản hồi mặc định cho các truy vấn khác. Một mô hình "
ChatGoogleGenerativeAI
" được khởi tạo, đảm bảo nó có khả năng gọi công cụ. Một "
ChatPromptTemplate
" được tạo để hướng dẫn tương tác của agent. Hàm "
create_tool_calling_agent
" được sử dụng để kết hợp mô hình ngôn ngữ, các công cụ và prompt thành một agent. Một "
AgentExecutor
" sau đó được thiết lập để quản lý việc thực thi của agent và gọi công cụ. Hàm bất đồng bộ "
run_agent_with_tool
" được định nghĩa để gọi agent với một truy vấn nhất định và in kết quả. Hàm bất đồng bộ chính ("main") chuẩn bị nhiều truy vấn để chạy đồng thời. Các truy vấn này được thiết kế để kiểm tra cả phản hồi cụ thể và phản hồi mặc định của công cụ "
search_information
". Cuối cùng, lệnh gọi "
asyncio.run(main())
" thực thi tất cả các tác vụ của agent. Đoạn mã bao gồm các kiểm tra để đảm bảo LLM được khởi tạo thành công trước khi tiếp tục thiết lập và thực thi agent.

Ví dụ Mã thực hành (CrewAI)

Đoạn mã này cung cấp một ví dụ thực tế về cách triển khai gọi hàm (Công cụ) trong framework CrewAI. Nó thiết lập một kịch bản đơn giản trong đó một agent được trang bị một công cụ để tra cứu thông tin. Ví dụ này đặc biệt minh họa việc lấy giá cổ phiếu mô phỏng bằng cách sử dụng agent và công cụ này.

# pip install crewai langchain-openai
import os
import logging

from crewai import Agent, Task, Crew
from crewai.tools import tool


# --- Thực hành tốt nhất: Cấu hình Logging ---
# Một thiết lập logging cơ bản giúp gỡ lỗi và theo dõi quá trình thực thi của crew.
logging.basicConfig(level=logging.INFO, format='%(asctime)s - %(levelname)s - %(message)s')


# --- Thiết lập Khóa API của bạn ---
# Đối với môi trường production, khuyến nghị sử dụng phương pháp an toàn hơn để quản lý khóa
# như các biến môi trường được tải lúc chạy hoặc một trình quản lý bí mật (secret manager).
#
# Đặt biến môi trường cho nhà cung cấp LLM bạn chọn (ví dụ: OPENAI_API_KEY)
# os.environ["OPENAI_API_KEY"] = "YOUR_API_KEY"
# os.environ["OPENAI_MODEL_NAME"] = "gpt-4o"


# --- 1. Công cụ được Tái cấu trúc: Trả về Dữ liệu Sạch ---
# Công cụ giờ đây trả về dữ liệu thô (một số thực) hoặc nêu (raise) một lỗi Python tiêu chuẩn.
# Điều này làm cho nó có thể tái sử dụng nhiều hơn và buộc agent phải xử lý các kết quả một cách đúng đắn.
@tool("Stock Price Lookup Tool")
def get_stock_price(ticker: str) -> float:
    """
    Fetches the latest simulated stock price for a given stock ticker symbol.
    Trả về giá dưới dạng số thực. Nêu (raise) lỗi ValueError nếu không tìm thấy mã cổ phiếu.
    """
    logging.info(f"Tool Call: get_stock_price for ticker '{ticker}'")

    simulated_prices = {
        "AAPL": 178.15,
        "GOOGL": 1750.30,
        "MSFT": 425.50,
    }

    price = simulated_prices.get(ticker.upper())
    if price is not None:
        return price
    else:
        # Nêu một lỗi cụ thể tốt hơn là trả về một chuỗi.
        # Agent được trang bị để xử lý các ngoại lệ và có thể quyết định hành động tiếp theo.
        raise ValueError(f"Simulated price for ticker '{ticker.upper()}' not found.")


# --- 2. Định nghĩa Agent ---
# Định nghĩa agent vẫn giữ nguyên, nhưng giờ đây nó sẽ tận dụng công cụ đã được cải tiến.
financial_analyst_agent = Agent(
    role='Senior Financial Analyst',
    goal='Analyze stock data using provided tools and report key prices.',
    backstory="You are an experienced financial analyst adept at using data sources to find stock information. You provide clear, direct answers.",
    verbose=True,
    tools=[get_stock_price],
    # Cho phép ủy quyền có thể hữu ích, nhưng không cần thiết cho tác vụ đơn giản này.
    allow_delegation=False,
)


# --- 3. Tác vụ được Tinh chỉnh: Hướng dẫn Rõ ràng hơn và Xử lý Lỗi ---
# Mô tả tác vụ cụ thể hơn và hướng dẫn agent cách phản ứng
# với cả việc truy xuất dữ liệu thành công và các lỗi tiềm ẩn.
analyze_aapl_task = Task(
    description=(
        "What is the current simulated stock price for Apple (ticker: AAPL)? "
        "Use the 'Stock Price Lookup Tool' to find it. "
        "If the ticker is not found, you must report that you were unable to retrieve the price."
    ),
    expected_output=(
        "A single, clear sentence stating the simulated stock price for AAPL. "
        "For example: 'The simulated stock price for AAPL is $178.15.' "
        "If the price cannot be found, state that clearly."
    ),
    agent=financial_analyst_agent,
)


# --- 4. Thành lập Crew ---
# Crew điều phối cách agent và tác vụ làm việc cùng nhau.
financial_crew = Crew(
    agents=[financial_analyst_agent],
    tasks=[analyze_aapl_task],
    verbose=True  # Đặt thành False để có ít log chi tiết hơn trong môi trường production
)


# --- 5. Chạy Crew trong một Khối Thực thi Chính ---
# Sử dụng khối __name__ == "__main__": là một thực hành tốt tiêu chuẩn của Python.
def main():
    """Hàm chính để chạy crew."""
    # Kiểm tra khóa API trước khi bắt đầu để tránh lỗi lúc chạy.
    if not os.environ.get("OPENAI_API_KEY"):
        print("ERROR: The OPENAI_API_KEY environment variable is not set.")
        print("Please set it before running the script.")
        return

    print("\n## Starting the Financial Crew...")
    print("---------------------------------")

    # Phương thức kickoff bắt đầu thực thi.
    result = financial_crew.kickoff()

    print("\n---------------------------------")
    print("## Crew execution finished.")
    print("\nFinal Result:\n", result)


if __name__ == "__main__":
    main()

"""
Đoạn mã này minh họa một ứng dụng đơn giản sử dụng thư viện Crew.ai để mô phỏng một tác vụ phân tích tài chính. Nó định nghĩa một công cụ tùy chỉnh, "
get_stock_price
", mô phỏng việc tra cứu giá cổ phiếu cho các mã được định nghĩa trước. Công cụ được thiết kế để trả về một số thực (floating-point number) cho các mã hợp lệ hoặc nêu (raise) lỗi "
ValueError
" cho các mã không hợp lệ. Một "
Agent
" của Crew.ai tên là "
financial_analyst_agent
" được tạo với vai trò là một Nhà phân tích Tài chính Cấp cao. Agent này được cung cấp công cụ "
get_stock_price
" để tương tác. Một "
Task
" được định nghĩa, "
analyze_aapl_task
", hướng dẫn cụ thể agent tìm giá cổ phiếu mô phỏng cho AAPL bằng cách sử dụng công cụ. Mô tả tác vụ bao gồm các hướng dẫn rõ ràng về cách xử lý cả trường hợp thành công và thất bại khi sử dụng công cụ. Một "
Crew
" được tập hợp, bao gồm "
financial_analyst_agent
" và "
analyze_aapl_task
". Cài đặt "
verbose
" được bật cho cả agent và crew để cung cấp ghi log chi tiết trong quá trình thực thi. Phần chính của tập lệnh chạy tác vụ của crew bằng phương thức "
kickoff()
" trong một khối "
if __name__ == "__main__":
" tiêu chuẩn. Trước khi bắt đầu crew, nó kiểm tra xem biến môi trường "
OPENAI_API_KEY
" đã được đặt hay chưa, điều này là bắt buộc để agent hoạt động. Kết quả thực thi của crew, tức là đầu ra của tác vụ, sau đó được in ra console. Đoạn mã cũng bao gồm cấu hình logging cơ bản để theo dõi tốt hơn các hành động và lệnh gọi công cụ của crew. Nó sử dụng các biến môi trường để quản lý khóa API, mặc dù có lưu ý rằng các phương pháp an toàn hơn được khuyến nghị cho môi trường production. Tóm lại, logic cốt lõi cho thấy cách định nghĩa các công cụ, agent và tác vụ để tạo ra một quy trình làm việc cộng tác trong Crew.ai.

Mã thực hành (Google ADK)

Google Agent Developer Kit (ADK) bao gồm một thư viện các công cụ được tích hợp sẵn có thể được kết hợp trực tiếp vào các khả năng của agent.

Google search: Một ví dụ chính của thành phần như vậy là công cụ Google Search. Công cụ này phục vụ như một giao diện trực tiếp với công cụ tìm kiếm Google, trang bị cho agent chức năng thực hiện tìm kiếm trên web và truy xuất thông tin bên ngoài.

from google.adk.agents import Agent
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService
from google.adk.tools import google_search
from google.genai import types
import nest_asyncio
import asyncio


# Định nghĩa các biến cần thiết cho việc thiết lập Session và thực thi Agent
APP_NAME = "Google Search_agent"
USER_ID = "user1234"
SESSION_ID = "1234"


# Định nghĩa Agent có quyền truy cập vào công cụ tìm kiếm
root_agent = ADKAgent(
    name="basic_search_agent",
    model="gemini-2.0-flash-exp",
    description="Agent to answer questions using Google Search.",
    instruction="I can answer your questions by searching the internet. Just ask me anything!",
    tools=[google_search]  # Google Search là một công cụ được xây dựng sẵn để thực hiện các tìm kiếm của Google.
)


# Tương tác Agent
async def call_agent(query):
    """
    Hàm trợ giúp để gọi agent với một truy vấn.
    """
    # Session và Runner
    session_service = InMemorySessionService()
    session = await session_service.create_session(
        app_name=APP_NAME,
        user_id=USER_ID,
        session_id=SESSION_ID,
    )
    runner = Runner(agent=root_agent, app_name=APP_NAME, session_service=session_service)

    content = types.Content(role='user', parts=[types.Part(text=query)])
    events = runner.run(user_id=USER_ID, session_id=SESSION_ID, new_message=content)

    for event in events:
        if event.is_final_response():
            final_response = event.content.parts[0].text
            print("Agent Response: ", final_response)

nest_asyncio.apply()
asyncio.run(call_agent("what's the latest ai news?"))

"""
Đoạn mã này minh họa cách tạo và sử dụng một agent cơ bản được cung cấp bởi Google ADK cho Python. Agent này được thiết kế để trả lời các câu hỏi bằng cách sử dụng Google Search như một công cụ. Đầu tiên, các thư viện cần thiết từ IPython, google.adk và google.genai được nhập vào. Các hằng số cho tên ứng dụng, ID người dùng và ID phiên được định nghĩa. Một thực thể "
Agent
" có tên "basic_search_agent" được tạo với mô tả và hướng dẫn chỉ rõ mục đích của nó. Nó được cấu hình để sử dụng công cụ "
Google Search
", một công cụ được xây dựng sẵn do ADK cung cấp. Một "
InMemorySessionService
" (xem Chương 8) được khởi tạo để quản lý các phiên cho agent. Một phiên mới được tạo cho ứng dụng, ID người dùng và ID phiên đã chỉ định. Một "
Runner
" được khởi tạo, liên kết agent đã tạo với dịch vụ phiên. Runner này chịu trách nhiệm thực thi các tương tác của agent trong một phiên. Một hàm trợ giúp "
call_agent
" được định nghĩa để đơn giản hóa quá trình gửi truy vấn đến agent và xử lý phản hồi. Bên trong "
call_agent
", truy vấn của người dùng được định dạng thành một đối tượng "
types.Content
" với vai trò 'user'. Phương thức "
runner.run
" được gọi với ID người dùng, ID phiên và nội dung tin nhắn mới. Phương thức "
runner.run
" trả về một danh sách các sự kiện đại diện cho các hành động và phản hồi của agent. Đoạn mã lặp qua các sự kiện này để tìm phản hồi cuối cùng. Nếu một sự kiện được xác định là phản hồi cuối cùng, nội dung văn bản của phản hồi đó sẽ được trích xuất. Phản hồi của agent đã trích xuất sau đó được in ra console. Cuối cùng, hàm "
call_agent
" được gọi với truy vấn "what's the latest ai news?" để minh họa agent trong hành động.

Thực thi mã:

Google ADK có các thành phần tích hợp cho các tác vụ chuyên biệt, bao gồm một môi trường để thực thi mã động. Công cụ "
built_in_code_execution
" cung cấp cho agent một trình thông dịch Python trong môi trường sandbox. Điều này cho phép mô hình viết và chạy mã để thực hiện các tác vụ tính toán, thao tác với các cấu trúc dữ liệu và thực thi các kịch bản thủ tục. Chức năng như vậy rất quan trọng để giải quyết các vấn đề đòi hỏi logic tất định và các phép tính chính xác, vốn nằm ngoài phạm vi của việc tạo ngôn ngữ xác suất đơn thuần.

import os
import getpass
import asyncio
import nest_asyncio
import logging
from typing import List

from dotenv import load_dotenv
from google.adk.agents import Agent as ADKAgent, LlmAgent
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService
from google.adk.tools import google_search
from google.adk.code_executors import BuiltInCodeExecutor
from google.genai import types


# Định nghĩa các biến cần thiết cho việc thiết lập Session và thực thi Agent
APP_NAME = "calculator"
USER_ID = "user1234"
SESSION_ID = "session_code_exec_async"


# Định nghĩa Agent
code_agent = LlmAgent(
    name="calculator_agent",
    model="gemini-2.0-flash",
    code_executor=BuiltInCodeExecutor(),
    instruction="""
You are a calculator agent.
  When given a mathematical expression, write and execute Python code to calculate the result.
  Return only the final numerical result as plain text, without markdown or code blocks.
  """,
    description="Executes Python code to perform calculations.",
)


# Tương tác Agent (Bất đồng bộ)
async def call_agent_async(query):
    # Session và Runner
    session_service = InMemorySessionService()
    session = await session_service.create_session(
        app_name=APP_NAME,
        user_id=USER_ID,
        session_id=SESSION_ID,
    )
    runner = Runner(agent=code_agent, app_name=APP_NAME, session_service=session_service)

    content = types.Content(role="user", parts=[types.Part(text=query)])
    print(f"\n--- Running Query: {query} ---")

    final_response_text = "No final text response captured."

    try:
        # Sử dụng run_async
        async for event in runner.run_async(
            user_id=USER_ID,
            session_id=SESSION_ID,
            new_message=content,
        ):
            print(f"Event ID: {event.id}, Author: {event.author}")

            # --- Kiểm tra các phần cụ thể TRƯỚC TIÊN ---
            # has_specific_part = False
            if event.content and event.content.parts and event.is_final_response():
                for part in event.content.parts:  # Lặp qua tất cả các phần
                    if part.executable_code:
                        # Truy cập chuỗi mã thực tế thông qua .code
                        print(
                            f"  Debug: Agent generated code:\n```python\n{part.executable_code.code}\n```"
                        )
                        has_specific_part = True
                    elif part.code_execution_result:
                        # Truy cập outcome và output một cách chính xác
                        print(
                            f"  Debug: Code Execution Result: {part.code_execution_result.outcome} - Output:\n{part.code_execution_result.output}"
                        )
                        has_specific_part = True
                    # Cũng in bất kỳ phần văn bản nào được tìm thấy trong bất kỳ sự kiện nào để gỡ lỗi
                    elif part.text and not part.text.isspace():
                        print(f"  Text: '{part.text.strip()}'")
                        # Đừng đặt has_specific_part=True ở đây, vì chúng ta muốn logic phản hồi cuối cùng bên dưới

                # --- Kiểm tra phản hồi cuối cùng SAU các phần cụ thể ---
                text_parts = [part.text for part in event.content.parts if part.text]
                final_result = "".join(text_parts)
                print(f"==> Final Agent Response: {final_result}")

    except Exception as e:
        print(f"ERROR during agent run: {e}")

    print("-" * 30)


# Hàm async chính để chạy các ví dụ
async def main():
    await call_agent_async("Calculate the value of (5 + 7) * 3")
    await call_agent_async("What is 10 factorial?")


# Thực thi hàm async chính
try:
    nest_asyncio.apply()
    asyncio.run(main())
except RuntimeError as e:
    # Xử lý lỗi cụ thể khi chạy asyncio.run trong một vòng lặp sự kiện đã chạy (như Jupyter/Colab)
    if "cannot be called from a running event loop" in str(e):
        print("\nRunning in an existing event loop (like Colab/Jupyter).")
        print("Please run `await main()` in a notebook cell instead.")
        # Nếu trong một môi trường tương tác như notebook, bạn có thể cần chạy:
        # await main()
    else:
        raise e  # Nêu lại các lỗi runtime khác

"""
Tập lệnh này sử dụng Bộ công cụ Phát triển Agent của Google (ADK) để tạo ra một agent giải quyết các bài toán bằng cách viết và thực thi mã Python. Nó định nghĩa một "
LlmAgent
" được hướng dẫn cụ thể để hoạt động như một máy tính, trang bị cho nó công cụ "
built_in_code_execution
". Logic chính nằm trong hàm "
call_agent_async
", hàm này gửi một truy vấn của người dùng đến "
runner
" của agent và xử lý các sự kiện kết quả. Bên trong hàm này, một vòng lặp bất đồng bộ lặp qua các sự kiện, in ra mã Python được tạo và kết quả thực thi của nó để gỡ lỗi. Đoạn mã phân biệt cẩn thận giữa các bước trung gian này và sự kiện cuối cùng chứa câu trả lời bằng số. Cuối cùng, một hàm "
main
" chạy agent với hai biểu thức toán học khác nhau để minh họa khả năng thực hiện các phép tính của nó.

Tìm kiếm doanh nghiệp:

Đoạn mã này định nghĩa một ứng dụng Google ADK bằng thư viện "
google.adk
" trong Python. Nó đặc biệt sử dụng một "
VSearchAgent
", được thiết kế để trả lời các câu hỏi bằng cách tìm kiếm một kho dữ liệu (datastore) Vertex AI Search cụ thể. Đoạn mã khởi tạo một "
VSearchAgent
" có tên "q2_strategy_vsearch_agent", cung cấp mô tả, mô hình sử dụng ("gemini-2.0-flash-exp") và ID của kho dữ liệu Vertex AI Search. "
DATASTORE_ID
" dự kiến sẽ được đặt làm biến môi trường. Sau đó, nó thiết lập một "
Runner
" cho agent, sử dụng "
InMemorySessionService
" để quản lý lịch sử cuộc trò chuyện. Một hàm bất đồng bộ "
call_vsearch_agent_async
" được định nghĩa để tương tác với agent. Hàm này nhận một truy vấn, xây dựng một đối tượng nội dung tin nhắn và gọi phương thức "
run_async
" của runner để gửi truy vấn đến agent. Hàm này sau đó truyền (stream) phản hồi của agent trở lại console khi nó đến. Nó cũng in thông tin về phản hồi cuối cùng, bao gồm bất kỳ ghi nhận nguồn (source attributions) nào từ kho dữ liệu. Xử lý lỗi được bao gồm để bắt các ngoại lệ trong quá trình thực thi của agent, cung cấp các thông báo thông tin về các vấn đề tiềm ẩn như ID kho dữ liệu không chính xác hoặc thiếu quyền. Một hàm bất đồng bộ khác "
run_vsearch_example
" được cung cấp để minh họa cách gọi agent với các truy vấn ví dụ. Khối thực thi chính kiểm tra xem "
DATASTORE_ID
" đã được đặt hay chưa và sau đó chạy ví dụ bằng "
asyncio.run
". Nó bao gồm một kiểm tra để xử lý các trường hợp mã được chạy trong một môi trường đã có vòng lặp sự kiện đang chạy, như một máy tính xách tay Jupyter (Jupyter notebook).

import os
import asyncio

from google.genai import types
from google.adk import agents
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService


# --- Cấu hình ---
# Đảm bảo bạn đã đặt các biến môi trường GOOGLE_API_KEY và DATASTORE_ID
# Ví dụ:
# os.environ["GOOGLE_API_KEY"] = "YOUR_API_KEY"
# os.environ["DATASTORE_ID"] = "YOUR_DATASTORE_ID"
DATASTORE_ID = os.environ.get("DATASTORE_ID")


# --- Các hằng số ứng dụng ---
APP_NAME = "vsearch_app"
USER_ID = "user_123"   # ID người dùng ví dụ
SESSION_ID = "session_456"  # ID phiên ví dụ


# --- Định nghĩa Agent (Đã cập nhật với mô hình mới hơn từ hướng dẫn) ---
vsearch_agent = agents.VSearchAgent(
    name="q2_strategy_vsearch_agent",
    description="Answers questions about Q2 strategy documents using Vertex AI Search.",
    model="gemini-2.0-flash-exp",  # Mô hình được cập nhật dựa trên các ví dụ của hướng dẫn
    datastore_id=DATASTORE_ID,
    model_parameters={"temperature": 0.0},
)


# --- Khởi tạo Runner và Session ---
runner = Runner(
    agent=vsearch_agent,
    app_name=APP_NAME,
    session_service=InMemorySessionService(),
)


# --- Logic Gọi Agent ---
async def call_vsearch_agent_async(query: str):
    """Khởi tạo một phiên và truyền (stream) phản hồi của agent."""
    print(f"User: {query}")
    print("Agent: ", end="", flush=True)

    try:
        # Xây dựng nội dung tin nhắn một cách chính xác
        content = types.Content(role="user", parts=[types.Part(text=query)])

        # Xử lý các sự kiện khi chúng đến từ runner bất đồng bộ
        async for event in runner.run_async(
            user_id=USER_ID,
            session_id=SESSION_ID,
            new_message=content,
        ):
            # Để truyền (stream) văn bản phản hồi theo từng token
            if hasattr(event, "content_part_delta") and event.content_part_delta:
                print(event.content_part_delta.text, end="", flush=True)

            # Xử lý phản hồi cuối cùng và siêu dữ liệu (metadata) liên quan của nó
            if event.is_final_response():
                print()  # Xuống dòng mới sau phản hồi truyền (stream)
                if event.grounding_metadata:
                    print(
                        f"  (Source Attributions: "
                        f"{len(event.grounding_metadata.grounding_attributions)} sources found)"
                    )
                else:
                    print("  (No grounding metadata found)")
                print("-" * 30)

    except Exception as e:
        print(f"\nAn error occurred: {e}")
        print(
            "Please ensure your datastore ID is correct and that the service account "
            "has the necessary permissions."
        )
        print("-" * 30)


# --- Chạy Ví dụ ---
async def run_vsearch_example():
    # Thay thế bằng một câu hỏi liên quan đến nội dung kho dữ liệu CỦA BẠN
    await call_vsearch_agent_async("Summarize the main points about the Q2 strategy document.")
    await call_vsearch_agent_async("What safety procedures are mentioned for lab X?")


# --- Thực thi ---
if __name__ == "__main__":
    if not DATASTORE_ID:
        print("Error: DATASTORE_ID environment variable is not set.")
    else:
        try:
            asyncio.run(run_vsearch_example())
        except RuntimeError as e:
            # Điều này xử lý các trường hợp khi asyncio.run được gọi trong một môi trường
            # đã có một vòng lặp sự kiện đang chạy (như Jupyter notebook).
            if "cannot be called from a running event loop" in str(e):
                print("Skipp
Nhìn chung, đoạn mã này cung cấp một framework cơ bản để xây dựng một ứng dụng AI đàm thoại tận dụng Vertex AI Search để trả lời các câu hỏi dựa trên thông tin được lưu trữ trong một kho dữ liệu. Nó minh họa cách định nghĩa một agent, thiết lập một runner và tương tác với agent một cách bất đồng bộ trong khi truyền (stream) phản hồi. Trọng tâm là truy xuất và tổng hợp thông tin từ một kho dữ liệu cụ thể để trả lời các truy vấn của người dùng.

Vertex Extensions (Tiện ích mở rộng của Vertex):

Một tiện ích mở rộng của Vertex AI là một trình bao bọc API có cấu trúc (structured API wrapper) cho phép mô hình kết nối với các API bên ngoài để xử lý dữ liệu và thực thi hành động theo thời gian thực. Các tiện ích mở rộng cung cấp các đảm bảo về bảo mật, quyền riêng tư dữ liệu và hiệu suất cấp doanh nghiệp. Chúng có thể được sử dụng cho các tác vụ như tạo và chạy mã, truy vấn các trang web và phân tích thông tin từ các kho dữ liệu riêng tư. Google cung cấp các tiện ích mở rộng được xây dựng sẵn cho các trường hợp sử dụng phổ biến như Code Interpreter (Trình thông dịch mã) và Vertex AI Search, với tùy chọn tạo các tiện ích mở rộng tùy chỉnh. Lợi ích chính của các tiện ích mở rộng bao gồm các kiểm soát doanh nghiệp mạnh mẽ và tích hợp liền mạch với các sản phẩm khác của Google. Sự khác biệt chính giữa tiện ích mở rộng và gọi hàm nằm ở việc thực thi chúng: Vertex AI tự động thực thi các tiện ích mở rộng, trong khi các lệnh gọi hàm yêu cầu người dùng hoặc máy khách (client) thực thi thủ công.

Tóm tắt nhanh

Vấn đề là gì:

Các LLM là những cỗ máy tạo văn bản mạnh mẽ, nhưng về cơ bản chúng bị ngắt kết nối với thế giới bên ngoài. Kiến thức của chúng là tĩnh, bị giới hạn trong dữ liệu mà chúng được huấn luyện, và chúng thiếu khả năng thực hiện các hành động hoặc truy xuất thông tin thời gian thực. Hạn chế cố hữu này ngăn cản chúng hoàn thành các tác vụ đòi hỏi tương tác với các API, cơ sở dữ liệu hoặc dịch vụ bên ngoài. Nếu không có cầu nối đến các hệ thống bên ngoài này, tiện ích của chúng để giải quyết các vấn đề trong thế giới thực bị hạn chế nghiêm trọng.

Tại sao (cần giải pháp):

Mẫu hình Sử dụng Công cụ, thường được triển khai thông qua gọi hàm, cung cấp một giải pháp tiêu chuẩn hóa cho vấn đề này. Nó hoạt động bằng cách mô tả các hàm bên ngoài có sẵn, hoặc "công cụ", cho LLM theo cách mà nó có thể hiểu được. Dựa trên yêu cầu của người dùng, LLM của agent sau đó có thể quyết định xem có cần một công cụ hay không và tạo ra một đối tượng dữ liệu có cấu trúc (như JSON) chỉ định hàm nào cần gọi và với các đối số nào. Một lớp điều phối sẽ thực thi lệnh gọi hàm này, truy xuất kết quả và cung cấp lại cho LLM. Điều này cho phép LLM kết hợp thông tin bên ngoài, cập nhật hoặc kết quả của một hành động vào phản hồi cuối cùng của nó, giúp nó có khả năng hành động một cách hiệu quả.

Nguyên tắc chung:

Sử dụng mẫu hình Sử dụng Công cụ bất cứ khi nào một agent cần thoát ra khỏi kiến thức nội tại của LLM và tương tác với thế giới bên ngoài. Điều này là cần thiết cho các tác vụ đòi hỏi dữ liệu thời gian thực (ví dụ: kiểm tra thời tiết, giá cổ phiếu), truy cập thông tin cá nhân hoặc độc quyền (ví dụ: truy vấn cơ sở dữ liệu của công ty), thực hiện các phép tính chính xác, thực thi mã, hoặc kích hoạt các hành động trong các hệ thống khác (ví dụ: gửi email, điều khiển thiết bị thông minh). 

Tóm tắt trực quan:

<figure> <img src="../imgs/fig.5.2.Tool_use_design_pattern.png" alt="fig.5.2.Tool_use_design_pattern"> <figcaption>Hình 2: Mẫu hình thiết kế sử dụng công cụ</figcaption> </figure>

Những điểm chính cần ghi nhớ

Sử dụng Công cụ (Gọi hàm) cho phép các agent tương tác với các hệ thống bên ngoài và truy cập thông tin động.

Nó liên quan đến việc định nghĩa các công cụ với các mô tả và tham số rõ ràng mà LLM có thể hiểu được.

LLM quyết định khi nào sử dụng một công cụ và tạo ra các lệnh gọi hàm có cấu trúc.

Các framework của agent thực thi các lệnh gọi công cụ thực tế và trả kết quả về cho LLM.

Sử dụng Công cụ là điều cần thiết để xây dựng các agent có thể thực hiện các hành động trong thế giới thực và cung cấp thông tin cập nhật.

LangChain đơn giản hóa việc định nghĩa công cụ bằng cách sử dụng decorator "
@tool
" và cung cấp "
create_tool_calling_agent
" cũng như "
AgentExecutor
" để xây dựng các agent sử dụng công cụ.

Google ADK có một số công cụ được xây dựng sẵn rất hữu ích như Google Search, Code Execution (Thực thi mã) và Vertex AI Search Tool.

Kết luận

Mẫu hình Sử dụng Công cụ là một nguyên tắc kiến trúc quan trọng để mở rộng phạm vi chức năng của các mô hình ngôn ngữ lớn vượt ra ngoài khả năng tạo văn bản nội tại của chúng. Bằng cách trang bị cho mô hình khả năng giao tiếp với phần mềm và các nguồn dữ liệu bên ngoài, mô hình này cho phép một agent thực hiện các hành động, thực thi các phép tính và truy xuất thông tin từ các hệ thống khác. Quá trình này liên quan đến việc mô hình tạo ra một yêu cầu có cấu trúc để gọi một công cụ bên ngoài khi nó xác định rằng làm như vậy là cần thiết để hoàn thành truy vấn của người dùng. Các framework như LangChain, Google ADK và Crew AI cung cấp các thành phần và sự trừu tượng hóa có cấu trúc (structured abstractions) tạo điều kiện thuận lợi cho việc tích hợp các công cụ bên ngoài này. Các framework này quản lý quá trình hiển thị các thông số kỹ thuật của công cụ cho mô hình và phân tích cú pháp các yêu cầu sử dụng công cụ tiếp theo của nó. Điều này đơn giản hóa việc phát triển các hệ thống agent phức tạp có thể tương tác và thực hiện hành động trong các môi trường kỹ thuật số bên ngoài.

Tài liệu tham khảo

Tài liệu LangChain (Công cụ): 
https://python.langchain.com/docs/integrations/tools/

Tài liệu Google Agent Developer Kit (ADK) (Công cụ): 
https://google.github.io/adk-docs/tools/

Tài liệu Gọi hàm của OpenAI: 
https://platform.openai.com/docs/guides/function-calling

Tài liệu CrewAI (Công cụ): 
https://docs.crewai.com/concepts/tools

```