# Learning Linux

## Work on the command line

### 9. File-Viewing Commands: head, tail, less, cut, wc

head
- lệnh để xem các dòng từ trên xuống của file. mặc định sẽ hiện thị ra 10 dòng đầu của 1 file.
- Một số option:
	- `-n`: số dòng đầu trong file muốn hiện thị
	- `-q`: không hiện thị tên file ở output
	- `-v`: hiện thị tên file ở output
	

tail
- Hiện thị các dòng cuối của file. Có thể theo dõi thông tin mới được ghi vào file theo thời gian thực.
- Một số option:
	- `-n`: số dòng muốn hiện thị
	- `-q` và `-v` tương tự như head
	- `-f`: theo dõi các thông tin mới được ghi vào theo thời gian thực.
	

less
- Khi có output hiện thị trên màn hình, có thể output đấy có nhiều thông tin và hiện thị tràn ra ngoài màn hình. Như vậy chúng ta chỉ xem được các output cuối. Sử dụng `less` cho phép chúng ta xem lần lượt từ trên xuống nhằm có thể xem hết thông tin của output.
- Ví dụ xem nội dung file, có thể sử dụng less để đọc nội dung từ trên xuống.


cut
- cut là 1 tiện ích nhỏ giúp chúng ta cắt, trích xuất nội dung của tập tin theo cột. Nó cũng có thể chỉ ra dấu phân cách phân biệt các cột. Trong thuật ngữ của cut, các cột được gọi là các trường (field).

<đang update>

## Manage processes

### Processes

Mỗi chương trình, cho dù đó là một lệnh, ứng dụng hoặc tập lệnh (scripts) chạy trên hệ thống đều là process. Shell là một process, mỗi lệnh được thực thi từ shell được gọi là các process con. Các thuộc tính và khái niệm liên quan đến process bao gồm:
- lifetime: lifetime của process được định nghĩa là quãng thời gian mà process đó cần để thực thi.
- Process ID (PID): Mỗi process có một số được gán cho nó từ khi nó bắt đầu. PID là số nguyên duy nhất đại diện cho process
- User ID (UID) and Group ID (GID): Process phải có các quyền hạn kèm theo, và UID và GID của process được liên kết với user, người mà đã khởi tạo process. Các quyền này sẽ giới hạn quyền truy cập của process tới các object trong hệ thống.
- Parent process: Process đầu tiên được bắt đầu bởi kernel tại thời điểm mà start hệ thống là một chương trình được gọi là `init`. Process này có PID là 1 và là cha của tất cả các process khác trong hệ thống. Shell cũng là một process của init và là cha của các process được bắt đầu bởi shell, các process này được gọi là process hay subprocess.
- Parent process ID (PPID): đây là PID của process cha
- Environment: Mỗi process giữ một danh sách các biến và giá trị của biến. Đây là danh sách được biến như là `environment` của process, và các biến này được gọi là `environment variables`.
- Current working directory: Thư mục mặc định được liên kết với mỗi process. Process này sẽ đọc và ghi các file trong thư mục này trừ khi chúng được chỉ định ở nơi khác trong filesystem.

## 1. Process Monitoring

Monitoring các process sử dụng các công cụ: ps, top, htop

#### ps

Cú pháp:
	
	ps [option]
	
Chức năng: Lệnh này sẽ in ra màn hình các processes hiện tại
Các options hay được sử dụng:

`-a`: show tất các process

```sh
~# ps -a
   PID TTY          TIME CMD
  1936 tty1     00:00:00 bash
  2382 pts/2    00:00:00 vi
  2496 pts/3    00:00:00 tailf
  2534 pts/1    00:00:00 bash
  2642 tty2     00:00:00 bash
  2861 pts/4    00:00:00 tailf
  2862 pts/0    00:00:00 ps
```

`-f`: show đầy đủ định dạnh các processes của user hiện tại.

```sh
~# ps -f
UID         PID   PPID  C STIME TTY          TIME CMD
root       2088   2025  0 16:20 pts/0    00:00:00 -bash
root       2920   2088  0 17:36 pts/0    00:00:00 ps -f
```

`-x`: Bao gồm các process mà không cần kiểm soát terminal. Thường cần thiết để xem các daemon process.

```sh
~$ ps -x
   PID TTY      STAT   TIME COMMAND
  2222 ?        Ss     0:00 /lib/systemd/systemd --user
  2223 ?        S      0:00 (sd-pam)
  2259 ?        S      0:00 sshd: ducpx@pts/1
  2274 pts/1    Ss     0:00 -bash
  2300 ?        S      0:00 sshd: ducpx@notty
  2303 ?        Ss     0:00 /usr/lib/openssh/sftp-server
  2337 ?        S      0:00 sshd: ducpx@pts/2
  2352 pts/2    Ss     0:00 -bash
  2380 ?        S      0:00 sshd: ducpx@notty
  2381 ?        Ss     0:00 /usr/lib/openssh/sftp-server
  2382 pts/2    S+     0:00 vi df
  2534 pts/1    S      0:00 bash
  2907 tty3     S+     0:00 -bash
  3004 pts/1    R+     0:00 ps -x
```

#### top
Lệnh top dùng để xem những gì đang xảy ra trong hệ thống theo "real time". Top giúp chúng ta monitor hệ thống, cho biết tiến trình nào đang hoạt động và sử dụng tài nguyên. Xem một số thông tin của top.

Sử dụng command

```sh
$ top
```

- 1. dòng đầu


### 2. Foreground and Background Processes

- 1. Foreground processes

Foreground processes là các command hoặc các task được chạy trực tiếp và chờ cho đến khi nó hoàn. Ví dụ trong shell, khi bạn nhập lệnh `ls` để liệt kê các file và thư mục có trong thư mục hiện tại. Bạn phải chờ ls được hoàn thành rồi mới có thể thực hiện được các command tiếp theo.

- 2. Background processes

Không giống với foreground, shell không cần phải chờ một background process kết thúc để chạy command khác. Ta có thể chạy nhiều background processes.

Để chạy một background process, chỉ cần thêm một space và dấu & sau lệnh

```sh
$ command &
```

khi thực hiện lệnh ở background, terminal có thể nhận được các lệnh khác. Process chạy ở background có độ ưu tiên thấp hơn foreground.


### 3. Kill process
Có process nào đó làm treo hệ thống, hoặc sử dụng quá nhiều tài nguyên và ta có nhu cầu kết thúc process đó.

Để kết thúc process, ta cần biết tên hoặc id của process. Sử dụng ps hoặc top để xem id của process. Sau đó dùng `kill` để kết thúc.

```sh
$ kill id_process
```












































































