# Text2SQL Agent

Agent chuyển đổi truy vấn ngôn ngữ tự nhiên thành SQL, sử dụng:
- **SQLite** làm cơ sở dữ liệu.
- **phidata** để xây dựng agent.
- **Groq API** để thực thi mô hình ngôn ngữ.

Dự án có kèm ví dụ giao diện bằng Streamlit để nhập câu hỏi và nhận kết quả trực tiếp.

---

## 🚀 Tổng quan

Text2SQL Agent cho phép người dùng nhập truy vấn bằng ngôn ngữ tự nhiên (tiếng Anh), sau đó:
1. Agent (dựa trên **phidata**) gọi **Groq API** để phân tích và sinh câu SQL.
2. SQL được thực thi trên **SQLite database** đã khởi tạo sẵn từ dữ liệu mẫu.
3. Kết quả được trả về cho người dùng qua terminal hoặc giao diện Streamlit.

---

## 📦 Cài đặt

1. Clone repo:
   ```bash
   git clone https://github.com/NghiaAi/Text2SQl_Agent.git
   ```

2. Tạo môi trường ảo và cài các dependencies:
   ```bash
   python -m venv venv
   source venv/bin/activate   # Mac/Linux
   venv\Scripts\activate      # Windows

   pip install -r requirements.txt
   ```


3. Thiết lập API key cho **Groq**:
   ```bash
   export GROQ_API_KEY=your_api_key_here   # Mac/Linux
   set GROQ_API_KEY=your_api_key_here      # Windows
   ```

---

## 🗄️ Khởi tạo cơ sở dữ liệu

Dữ liệu mẫu gồm:
- **djia_companies_20250426.csv**
- **djia_prices_20250426.csv**

Chạy script:
```bash
python create_db.py
```

Script sẽ tạo file **SQLite database** (ví dụ: `djia.db`) trong thư mục `db/`.

---

## 🤖 Chạy agent

Agent chính nằm trong file **agent.py**.

Chạy thử:
```bash
streamlit run djia_streamlit.py
```

Sau đó mở trình duyệt tại [http://localhost:8501](http://localhost:8501).
Ví dụ:
```
Input: What was the closing price of Merck on October 10, 2024?
Output: The closing price of Merck on October 10, 2024, was $107.60.
      SELECT Close FROM prices WHERE Ticker = "MRK" AND DATE(Date) = "2024-10-10"
```


## 📂 Cấu trúc dự án

```
Text2SQl_Agent/
├── agent.py                # Agent chính (phidata + Groq API)
├── create_db.py            # Script khởi tạo SQLite DB từ CSV
├── djia_streamlit.py       # Demo giao diện với Streamlit
├── db/
│   ├── djia.db
│── djia_prices_20250426.csv
|── djia_companies_20250426
└── README.md               # Tài liệu
```


## 💡 Hướng phát triển

- Hỗ trợ nhiều cơ sở dữ liệu ngoài SQLite (PostgreSQL, MySQL…).
- Mở rộng xử lý đa ngôn ngữ.
- Bổ sung kiểm soát truy vấn SQL để tránh lỗi hoặc lạm dụng.
- Thêm visualization (biểu đồ) trực tiếp trong Streamlit.

---

## 📜 Bản quyền

MIT License — tự do sử dụng, chỉnh sửa và phân phối.
