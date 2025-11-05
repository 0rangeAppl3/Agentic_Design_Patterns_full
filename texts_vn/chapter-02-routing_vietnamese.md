Chương 2: Định tuyến (Routing)

Tổng quan về Mẫu hình Định tuyến

Mặc dù xử lý tuần tự thông qua xâu chuỗi prompt là một kỹ thuật nền tảng để thực thi các quy trình công việc tuyến tính, tất định với các mô hình ngôn ngữ, khả năng áp dụng của nó bị hạn chế trong các tình huống đòi hỏi phản ứng thích ứng. Các hệ thống có tính tác tử (agentic systems) trong thế giới thực thường phải phân xử giữa nhiều hành động tiềm năng dựa trên các yếu tố ngẫu nhiên, chẳng hạn như trạng thái của môi trường, đầu vào của người dùng hoặc kết quả của một hoạt động trước đó. Năng lực ra quyết định động này, chi phối luồng kiểm soát đến các chức năng, công cụ hoặc quy trình con chuyên biệt khác nhau, đạt được thông qua một cơ chế được gọi là định tuyến.

Định tuyến đưa logic điều kiện vào khung hoạt động của tác tử, cho phép chuyển đổi từ một đường dẫn thực thi cố định sang một mô hình mà tác tử tự động đánh giá các tiêu chí cụ thể để lựa chọn từ một tập hợp các hành động tiếp theo có thể có. Điều này cho phép hành vi hệ thống linh hoạt và nhận thức được ngữ cảnh hơn.

Ví dụ, một tác tử được thiết kế cho các yêu cầu của khách hàng, khi được trang bị chức năng định tuyến, trước tiên có thể phân loại một truy vấn đến để xác định ý định của người dùng. Dựa trên phân loại này, nó sau đó có thể chuyển hướng truy vấn đến một tác tử chuyên biệt để trả lời câu hỏi trực tiếp, một công cụ truy xuất cơ sở dữ liệu để lấy thông tin tài khoản, hoặc một quy trình leo thang cho các vấn ...

Vì vậy, một tác tử tinh vi hơn sử dụng định tuyến có thể:

Phân tích truy vấn của người dùng.

Định tuyến truy vấn dựa trên ý định của nó:

Nếu ý định là "kiểm tra trạng thái đơn hàng", định tuyến đến một tác tử con hoặc chuỗi công cụ tương tác với cơ sở dữ liệu đơn hàng.

Nếu ý định là "thông tin sản phẩm", định tuyến đến một tác tử con hoặc chuỗi tìm kiếm danh mục sản phẩm.

Nếu ý định là "hỗ trợ kỹ thuật", định tuyến đến một chuỗi khác truy cập hướng dẫn khắc phục sự cố hoặc leo thang lên con người.

Nếu ý định là "không rõ ràng", định tuyến đến một tác tử con làm rõ hoặc chuỗi prompt làm rõ.

Thành phần cốt lõi của mẫu hình Định tuyến là một cơ chế thực hiện việc đánh giá và điều hướng luồng. Cơ chế này có thể được thực hiện theo nhiều cách:

Định tuyến dựa trên LLM (LLM-based Routing): Bản thân mô hình ngôn ngữ có thể được prompt để phân tích đầu vào và đưa ra một mã định danh hoặc hướng dẫn cụ thể cho biết bước hoặc đích tiếp theo. Ví dụ, một prompt có thể yêu cầu LLM "Phân tích truy vấn người dùng sau đây và chỉ xuất ra danh mục: 'Trạng thái đơn hàng', 'Thông tin sản phẩm', 'Hỗ trợ kỹ thuật' hoặc 'Khác'." Hệ thống tác tử sau đó đọc đầu ra này và điều hướng quy trình làm việc tương ứng.

Định tuyến dựa trên Nhúng (Embedding-based Routing): Truy vấn đầu vào có thể được chuyển đổi thành một nhúng véc-tơ (vector embedding) (xem RAG, Chương 14). Nhúng này sau đó được so sánh với các nhúng đại diện cho các tuyến hoặc khả năng khác nhau. Truy vấn được định tuyến đến tuyến có nhúng tương tự nhất. Điều này hữu ích cho định tuyến ngữ nghĩa (semantic routing), nơi quyết định dựa trên ý nghĩa của đầu vào chứ không chỉ là từ khóa.

