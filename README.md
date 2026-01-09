# XÂY DỰNG ỨNG DỤNG SHELL (TƯƠNG TỰ BASH)

## 1. GIỚI THIỆU CHUNG

### 1.1. Mục tiêu 
Xay dựng một chương trình shell đơn giản bằng ngôn ngữ C thực hiện một số chức năng

### 1.2. Các chức năng chính
Hệ thống shell được phát triển với các khả năng sau:

- Thực thi lệnh nội trú (built-in commands) và lệnh ngoại trú (external commands)
- Xử lý cơ chế đường ống (pipe) và chuyển hướng luồng dữ liệu (redirection)
- Hỗ trợ thực thi tiến trình nền (background process execution)
- Phân tích cú pháp các ký tự đặc biệt: dấu ngoặc đơn ('..'), ngoặc kép (".."), backtick(`..`) và wildcards (?*)

## 2. ĐÁNH GIÁ MỨC ĐỘ HOÀN THIỆN

Hệ thống đã đạt được các mức độ hoàn thiện như sau:

- **Thực thi lệnh**: Chạy thành công 1 số lệnh cơ bản như lệnh nội trú (cd, exit, help, ...) và lệnh ngoại trú (ls, cat, grep, ...)
- **Xử lý ký tự đặc biệt**: Phân tích cú pháp chính xác các toán tử pipe (|), chuyển hướng (>, >>, <) và wildcards (*, ?)
- **Quản lý tiến trình**: Cài đặt hoàn chỉnh cơ chế thực thi tiến trình nền sử dụng toán tử ampersand (&)

## 3. PHÂN CÔNG NHIỆM VỤ

Nhiệm vụ cụ thể của từng thành viên:

| Thành viên | Nhiệm vụ chính |
|------------|----------------|
| Nguyễn Huy Hoàng | Cài đặt lệnh ngoại trú và xử lý wildcards (?, *) |
| Nguyễn Minh Đức | Triển khai cơ chế pipe và redirection |
| Lương Trọng Hưởng | Phát triển tính năng thực thi tiến trình nền |
| Nguyễn Quang Tháng | Xử lý và phân tích cú pháp các loại dấu ngoặc |
| Trần Phú Ninh | Cài đặt và tối ưu hóa các lệnh nội trú |

## 4. HƯỚNG DẪN BIÊN DỊCH VÀ THỰC THI

### 4.1. Biên dịch chương trình
```bash
make
```

### 4.2. Khởi chạy ứng dụng
```bash
./test
```

## 5. LỆNH NỘI TRÚ (BUILT-IN COMMANDS)

Các lệnh nội trú được tích hợp trực tiếp vào shell:

- **pwd**: Hiển thị đường dẫn của thư mục làm việc hiện tại
- **cd**: Thay đổi thư mục làm việc (change directory)
- **echo**: Xuất chuỗi ký tự hoặc giá trị biến ra luồng đầu ra chuẩn
- **export**: Chuyển đổi biến shell thành biến môi trường toàn cục
- **unset**: Gỡ bỏ biến shell hoặc biến môi trường khỏi không gian tên hiện tại
- **jobs**: Liệt kê danh sách các tiến trình đang thực thi ở chế độ nền
- **set**: Cấu hình và quản lý các tùy chọn cũng như biến của shell
- **kill**: Gửi tín hiệu điều khiển (signal) đến tiến trình hoặc job để quản lý vòng đời

## 6. LỆNH NGOẠI TRÚ (EXTERNAL COMMANDS)

Các lệnh ngoại trú được thực thi thông qua việc tạo tiến trình con:

- **ls**: Liệt kê nội dung thư mục
- **date**: Hiển thị ngày tháng hệ thống hiện tại
- **time**: Hiển thị thời gian hệ thống hiện tại
- **whoami**: Trả về tên người dùng đang thực thi shell
- **sleep**: Tạm dừng tiến trình trong khoảng thời gian xác định (đơn vị: giây)
- **cat**: Đọc và xuất nội dung file ra đầu ra chuẩn, hỗ trợ nối nhiều file
- **wc**: Thống kê số dòng, số từ và số byte của file hoặc luồng đầu vào

## 7. CƠ CHẾ ĐƯỜNG ỐNG (PIPE)

### 7.1. Định nghĩa
Pipe là cơ chế Inter-Process Communication (IPC) cho phép kết nối luồng đầu ra chuẩn (stdout) của tiến trình nguồn với luồng đầu vào chuẩn (stdin) của tiến trình đích.

### 7.2. Cú pháp và ví dụ minh họa

```bash
# Đếm số lượng mục trong thư mục hiện tại
ls | wc -l

# Kết hợp wildcard với pipe để đếm file theo pattern
ls *.txt | wc -l

# Xử lý dữ liệu đầu ra trước khi lưu file
ls *.txt > list.txt
```

## 8. CƠ CHẾ CHUYỂN HƯỚNG (REDIRECTION)

### 8.1. Khái niệm
Redirection là kỹ thuật điều hướng luồng dữ liệu vào/ra của tiến trình, cho phép thay thế các file descriptor mặc định (stdin, stdout, stderr).

### 8.2. Các toán tử chuyển hướng

#### 8.2.1. Chuyển hướng đầu ra với ghi đè (>)
```bash
# Ghi đầu ra của lệnh vào file (truncate mode)
ls > output.txt
```

#### 8.2.2. Chuyển hướng đầu ra với ghi thêm (>>)
```bash
# Nối đầu ra vào cuối file (append mode)
ls >> output.txt
```

#### 8.2.3. Chuyển hướng đầu vào (<)
```bash
# Đọc đầu vào từ file
wc -l < input.txt
```

## 9. XỬ LÝ KÝ TỰ ĐẶC BIỆT

### 9.1. Dấu ngoặc đơn ('...')
**Chức năng**: Bảo toàn chuỗi ký tự nguyên gốc (literal string), vô hiệu hóa mọi phép thay thế và mở rộng.

```bash
echo '$HOME'
# Output: $HOME
```

### 9.2. Dấu ngoặc kép ("...")
**Chức năng**: Nhóm chuỗi ký tự với phép thay thế biến, nhưng vô hiệu hóa wildcard expansion.

```bash
echo "Xin chào $USER"
# Output: Xin chào [tên người dùng]
```

### 9.3. Dấu Backtick (`...`)
**Chức năng**: Thực thi lệnh bên trong và thay thế bằng kết quả trả về (command substitution).

```bash
echo `pwd`
# Output: /đường/dẫn/thư/mục/hiện/tại
```

### 9.4. Ký tự đại diện (Wildcards)

#### 9.4.1. Dấu sao (*)
Khớp với chuỗi ký tự có độ dài tùy ý (≥ 0 ký tự).

```bash
ls *.c
# Liệt kê tất cả file có phần mở rộng .c
```

#### 9.4.2. Dấu hỏi (?)
Khớp với đúng một ký tự bất kỳ.

```bash
ls test?.txt
# Khớp với: test1.txt, testA.txt, etc.
```