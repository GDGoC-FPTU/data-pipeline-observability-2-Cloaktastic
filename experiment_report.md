# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-2A202600669   
**Name:** Nguyen Doan Gia Tuan   
**Date:** 10/6/2026  

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 10 | Du lieu da qua validation & transformation, gia tri hop le va category duoc chuan hoa. |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 2 | Dai ly khong loc bo thong tin "rac", dan den viec de xuat mot thiet bi lam outlier cuc doan (Nuclear Reactor). |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Khi sử dụng dữ liệu rác (Garbage Data) chưa qua xử lý, tác nhân AI (Agent) đưa ra kết quả không chính xác vì các lý do sau:

1. **Dữ liệu ngoại lai cực đoan (Outliers):** Bản ghi 'Nuclear Reactor' có giá trị $999,999 là một outlier quá lớn so với các sản phẩm điện tử tiêu dùng thông thường. Thuật toán tìm sản phẩm điện tử có giá lớn nhất sẽ lập tức trả về giá trị này mà không có sự kiểm duyệt ngữ cảnh hay sàng lọc ngưỡng hợp lý.
2. **Sai kiểu dữ liệu (Wrong data types):** Bản ghi 'Broken Chair' có giá trị là chuỗi ký tự ('ten dollars') thay vì số thực/số nguyên. Điều này khiến cột giá trong DataFrame bị nhận diện là kiểu Object (string), dẫn đến việc so sánh và sắp xếp số liệu bị sai lệch hoặc có thể gây crash hệ thống khi xử lý quy mô lớn.
3. **Giá trị trống/thiếu (Null values):** Việc thiếu thông tin 'id' hay 'category' (như bản ghi Ghost Item) sẽ làm gãy các bước lọc dữ liệu theo nhóm.
4. **Trùng lặp mã định danh (Duplicate IDs):** Trùng lặp ID (như ID 1 cho cả Laptop và Banana) vi phạm tính toàn vẹn dữ liệu (data integrity), khiến Agent bị nhầm lẫn khi tìm kiếm thông tin theo khóa chính.

Như vậy, việc thiếu đi một pipeline ETL chuẩn chỉnh để lọc nhiễu đã trực tiếp làm "nhiễm độc" cơ sở tri thức của AI Agent.

---

## 3. Ket luan

**Quality Data > Quality Prompt?**

Tôi hoàn toàn đồng ý với nhận định này. Dù prompt có được tối ưu hóa tốt đến đâu đi nữa thì theo nguyên lý "Garbage In, Garbage Out", AI Agent vẫn sẽ đưa ra các kết quả sai lệch nếu dữ liệu đầu vào không sạch. Một prompt chất lượng không thể sửa chữa cấu trúc dữ liệu bị hỏng, các giá trị null hay các outlier cực đoan. Vì vậy, xây dựng một đường ống dẫn dữ liệu (ETL) sạch và quan sát được (observable) luôn là điều kiện tiên quyết và quan trọng hơn cả việc thiết kế prompt.