Định tuyến dựa trên Quy tắc (Rule-based Routing): Điều này liên quan đến việc sử dụng các quy tắc hoặc logic được xác định trước (ví dụ: câu lệnh if-else, trường hợp switch) dựa trên các từ khóa, mẫu hoặc dữ liệu có cấu trúc được trích xuất từ đầu vào. Điều này có thể nhanh hơn và tất định hơn định tuyến dựa trên LLM, nhưng kém linh hoạt hơn trong việc xử lý các đầu vào đa sắc thái hoặc mới lạ.

Định tuyến dựa trên Mô hình Học máy (Machine Learning Model-Based Routing): Nó sử dụng một mô hình phân biệt (discriminative model), chẳng hạn như một bộ phân loại (classifier), đã được huấn luyện đặc biệt trên một kho dữ liệu nhỏ có gán nhãn để thực hiện tác vụ định tuyến. Mặc dù nó có những điểm tương đồng về mặt khái niệm với các phương pháp dựa trên nhúng, đặc điểm chính của nó là quy trình tinh chỉnh có giám sát (supervised fine-tuning), điều chỉnh các tham số của mô hình để tạo ra một chức năng định tuyến chuyên biệt. Kỹ thuật này khác biệt với định tuyến dựa trên LLM vì thành phần ra quyết định không phải là một mô hình sinh (generative model) thực thi một prompt tại thời điểm suy luận (inference time). Thay vào đó, logic định tuyến được mã hóa bên trong các trọng số đã học của mô hình được tinh chỉnh. Mặc dù LLM có thể được sử dụng trong bước tiền xử lý để tạo dữ liệu tổng hợp nhằm tăng cường tập huấn luyện, chúng không tham gia vào quyết định định tuyến thời gian thực.

Các cơ chế định tuyến có thể được thực hiện tại nhiều thời điểm trong chu trình hoạt động của tác tử. Chúng có thể được áp dụng ngay từ đầu để phân loại một tác vụ chính, tại các điểm trung gian trong một chuỗi xử lý để xác định một hành động tiếp theo, hoặc trong một chương trình con để chọn công cụ thích hợp nhất từ một tập hợp nhất định.

