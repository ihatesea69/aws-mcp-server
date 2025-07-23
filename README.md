# AWS MCP: Model Context Protocol trên AWS

![AWS Logo](https://www.telecomreview.com/images/stories/2023/09/Amazon_and_Anthropic.jpg)

<a href="https://glama.ai/mcp/servers/@ihatesea69/AWS-MCP">
  <img width="380" height="200" src="https://glama.ai/mcp/servers/@ihatesea69/AWS-MCP/badge" alt="AWS Server MCP server" />
</a>

## Giới thiệu về Model Context Protocol (MCP)
### Bắt đầu với MCP

MCP (Model Context Protocol) là một giao thức mở chuẩn hóa cách các ứng dụng cung cấp ngữ cảnh cho các mô hình ngôn ngữ lớn (LLMs). Hãy tưởng tượng MCP giống như một cổng USB-C cho các ứng dụng AI. Cũng như USB-C cung cấp một phương thức chuẩn để kết nối thiết bị với các phụ kiện khác nhau, MCP cung cấp một phương thức chuẩn để kết nối mô hình AI với các nguồn dữ liệu và công cụ khác nhau.

### Tại sao nên sử dụng MCP?
MCP giúp xây dựng các agent và quy trình tự động phức tạp dựa trên LLMs. Các mô hình LLM thường cần tích hợp với dữ liệu và công cụ, và MCP cung cấp:
- **Danh sách ngày càng tăng các tích hợp sẵn có** giúp LLM của bạn kết nối trực tiếp.
- **Khả năng linh hoạt** để chuyển đổi giữa các nhà cung cấp LLM.
- **Các phương pháp bảo mật dữ liệu tốt nhất** trong hạ tầng của bạn.

### Kiến trúc tổng quát
Ở mức cơ bản, MCP tuân theo kiến trúc client-server, nơi một ứng dụng chủ có thể kết nối với nhiều máy chủ khác nhau:

![AWS Logo](https://quickstartgenai.com/_next/image?url=https%3A%2F%2Fcdn.sanity.io%2Fimages%2Ft2bsu7sk%2Fproduction%2Fd0d1f7922931519f74e92737ae860809d8a45784-563x384.png&w=1920&q=75)

- **MCP Hosts**: Các chương trình như Claude Desktop, IDEs hoặc công cụ AI muốn truy cập dữ liệu thông qua MCP.
- **MCP Clients**: Các client giao thức duy trì kết nối 1:1 với server.
- **MCP Servers**: Các chương trình nhẹ, mỗi chương trình cung cấp các khả năng cụ thể thông qua Model Context Protocol.
- **Local Data Sources**: Các tệp, cơ sở dữ liệu và dịch vụ trên máy tính của bạn mà MCP server có thể truy cập an toàn.
- **Remote Services**: Các hệ thống bên ngoài có sẵn trên Internet (ví dụ: thông qua API) mà MCP server có thể kết nối.

---

## Giới thiệu về AWS MCP
AWS MCP (Model Context Protocol) là một máy chủ cho phép các trợ lý AI như Claude tương tác với môi trường AWS thông qua ngôn ngữ tự nhiên. Điều này giúp bạn dễ dàng quản lý và truy vấn tài nguyên AWS mà không cần phải sử dụng AWS Console hoặc CLI truyền thống.

AWS MCP có thể được coi là một giải pháp thay thế mạnh mẽ cho Amazon Q, mang lại sự linh hoạt và bảo mật cao hơn.

## Tính năng chính của AWS MCP
-  **Truy vấn và chỉnh sửa tài nguyên AWS bằng ngôn ngữ tự nhiên**
-  **Hỗ trợ nhiều hồ sơ AWS và xác thực SSO**
- **Hỗ trợ đa vùng AWS**
- **Quản lý thông tin xác thực an toàn** (Không tiết lộ thông tin xác thực ra bên ngoài, chỉ sử dụng thông tin cục bộ)
- **Thực thi cục bộ với thông tin đăng nhập AWS của bạn**

## Yêu cầu trước khi cài đặt
Để sử dụng AWS MCP, bạn cần đảm bảo môi trường của bạn có:
- **Node.js**
- **Ứng dụng Claude Desktop**
- **Thông tin xác thực AWS được cấu hình cục bộ (AWS Configure)** (lưu trong thư mục `~/.aws/`)

## Hướng dẫn cài đặt AWS MCP
### 1. Clone repository
Trước tiên, bạn cần tải mã nguồn từ GitHub về máy tính của mình:
```bash
git clone https://github.com/ihatesea69/AWS-MCP
cd aws-mcp
```

### 2. Cài đặt dependencies
Bạn có thể sử dụng `pnpm` hoặc `npm` để cài đặt:
```bash
pnpm install
# hoặc
npm install
```

## Cấu hình và sử dụng AWS MCP với Claude Desktop
### 1. Cấu hình trong Claude Desktop
Mở ứng dụng Claude Desktop, đi tới:
```
Settings -> Developer -> Edit Config
```

Sau đó, thêm mục sau vào tệp `claude_desktop_config.json`:
```json
{
  "mcpServers": {
    "aws": {
      "command": "npm", // hoặc pnpm
      "args": [
        "--silent",
        "--prefix",
        "/Users/<YOUR USERNAME>/aws-mcp",
        "start"
      ]
    }
  }
}
```
> Lưu ý: Thay thế `/Users/<YOUR USERNAME>/aws-mcp` bằng đường dẫn thực tế tới thư mục dự án của bạn.

### 2. Khởi động lại Claude Desktop
Chạy dự án của bạn bằng điều hướng (cd) tới thư mục chứa index.ts và chạy lệnh NPM start 

Sau khi chỉnh sửa cấu hình, hãy khởi động lại ứng dụng Claude Desktop. Nếu quá trình cài đặt đúng, bạn sẽ thấy thông báo kết nối thành công với MCP.

### 3. Sử dụng AWS MCP trong Claude
Bạn có thể bắt đầu sử dụng bằng cách nhập các câu lệnh tự nhiên như:
- "List available AWS profiles"
- "List all EC2 instances in my account"
- "Show me S3 buckets with their sizes"
- "What Lambda functions are deployed in us-east-1?"
- "List all ECS clusters and their services"

## Cấu hình MCP với `nvm`
Nếu bạn sử dụng Node.js thông qua `nvm`, hãy biên dịch từ mã nguồn trước và thêm cấu hình sau:
```json
{
  "mcpServers": {
    "aws": {
      "command": "/Users/<USERNAME>/.nvm/versions/node/v20.10.0/bin/node",
      "args": [
        "<WORKSPACE_PATH>/aws-mcp/node_modules/tsx/dist/cli.mjs",
        "<WORKSPACE_PATH>/aws-mcp/index.ts",
        "--prefix",
        "<WORKSPACE_PATH>/aws-mcp",
        "start"
      ]
    }
  }
}
```
> Lưu ý: Thay thế `<USERNAME>` và `<WORKSPACE_PATH>` bằng đường dẫn thực tế trên hệ thống của bạn.

## Kết luận
AWS MCP là một công cụ mạnh mẽ cho phép bạn quản lý tài nguyên AWS bằng cách sử dụng trợ lý AI Claude. Với khả năng truy vấn và điều khiển thông qua ngôn ngữ tự nhiên, AWS MCP giúp đơn giản hóa việc quản lý AWS một cách đáng kể. Nếu bạn đang tìm kiếm một giải pháp thay thế cho Amazon Q, AWS MCP là một lựa chọn đáng cân nhắc!

Nguon - Credit : https://github.com/RafalWilinski/aws-mcp