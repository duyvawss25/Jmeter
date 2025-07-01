# 🧾 BÁO CÁO KIỂM THỬ HIỆU SUẤT JMETER

- **Tên Dự Án**: Load Testing of `fakestoreapi.com/products`  
- **Ngày Kiểm Thử**: 01/07/2025  
- **Người Kiểm Thử**: Cao Văn Duy   

---

## 1. Mục Tiêu Kiểm Thử

Mục tiêu của đợt kiểm thử này là đánh giá hiệu năng và khả năng đáp ứng của một dịch vụ API công khai tại địa chỉ `https://fakestoreapi.com/products`. API này trả về danh sách các sản phẩm dạng JSON, thường được sử dụng trong các bài kiểm thử giả lập thương mại điện tử.  
Kiểm thử được thực hiện bằng công cụ Apache JMeter để mô phỏng nhiều người dùng truy cập đồng thời và gửi request đến API. Mục tiêu là đảm bảo API hoạt động ổn định trong cả điều kiện tải thấp và tải cao, không xảy ra lỗi và thời gian phản hồi nằm trong giới hạn chấp nhận được.

---

## 2. Môi Trường Kiểm Thử

Quá trình kiểm thử được thực hiện trên môi trường đơn giản nhưng đảm bảo yêu cầu kỹ thuật:
- Công cụ kiểm thử: **Apache JMeter phiên bản 5.6.3**
- Hệ điều hành: **Windows 10 Pro x64**
- Kết nối mạng ổn định, không bị giới hạn firewall khi truy cập API công khai
- Không có proxy hoặc cache nào can thiệp vào quá trình gửi nhận request
- Không sử dụng hệ thống backend riêng mà chỉ kết nối đến dịch vụ API công cộng `fakestoreapi.com`

---

## 3. Phương Pháp Kiểm Thử

Phương pháp kiểm thử được sử dụng trong đợt này là **kiểm thử hiệu suất tự động**, tập trung vào việc:
- Gửi các request đồng thời từ nhiều người dùng ảo (thread)
- Lặp lại các request để kiểm tra độ ổn định theo thời gian
- Theo dõi thời gian phản hồi, tỉ lệ thành công, và khả năng xử lý khi có tải tăng
- Phân tích các số liệu thống kê như throughput, latency, success rate...

JMeter được sử dụng để cấu hình chi tiết số lượng người dùng, thời gian ramp-up, vòng lặp, và các loại listener như Summary Report, Graph Results, View Results Tree để theo dõi kết quả trong thời gian thực.

---

## 4. Kịch Bản Kiểm Thử

---

### 🧪 Kịch Bản Kiểm Thử Lần 1

- **Tên kịch bản**: Kiểm thử cơ bản với 1 người dùng
- **Mục đích**: Mục đích của kịch bản này là kiểm tra phản hồi cơ bản của API khi có duy nhất một người dùng gửi một yêu cầu đơn lẻ. Đây là trường hợp đơn giản nhất nhằm xác nhận rằng API đang hoạt động, có thể kết nối được, và trả về dữ liệu đúng như kỳ vọng.

| Thông số cấu hình         | Giá trị                                  |
|---------------------------|-------------------------------------------|
| HTTP Request              | `https://fakestoreapi.com/products`      |
| Method                    | `GET`                                    |
| Number of Threads (User)  | `1`                                      |
| Ramp-up Period (s)        | `1`                                      |
| Loop Count                | `1`                                      |

- **Kết quả:
![image](https://github.com/user-attachments/assets/be5ecdcd-c904-4fe5-9a15-4ce57f091bfc)
![image](https://github.com/user-attachments/assets/4c18be20-b583-4b55-b46f-4a6a24c7b49f)
![image](https://github.com/user-attachments/assets/619bd167-afb4-48ad-ac52-be3ac1774e94)


---

### 🧪 Kịch Bản Kiểm Thử Lần 2

- **Tên kịch bản**: Kiểm thử với nhiều người dùng đồng thời
- **Mục đích**: Kịch bản này nhằm mô phỏng tình huống có nhiều người dùng cùng truy cập API trong một khoảng thời gian ngắn. Việc này giúp kiểm tra xem hệ thống có thể đáp ứng được nhiều yêu cầu đồng thời hay không, có xảy ra tình trạng nghẽn hoặc lỗi phản hồi hay không.

| Thông số cấu hình         | Giá trị                                  |
|---------------------------|-------------------------------------------|
| HTTP Request              | `https://fakestoreapi.com/products`      |
| Method                    | `GET`                                    |
| Number of Threads (User)  | `10`                                     |
| Ramp-up Period (s)        | `5`                                      |
| Loop Count                | `5`                                      |

- **Kết quả:
![image](https://github.com/user-attachments/assets/62f4798c-21d7-4976-b0a0-d6b875de8002)
![image](https://github.com/user-attachments/assets/8a48bc01-eb93-403b-ac14-89e6f49cfcc1)
![image](https://github.com/user-attachments/assets/07497621-29a9-4266-a32a-ae0cea3f5504)
---

## 5. Kết Luận

Qua hai kịch bản kiểm thử trên, có thể nhận thấy rằng API công khai `https://fakestoreapi.com/products` hoạt động ổn định và có hiệu năng tốt trong điều kiện sử dụng thông thường cũng như khi phải xử lý nhiều người dùng cùng truy cập.  
Tất cả các request đều được xử lý đúng, không có lỗi xảy ra và thời gian phản hồi ở mức rất khả quan. Với kết quả đó, API hoàn toàn phù hợp để dùng làm dịch vụ giả lập trong môi trường kiểm thử hoặc giảng dạy kỹ thuật kiểm thử hiệu suất bằng JMeter.