Các khung tính toán (Computational frameworks) như LangChain, LangGraph và Bộ công cụ phát triển tác tử của Google (Google's Agent Developer Kit - ADK) cung cấp các cấu trúc rõ ràng để xác định và quản lý logic điều kiện như vậy. Với kiến trúc đồ thị dựa trên trạng thái, LangGraph đặc biệt phù hợp cho các kịch bản định tuyến phức tạp, nơi các quyết định phụ thuộc vào trạng thái tích lũy của toàn bộ hệ thống. Tương tự, ADK của Google cung cấp các thành phần nền tảng để cấu trúc các khả năng và mô hình tương tác của tác tử, làm cơ sở để thực hiện logic định tuyến. Trong các môi trường thực thi được cung cấp bởi các khung này, các nhà phát triển xác định các đường dẫn hoạt động có thể có và các hàm hoặc đánh giá dựa trên mô hình quyết định sự chuyển đổi giữa các nút trong đồ thị tính toán.

Việc triển khai định tuyến cho phép một hệ thống vượt ra ngoài xử lý tuần tự tất định. Nó tạo điều kiện cho sự phát triển của các luồng thực thi thích ứng hơn có thể phản ứng linh hoạt và thích hợp với một loạt các đầu vào và thay đổi trạng thái rộng hơn.

Ứng dụng thực tế & Các trường hợp sử dụng

Mẫu hình định tuyến là một cơ chế kiểm soát quan trọng trong thiết kế các hệ thống tác tử thích ứng, cho phép chúng tự động thay đổi đường dẫn thực thi của mình để phản ứng với các đầu vào biến đổi và trạng thái nội bộ. Tiện ích của nó trải rộng trên nhiều lĩnh vực bằng cách cung cấp một lớp logic điều kiện cần thiết.

Trong tương tác giữa người và máy, chẳng hạn như với các trợ lý ảo hoặc gia sư do AI điều khiển, định tuyến được sử dụng để diễn giải ý định của người dùng. Một phân tích ban đầu về truy vấn ngôn ngữ tự nhiên sẽ xác định hành động tiếp theo thích hợp nhất, cho dù đó là gọi một công cụ truy xuất thông tin cụ thể, leo thang lên một nhà điều hành con người, hay chọn mô-đun tiếp theo trong một chương trình giảng dạy dựa trên hiệu suất của người dùng. Điều này cho phép hệ thống vượt ra ngoài các luồng đối thoại tuyến tính và phản hồi theo ngữ cảnh.

Trong các đường ống xử lý tài liệu và dữ liệu tự động, định tuyến phục vụ như một chức năng phân loại và phân phối. Dữ liệu đến, chẳng hạn như email, phiếu hỗ trợ hoặc các gói dữ liệu API (API payloads), được phân tích dựa trên nội dung, siêu dữ liệu hoặc định dạng. Hệ thống sau đó điều hướng từng mục đến một quy trình làm việc tương ứng, chẳng hạn như quy trình nhập khách hàng tiềm năng bán hàng, chức năng chuyển đổi dữ liệu cụ thể cho các định dạng JSON hoặc CSV, hoặc một đường dẫn leo thang vấn đề khẩn cấp.

Trong các hệ thống phức tạp liên quan đến nhiều công cụ hoặc tác tử chuyên biệt, định tuyến hoạt động như một bộ điều phối cấp cao. Một hệ thống nghiên cứu bao gồm các tác tử riêng biệt để tìm kiếm, tóm tắt và phân tích thông tin sẽ sử dụng một bộ định tuyến để gán nhiệm vụ cho tác tử phù hợp nhất dựa trên mục tiêu hiện tại. Tương tự, một trợ lý lập trình AI sử dụng định tuyến để xác định ngôn ngữ lập trình và ý định của người dùng—để gỡ lỗi, giải thích hoặc dịch—trước khi chuyển một đoạn mã cho công cụ chuyên biệt chính xác.

Cuối cùng, định tuyến cung cấp khả năng phân xử logic cần thiết để tạo ra các hệ thống đa dạng về chức năng và nhận thức được ngữ cảnh. Nó biến đổi một tác tử từ một người thực thi tĩnh các chuỗi được xác định trước thành một hệ thống động có thể đưa ra quyết định về phương pháp hiệu quả nhất để hoàn thành một tác vụ trong các điều kiện thay đổi.

Ví dụ Mã Thực hành (LangChain)

Thực hiện định tuyến trong mã bao gồm việc xác định các đường dẫn có thể có và logic quyết định đường dẫn nào sẽ thực hiện. Các khung như LangChain và LangGraph cung cấp các thành phần và cấu trúc cụ thể cho việc này. Cấu trúc đồ thị dựa trên trạng thái của LangGraph đặc biệt trực quan để hình dung và thực hiện logic định tuyến.

Mã này trình diễn một hệ thống giống như tác tử đơn giản sử dụng LangChain và AI tạo sinh của Google. Nó thiết lập một "điều phối viên" (coordinator) định tuyến các yêu cầu của người dùng đến các trình xử lý "tác tử con" (sub-agent) mô phỏng khác nhau dựa trên ý định của yêu cầu (đặt chỗ, thông tin hoặc không rõ ràng). Hệ thống sử dụng một mô hình ngôn ngữ để phân loại yêu cầu và sau đó ủy thác nó cho hàm xử lý thích hợp, mô phỏng một mẫu hình ủy thác cơ bản thường thấy trong các kiến trúc đa tác tử.

Đầu tiên, hãy đảm bảo bạn đã cài đặt các thư viện cần thiết:

pip install langchain langgraph google-cloud-aiplatform langchain-google-genai google-adk deprecated pydantic

Bạn cũng sẽ cần thiết lập môi trường của mình với khóa API cho mô hình ngôn ngữ bạn chọn (ví dụ: OpenAI, Google Gemini, Anthropic).

Python
# Copyright (c) 2025 Marco Fago
#
# This code is licensed under the MIT License.
# See the LICENSE file in the repository for the full license text.

from langchain_google_genai import ChatGoogleGenerativeAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser
from langchain_core.runnables import RunnablePassthrough, RunnableBranch

# --- Cấu hình ---
# Đảm bảo biến môi trường khóa API của bạn được đặt (ví dụ: GOOGLE_API_KEY)
try:
    llm = ChatGoogleGenerativeAI(model="gemini-2.5-flash", temperature=0)
    print(f"Đã khởi tạo mô hình ngôn ngữ: {llm.model}")
except Exception as e:
    print(f"Lỗi khi khởi tạo mô hình ngôn ngữ: {e}")
    llm = None

# --- Định nghĩa các Trình xử lý Tác tử con Mô phỏng (tương đương với sub_agents của ADK) ---
def booking_handler(request: str) -> str:
    """Mô phỏng Tác tử Đặt chỗ xử lý một yêu cầu."""
    print("\n--- ĐANG ỦY THÁC CHO TRÌNH XỬ LÝ ĐẶT CHỖ ---")
    return f"Trình xử lý Đặt chỗ đã xử lý yêu cầu: '{request}'. Kết quả: Hành động đặt chỗ mô phỏng."
def info_handler(request: str) -> str:
    """Mô phỏng Tác tử Thông tin xử lý một yêu cầu."""
    print("\n--- ĐANG ỦY THÁC CHO TRÌNH XỬ LÝ THÔNG TIN ---")
    return f"Trình xử lý Thông tin đã xử lý yêu cầu: '{request}'. Kết quả: Truy xuất thông tin mô phỏng."
def unclear_handler(request: str) -> str:
    """Xử lý các yêu cầu không thể ủy thác."""
    print("\n--- ĐANG XỬ LÝ YÊU CẦU KHÔNG RÕ RÀNG ---")
    return f"Điều phối viên không thể ủy thác yêu cầu: '{request}'. Vui lòng làm rõ."

# --- Định nghĩa Chuỗi Bộ định tuyến Điều phối viên (tương đương với hướng dẫn của điều phối viên ADK) ---
# Chuỗi này quyết định ủy thác cho trình xử lý nào. 
coordinator_router_prompt = ChatPromptTemplate.from_messages([
   ("system", """Phân tích yêu cầu của người dùng và xác định trình xử lý chuyên môn nào nên xử lý nó.
     - Nếu yêu cầu liên quan đến đặt vé máy bay hoặc khách sạn,        
     xuất ra 'booker'.     
     - Đối với tất cả các câu hỏi thông tin chung khác, xuất ra 'info'.     
     - Nếu yêu cầu không rõ ràng hoặc không phù hợp với cả hai loại,        
     xuất ra 'unclear'.     
     CHỈ xuất ra một từ: 'booker', 'info', hoặc 'unclear'"""),
   ("user", "{request}") ])
   if llm:
       coordinator_router_chain = coordinator_router_prompt | llm | StrOutputParser() 
       
# --- Định nghĩa Logic Ủy thác (tương đương với Auto-Flow dựa trên sub_agents của ADK) ---
# Sử dụng RunnableBranch để định tuyến dựa trên đầu ra của chuỗi bộ định tuyến. 
# Định nghĩa các nhánh cho RunnableBranch 
branches = {    
   "booker": RunnablePassthrough.assign(output=lambda x: booking_handler(x['request']['request'])),    
   "info": RunnablePassthrough.assign(output=lambda x: info_handler(x['request']['request'])),    
   "unclear": RunnablePassthrough.assign(output=lambda x: unclear_handler(x['request']['request'])), } 
   
# Tạo RunnableBranch. Nó nhận đầu ra của chuỗi bộ định tuyến 
# và định tuyến đầu vào ban đầu ('request') đến trình xử lý tương ứng. delegation_branch = RunnableBranch(
   (lambda x: x['decision'].strip() == 'booker', branches["booker"]),
   (lambda x: x['decision'].strip() == 'info', branches["info"]),     
   branches["unclear"] # Default branch for 'unclear' or any other output 
   )

