# XÂY DỰNG ỨNG DỤNG SHELL (TƯƠNG TỰ BASH)
## 1. Giới thiệu chung và chức năng
- Mục tiêu: Xây dựng một chương trình shell đơn giản bằng ngôn ngữ C.
- Các chức năng chính:
    + Thực thi một số lệnh nội trú và ngoại trú
    + Xử lý pipe (|) và redirection (>)
    + Cho phép chạy lệnh nền bằng &
    + Xử lý ngoặc '..', "..", `..`, ... và wildcards(?*)

## 2. Đánh giá mức độ hoàn thiện
- Thực hiện tốt các một số lệnh cơ bản: lệnh nội trú (cd, exit, help...) và lệnh ngoại trú (ls, cat, grep...)
- Xử lý đúng các ký tự đặc biệt: Pipe (|), chuyển hướng (>, >>, <) và Wildcards (*, ?)
- Đã xử lý chạy tiến trình nền (&)
## 3. Phân công nhiệm vụ:
- Nguyễn Huy Hoàng: cho phép cài đặt lệnh ngoại trú và xử lý wildcards (?*) 
- Nguyễn Minh Đức: Xử lý pipe và redirection
- Lương Trọng Hưởng: Cho phép chạy lệnh nền bằng &
- Nguyễn Quang Tháng: Xử lý các dấu ngoặc
- Trần Phú Ninh: Cho phép cài đặt và thực thi một số lệnh nội trú

## 4. Hướng dẫn cài đặt, dịch và sử dụng:
### Compile:
```bash
make
```
### Run:
```bash
run
```

## 5. Các lệnh nội trú
- pwd: folder đang ở hiện tại
- cd: chuyển sang folder khác
- echo: dùng để in (hiển thị) một chuỗi ký tự hoặc giá trị ra màn hình
- export: dùng để đưa biến shell thành biến môi trường
- unset: dùng để xóa biến (biến shell hoặc biến môi trường) ra khỏi shell hiện tại
- jobs: dùng để liệt kê các tiến trình đang chạy nền (background jobs) trong shell hiện tại
- set: để thiết lập, hiển thị hoặc thay đổi trạng thái và biến của shell
- kill: dùng để gửi tín hiệu (signal) tới process hoặc job để điều khiển hoặc kết thúc nó

## 6. Các lệnh ngoại trú 
- ls: liệt kê folder
- ate: in ra ngày tháng năm hiện tại
- time: in ra giờ hiện tại
- whoami: dùng để hiển thị tên người dùng (username) hiện đang đăng nhập và đang chạy shell
- sleep: dùng để tạm dừng (ngủ) tiến trình trong một khoảng thời gian xác định, sau đó tiếp tục hoặc kết thúc
- cat: dùng để hiển thị nội dung file ra màn hình, hoặc nối nhiều file lại với nhau
- wc: dùng để đếm số dòng, số từ và số ký tự (byte) của file hoặc dữ liệu đầu vào

## 7. Pipe
Pipe là cơ chế nối đầu ra của lệnh này vào đầu vào của lệnh khác


Cách dùng 

 ```bash
ls | wc -l :  Đếm số dòng trong output của ls → thường được hiểu là đếm số file/thư mục trong thư mục hiện tại.

ls *.txt > list.txt: Liệt kê tất cả các file có đuôi .txt trong thư mục hiện tại và ghi danh sách đó vào file list.txt (ghi đè nội dung cũ nếu có).

ls *.txt | wc -l: Đếm số lượng file có đuôi .txt trong thư mục hiện tại.
```

## 8. Redirection
Redirection (chuyển hướng) trong shell là cơ chế điều hướng luồng vào/ra của chương trình, thay vì dùng bàn phím và màn hình mặc định.

1. Chuyển hướng output >
```bash
ls > out.txt: chuyển (redirect) toàn bộ kết quả của lệnh ls vào file out.txt
```

2. Ghi thêm >>

```bash
ls >> out.txt: Ghi toàn bộ kết quả của lệnh ls vào cuối file
 
```

## 9. Dấu ngoặc và wildcards
1. Dấu ngoặc đơn ('...')
Dùng để bảo toàn nguyên vẹn chuỗi ký tự (Literal String). Shell sẽ không xử lý biến hay ký tự đặc biệt bên trong.
```Bash

echo '$HOME'
```
2. Dấu ngoặc kép ("...")
Dùng để nhóm chuỗi ký tự. Shell cho phép thay thế biến ($) nhưng bỏ qua các ký tự đại diện (*, ?).
```Bash
echo "Xin chao $NAME"
```
3. Dấu Backtick (`...`)
Dùng để thực thi lệnh bên trong và lấy kết quả trả về (Command Substitution).
```Bash
echo `pwd`
```
4. Wildcards (Ký tự đại diện)
Dùng để so khớp tên file/thư mục tự động.
Dấu sao (*): Khớp với một chuỗi ký tự bất kỳ (độ dài >= 0).
```Bash
ls *.c
```
Dấu hỏi chấm (?): Khớp với đúng một ký tự bất kỳ.
```Bash
ls test?.txt
```