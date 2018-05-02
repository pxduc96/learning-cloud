## install from source
Các bước tiến hành build phần mềm từ source code. 
Ví dụ sau đây nói về build `nodejs` từ source code

### Step 1: Getting the source code from github
Giống như các dự án open-source khác, sources của Nodejs có thể được tìm thấy trên github: https://github.com/nodejs/node

![Imgur](https://i.imgur.com/46mbVvD.png)
	
Ở trên github, chúng ta có thể tải về các phiên bản khác nhau của dự án. Lựa chọn các phiên bản khác nhau bằng cách chọn tags trong branch

![Imgur](https://i.imgur.com/XV0bYn2.png)
	
Các lập trình viên tạo `branch` và `tags` để theo dõi các sự kiện quan trọng của dự án, ví dụ như khi bắt đầu làm việc với một tính năng mới hoặc khi đẩy một release.

Sau khi chọn tag

![Imgur](https://i.imgur.com/WUUswUp.png)
	
Bây giờ có thể tải file zip hoặc sử git để clone về máy

![Imgur](https://i.imgur.com/da9zsRp.png)
	
### Step 2: Understanding the Build System of the program
Khi build một phần mềm từ source code, chúng ta thường nói về `compiling the sources` nhưng biên dịch chỉ là một pha được yêu cầu phải thực hiện. Một build system là một bộ các công cụ và các bước thực hành được sử dụng để tự động hóa và chỉ dẫn các nhiệm vụ khác nhau để xây dựng nên một phần mềm hoàn chỉnh, thông qua một vài lệnh.

Các build system là khác nhau, tùy thuộc và dự án, ngôn ngữ lập trình mà có các yêu cầu khác nhau. Hoặc phụ thuộc vào người lập trình hay là nền tảng triển khai.

Nodejs sử dụng `GNU-style build system`. Đây là một lựa chọn phổ biến trong cộng đồng nguồn mở.

`GNU-style build system` sử dụng 2 công cụ: `configure` và `make`

- configure: là một script dùng để cấu hình hệ thống và các tính năng có sẵn để chắc chắn project có thể được build. Phần quan trọng của configure là tạo `Makefile`, file này chứa các chỉ dẫn để build.

- `Make` tool: là một công cụ dùng để đọc các chỉ dẫn trong makefile và thực hiện chúng để build

### Step 3: Thực hiện build
- thực thi file config

```sh
./configure --prefix=/opt/node
```

- build

```sh
make

sudo make install
```

Lưu ý:
- Đây là một trong số các cách có thể build software từ source code. Đây cũng là cách build phổ biến
- Trong các mã nguồn, hầu hết đều có hướng dẫn build. Vì vậy cần đọc hướng dẫn để build đúng.