# Kết hợp chuỗi bộ định tuyến và nhánh ủy thác thành một runnable duy nhất 
# Đầu ra của chuỗi bộ định tuyến ('decision') được chuyển cùng với đầu vào ban đầu ('request') 
# đến delegation_branch. 
coordinator_agent = {    
   "decision": coordinator_router_chain,    
   "request": RunnablePassthrough() 
   } | delegation_branch | (lambda x: x['output']) 
   
   # Trích xuất đầu ra cuối cùng 
   # --- Ví dụ Sử dụng ---
   def main():    
      if not llm:
         print("\nBỏ qua thực thi do lỗi khởi tạo LLM.")
         return    
      print("--- Đang chạy với một yêu cầu đặt chỗ ---")
      request_a = "Book me a flight to London."
      result_a = coordinator_agent.invoke({"request": request_a})
      print(f"Kết quả cuối cùng A: {result_a}")
      print("\n--- Đang chạy với một yêu cầu thông tin ---")
      request_b = "What is the capital of Italy?"
      result_b = coordinator_agent.invoke({"request": request_b})
      print(f"Kết quả cuối cùng B: {result_b}")
      print("\n--- Đang chạy với một yêu cầu không rõ ràng ---")
      request_c = "Tell me about quantum physics."
      result_c = coordinator_agent.invoke({"request": request_c})
      print(f"Kết quả cuối cùng C: {result_c}") 
      
