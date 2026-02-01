# 🗣️ Talki - AI English Communication Coach (Agent-Based)

> **Dự án khởi nghiệp / EXE**
> _Nền tảng cải thiện độ tự tin, nhạy bén trong giao tiếp với AI Mentor chuyên sâu, tập trung vào phỏng vấn và giao tiếp thực tế._

## 📖 1. Tổng quan dự án (Project Overview)

**Talki** không phải là một ứng dụng "Chat với Bot" thông thường. Chúng tôi xây dựng một **AI Agent (Tác nhân AI)** đóng vai trò là một Mentor (người hướng dẫn) nghiêm khắc và thông minh.

Khác với các app hiện có, Talki sử dụng kiến trúc **RAG (Retrieval-Augmented Generation)** để AI có "ký ức" và kiến thức nghiệp vụ, giúp user luyện tập theo lộ trình cá nhân hóa chứ không chỉ hỏi đáp vu vơ.

### 🎯 Mục tiêu chính:

- **Mock Interview:** Giả lập phỏng vấn xin việc (IT, Business...) với bộ câu hỏi sát thực tế.
- **Strict Mentor Mode:** AI sẽ soi lỗi ngữ pháp, cách dùng từ ngay sau mỗi cuộc trò chuyện.
- **Personalized Learning:** Hệ thống ghi nhớ các lỗi sai cũ của người dùng để hỗ trợ khác phục.

---

## 🏗️ 2. Kiến trúc hệ thống (System Architecture)

Backend dùng **Python (FastAPI)** để tận dụng tối đa sức mạnh của hệ sinh thái AI/Data.

### 🛠️ Tech Stack

| Thành phần       | Công nghệ                   | Lý do lựa chọn                                                                        |
| :--------------- | :-------------------------- | :------------------------------------------------------------------------------------ |
| **Frontend**     | **ReactJS** (Vite)          | SPA nhanh, trải nghiệm mượt, component-based dễ tái sử dụng.                          |
| **Backend**      | **Python FastAPI**          | Hiệu năng cao (Async), hỗ trợ cực tốt cho thư viện AI, triển khai nhanh.              |
| **AI Core**      | **Google Gemini 1.5 Flash** | Model LLM mới nhất của Google, tốc độ phản hồi cực nhanh, chi phí tối ưu (Free tier). |
| **AI Framework** | **LangChain**               | Quản lý luồng hội thoại, tạo "Agent" có khả năng tư duy và dùng tool.                 |
| **Database**     | **PostgreSQL**              | Lưu trữ User, History, Progress (Relational Data).                                    |
| **Vector DB**    | **ChromaDB / FAISS**        | Lưu trữ kiến thức RAG (Ví dụ: Ngân hàng câu hỏi phỏng vấn, từ vựng) dưới dạng vector. |

### 🧩 Luồng xử lý (Data Flow)

```mermaid
graph TD
    User[User (ReactJS)] -->|Voice/Text| API[FastAPI Gateway]
    API --> Agent[AI Agent Controller]

    subgraph "AI Brain (Backend Logic)"
        Agent -->|1. Retrieve Context| VectorDB[(ChromaDB - RAG)]
        Agent -->|2. Check History| PG[(PostgreSQL)]
        Agent -->|3. Construct Prompt| LLM[Google Gemini API]
    end

    LLM -->|4. Answer/Feedback| Agent
    Agent -->|5. Save Progress| PG
    Agent -->|JSON Response| User
```
