[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=24112746&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Name:** Nguyen Doan Gia Tuan  
**Student ID:** AI20K-2A202600669  
**Student Email:** 26ai.tuanndg@vinuni.edu.vn  

---

## Mo ta

Bài lab này yêu cầu xây dựng một đường ống dẫn dữ liệu (ETL Pipeline) cơ bản bằng Python và Pandas để xử lý dữ liệu thô dạng JSON (`raw_data.json`).
Các nhiệm vụ chính đã hoàn thành:
1. **Extract:** Đọc dữ liệu JSON từ nguồn, xử lý ngoại lệ file không tồn tại.
2. **Validate:** Lọc bỏ các bản ghi không hợp lệ
3. **Transform:** Sử dụng thư viện Pandas để tính giá giảm 10%, chuẩn hóa trường `category` về dạng Title Case, và thêm cột thời gian xử lý.
4. **Load:** Xuất dữ liệu sang tệp tin csv
5. **Stress Test & Observability:** Test tầm quan trọng của việc kiểm soát chất lượng dữ liệu đầu vào lên phản hồi của Agent

---

## Cach chay (How to Run)

### Prerequisites


```bash
pip install pandas pytest
```

### Chay ETL Pipeline


```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)

1. Tạo dữ liệu rác:
   ```bash
   python generate_garbage.py
   ```
2. Chạy chương trình giả lập phản hồi:
   ```bash
   python agent_simulation.py
   ```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── generate_garbage.py      # Script tao du lieu rac
├── agent_simulation.py      # Script test phan hoi cua Agent
├── experiment_report.md     # Bao cao thi nghiem stress test
└── README.md                # File nay
```

---

## Ket qua

1. **ETL Pipeline:** 
   - Tổng số bản ghi thô: 5 bản ghi.
   - Số bản ghi hợp lệ: 3 bản ghi (Laptop, Chair, Monitor).
   - Số bản ghi bị loại bỏ do không hợp lệ: 2 bản ghi (Mystery Box vì price <= 0 và Phone vì category trống).
   - Kết quả xuất ra thành công trong file `processed_data.csv`.

2. **Phản hồi của Agent:**
   - **Với Clean Data:** Agent đề xuất chính xác sản phẩm `Laptop` với giá `$1200`. (Độ chính xác: 10/10)
   - **Với Garbage Data:** Do không có pipeline ETL lọc rác, Agent đề xuất nhầm thiết bị cực đoan `Nuclear Reactor` với giá `$999999` làm ảnh hưởng lớn đến kết quả. (Độ chính xác: 2/10)