if __name__ == "__main__":    
   import nest_asyncio
    nest_asyncio.apply()
    await main()


Tập lệnh này bao gồm một tác tử Điều phối viên (Coordinator) chính và hai sub_agents (tác tử con) chuyên biệt: Booker và Info. Mỗi tác tử chuyên biệt được trang bị một FunctionTool (Công cụ Hàm) bao bọc một hàm Python mô phỏng một hành động. Hàm booking_handler mô phỏng việc xử lý đặt vé máy bay và khách sạn, trong khi hàm info_handler mô phỏng việc truy xuất thông tin chung. unclear_handler được bao gồm như một giải pháp dự phòng cho các yêu cầu mà điều phối viên không thể ủy thác, mặc dù logic điều phối viên hiện tại không sử dụng nó một cách rõ ràng cho thất bại ủy thác trong hàm run_coordinator chính.

Vai trò chính của tác tử Điều phối viên, như được định nghĩa trong instruction (hướng dẫn) của nó, là phân tích các tin nhắn đến của người dùng và ủy thác chúng cho tác tử Booker hoặc Info. Việc ủy thác này được xử lý tự động bởi cơ chế Auto-Flow của ADK vì Điều phối viên đã định nghĩa các sub_agents. Hàm run_coordinator thiết lập một InMemoryRunner, tạo ID người dùng và phiên, sau đó sử dụng runner để xử lý yêu cầu của người dùng thông qua tác tử điều phối viên. Phương thức runner.run xử lý yêu cầu và tạo ra các sự kiện (events), và mã trích xuất văn bản phản hồi cuối cùng từ event.content.

Hàm main trình diễn việc sử dụng hệ thống bằng cách chạy điều phối viên với các yêu cầu khác nhau, cho thấy cách nó ủy thác các yêu cầu đặt chỗ cho Booker và các yêu cầu thông tin cho tác tử Info.

Tóm tắt nhanh

Vấn đề là gì: Các hệ thống tác tử thường phải phản ứng với nhiều loại đầu vào và tình huống khác nhau mà không thể được xử lý bởi một quy trình tuyến tính, duy nhất. Một quy trình công việc tuần tự đơn giản thiếu khả năng đưa ra quyết định dựa trên ngữ cảnh. Nếu không có cơ chế để chọn đúng công cụ hoặc quy trình con cho một tác vụ cụ thể, hệ thống vẫn cứng nhắc và không thích ứng. Hạn chế này gây khó khăn cho việc xây dựng các ứng dụng tinh vi có thể quản lý sự phức tạp và biến đổi của các yêu cầu người dùng trong thế giới thực.

Tại sao (sử dụng mẫu hình này): Mẫu hình Định tuyến cung cấp một giải pháp tiêu chuẩn hóa bằng cách đưa logic điều kiện vào khung hoạt động của tác tử. Nó cho phép hệ thống trước tiên phân tích một truy vấn đến để xác định ý định hoặc bản chất của nó. Dựa trên phân tích này, tác tử tự động điều hướng luồng kiểm soát đến công cụ, chức năng hoặc tác tử con chuyên biệt thích hợp nhất. Quyết định này có thể được thúc đẩy bởi các phương pháp khác nhau, bao gồm cả việc prompt LLM, áp dụng các quy tắc được xác định trước, hoặc sử dụng sự tương đồng ngữ nghĩa dựa trên nhúng. Cuối cùng, định tuyến biến đổi một đường dẫn thực thi tĩnh, được xác định trước thành một quy trình làm việc linh hoạt và nhận thức được ngữ cảnh, có khả năng lựa chọn hành động tốt nhất có thể.

Quy tắc chung: Sử dụng mẫu hình Định tuyến khi một tác tử phải quyết định giữa nhiều quy trình công việc, công cụ hoặc tác tử con riêng biệt dựa trên đầu vào của người dùng hoặc trạng thái hiện tại. Nó cần thiết cho các ứng dụng cần phân loại (triage) hoặc phân loại các yêu cầu đến để xử lý các loại tác vụ khác nhau, chẳng hạn như một bot hỗ trợ khách hàng phân biệt giữa các yêu cầu bán hàng, hỗ trợ kỹ thuật và các câu hỏi quản lý tài khoản.

Tóm tắt trực quan:

<figure> <img src="../img/fig,2.1.router_pattern_using_a llm_as_a_router.png" alt="Mẫu hình định tuyến, sử dụng LLM làm Bộ định tuyến" width="500" height="300"> <figcaption>Hình 1: Mẫu hình định tuyến, sử dụng LLM làm Bộ định tuyến</figcaption> </figure>

Những điểm chính cần nhớ

Định tuyến cho phép các tác tử đưa ra quyết định động về bước tiếp theo trong một quy trình làm việc dựa trên các điều kiện.

Nó cho phép các tác tử xử lý các đầu vào đa dạng và điều chỉnh hành vi của chúng, vượt ra ngoài việc thực thi tuyến tính.

Logic định tuyến có thể được thực hiện bằng cách sử dụng LLM, các hệ thống dựa trên quy tắc hoặc sự tương đồng nhúng.

Các khung như LangGraph và Google ADK cung cấp các cách có cấu trúc để xác định và quản lý định tuyến trong các quy trình làm việc của tác tử, mặc dù với các phương pháp kiến trúc khác nhau.

Kết luận

Mẫu hình Định tuyến là một bước quan trọng trong việc xây dựng các hệ thống tác tử thực sự động và phản ứng nhanh. Bằng cách thực hiện định tuyến, chúng ta vượt ra ngoài các luồng thực thi tuyến tính, đơn giản và trao quyền cho các tác tử của mình đưa ra quyết định thông minh về cách xử lý thông tin, phản hồi đầu vào của người dùng và sử dụng các công cụ hoặc tác tử con có sẵn.

Chúng ta đã thấy cách định tuyến có thể được áp dụng trong các lĩnh vực khác nhau, từ chatbot dịch vụ khách hàng đến các đường ống xử lý dữ liệu phức tạp. Khả năng phân tích đầu vào và điều hướng có điều kiện quy trình làm việc là nền tảng để tạo ra các tác tử có thể xử lý sự biến đổi vốn có của các tác vụ trong thế giới thực.

Các ví dụ mã sử dụng LangChain và Google ADK trình diễn hai cách tiếp cận khác nhau nhưng hiệu quả để thực hiện định tuyến. Cấu trúc dựa trên đồ thị của LangGraph cung cấp một cách trực quan và rõ ràng để xác định các trạng thái và chuyển tiếp, khiến nó trở nên lý tưởng cho các quy trình làm việc phức tạp, nhiều bước với logic định tuyến phức tạp. Mặt khác, Google ADK thường tập trung vào việc xác định các khả năng riêng biệt (Công cụ) và dựa vào khả năng của khung để định tuyến các yêu cầu của người dùng đến trình xử lý công cụ thích hợp, điều này có thể đơn giản hơn cho các tác tử với một tập hợp các hành động rời rạc được xác định rõ ràng.

Việc thành thạo mẫu hình Định tuyến là điều cần thiết để xây dựng các tác tử có thể điều hướng một cách thông minh các kịch bản khác nhau và cung cấp các phản hồi hoặc hành động phù hợp dựa trên ngữ cảnh. Đó là một thành phần quan trọng trong việc tạo ra các ứng dụng tác tử linh hoạt và mạnh mẽ.

Tài liệu tham khảo

Tài liệu LangGraph: https://www.langchain.com/

Tài liệu Bộ công cụ phát triển tác tử của Google: https://google.github.io/adk-docs/