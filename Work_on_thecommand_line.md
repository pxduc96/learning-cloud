## Ngày 2 - 5

### 8 tac
- `Tac` được dùng để in các dòng trong file theo thứ tự.

ví dụ file có nội dung

```sh
This is number one
This is number two
This is number three
This is number four
This is number five
This is number six
This is number seven
This is number one
```

- dùng tac để in các dòng theo thứ tự bảng chữ 

```sh
~$ tac tac.txt 
This is number one
This is number seven
This is number six
This is number five
This is number four
This is number three
This is number two
This is number one
```

Ta có thể sử dụng `tac` kết hợp với less để đọc các file log bắt đầu từ cuối file thay cho `tail`

- Sort được dùng để sắp xếp các dòng theo thứ tự alpha
file có nội dung như sau:

```sh
computer
mouse
LAPTOP
data
RedHat
laptop
debian
laptop
```

Kết quả khi sử dụng sort

```sh
~$ sort tecmint.txt 
computer
data
debian
laptop
laptop
LAPTOP
mouse
RedHat
```

các dòng được sắp xếp theo thứ tự bảng chữ cái. kết quả này chỉ hiện thị lên màn hình mà không làm thay đổi nội dung file. ta có thể lưu lại kết quả này vào một file khác.

```sh
~# sort tecmint.txt > sorted.txt
```

Để in theo thứ tự ngược lại, sử dụng option `-r`

```sh
~$ sort -r tecmint.txt 
RedHat
mouse
LAPTOP
laptop
laptop
debian
data
computer
```

Có thể sắp xếp theo cột, tính năng này có thể được sử dụng để list các file theo dung lượng. Ví dụ sắp xếp theo cột thứ 5

```sh
ll | sort -nk5
total 28
drwxr-xr-x.  2 root root     6 Mar  7 20:27 binfmt.d
drwxr-xr-x.  2 root root     6 Mar  7 20:27 modules-load.d
dr-xr-xr-x.  2 root root     6 Nov  5  2016 games
dr-xr-xr-x.  2 root root     6 Nov  5  2016 sse2
drwxr-xr-x.  3 root root    21 Oct 21  2017 grub
drwxr-xr-x.  3 root root    23 Mar  7 20:27 kernel
lrwxrwxrwx.  1 root root    24 Apr 24 20:15 sendmail.postfix -> ../sbin/sendmail.postfix
drwxr-xr-x.  3 root root    27 Apr 24 20:14 python2.7
lrwxrwxrwx.  1 root root    30 Apr 24 20:15 sendmail -> /etc/alternatives/mta-sendmail
drwxr-xr-x.  4 root root    31 Oct 20  2017 NetworkManager
drwxr-xr-x.  2 root root    50 Apr 24 20:15 polkit-1
drwxr-xr-x.  2 root root    55 Apr 24 14:42 locale
drwxr-xr-x.  2 root root    55 Jan 25 23:01 modprobe.d
drwxr-xr-x.  2 root root    56 Apr 24 14:43 kdump
drwxr-xr-x.  3 root root    64 Nov  5  2016 debug
drwxr-xr-x.  4 root root    69 Apr 24 14:43 modules
drwxr-xr-x.  6 root root    76 Apr 24 20:15 kbd
drwxr-xr-x.  2 root root    80 Jan 30 20:51 yum-plugins
drwxr-xr-x.  2 root root    85 Apr 24 14:43 sysctl.d
drwxr-xr-x.  8 root root    98 Apr 24 20:14 firewalld
drwxr-xr-x.  4 root root   236 Apr 24 14:43 dracut
drwxr-xr-x. 11 root root   240 Apr 24 14:43 tuned
drwxr-xr-x.  4 root root   252 Apr 24 14:43 udev
drwxr-xr-x. 12 root root  4096 Apr 24 14:43 systemd
drwxr-xr-x.  2 root root  4096 May  2 08:57 tmpfiles.d
drwxr-xr-x.  4 root root  4096 Mar  7 22:03 rpm
drwxr-xr-x. 78 root root 12288 Apr 24 14:43 firmware
```

- `split` dùng để cắt file thành các file nhỏ hơn
split cắt file gốc thành các file nhỏ với mỗi file 1000 dòng (mặc định). Ta có thể chỉ định số dòng bằng option `-l`

```sh
~# split myfile
~# wc -l *
  223844 
    1000 xaa
    1000 xab
    1000 xac
    1000 xad
    1000 xae
    1000 xaf
    1000 xag
    1000 xah
    ....
```

cắt các file theo dung lượng. cắt file thành các file nhỏ 5M

```sh
~# split -b 5M myfile
~$ ls -lh | sort -nk5
total 57M
-rw-------. 1 root root 1,5K Apr 24 20:18 anaconda-ks.cfg
-rw-r--r--. 1 root root 3,5M May  2 11:47 xaf
-rw-r--r--. 1 root root 5,0M May  2 11:47 xaa
-rw-r--r--. 1 root root 5,0M May  2 11:47 xab
-rw-r--r--. 1 root root 5,0M May  2 11:47 xac
-rw-r--r--. 1 root root 5,0M May  2 11:47 xad
-rw-r--r--. 1 root root 5,0M May  2 11:47 xae
-rw-r--r--. 1 root root  29M May  2 11:33 myfile
```

các file con sẽ có cùng tiền tố

```sh
~# split -b 5M myfile myfile_
~$ ll
total 58228
-rw-------. 1 root root     1533 Apr 24 20:18 anaconda-ks.cfg
-rw-r--r--. 1 root root 29809292 May  2 11:33 myfile
-rw-r--r--. 1 root root  5242880 May  2 11:52 myfile_aa
-rw-r--r--. 1 root root  5242880 May  2 11:52 myfile_ab
-rw-r--r--. 1 root root  5242880 May  2 11:52 myfile_ac
-rw-r--r--. 1 root root  5242880 May  2 11:52 myfile_ad
-rw-r--r--. 1 root root  5242880 May  2 11:52 myfile_ae
-rw-r--r--. 1 root root  3594892 May  2 11:52 myfile_af
```

có thể thay thế tên các file con bằng số thay vì bằng chữ cái

```sh
ll
total 58228
-rw-------. 1 root root     1533 Apr 24 20:18 anaconda-ks.cfg
-rw-r--r--. 1 root root 29809292 May  2 11:33 myfile
-rw-r--r--. 1 root root  5242880 May  2 11:55 myfile_00
-rw-r--r--. 1 root root  5242880 May  2 11:55 myfile_01
-rw-r--r--. 1 root root  5242880 May  2 11:55 myfile_02
-rw-r--r--. 1 root root  5242880 May  2 11:55 myfile_03
-rw-r--r--. 1 root root  5242880 May  2 11:55 myfile_04
-rw-r--r--. 1 root root  3594892 May  2 11:55 myfile_05
```

- `uniq` được dùng để loại bỏ các dòng liền kề giống nhau.




## 11 Vim => Vimtutor
Vim là một trình editor. Nó chứ bộ phím tắt đồ sộ giúp cho việc soạn thảo thuận tiện hơn

```sh
vim file_name
```

Sẽ tạo một mở file hoặc tạo file mới nếu file chưa tồn tại.

- Di chuyển con trỏ chuột. Sử dụng các phím mũi tên hoặc `H`: sang trái, `J`: xuống, `K`: lên, `L`: sang phải.
- Về đầu file `gg`, đến dòng cuối của file `shift + g`
- Sử dụng `v` với các phím mũi tên để bôi đen hoặc `V`
- Tìm kiếm: `?<text>, /<text>`
- `i` để chèn văn bản, `R` để replace
- Thoát: `:q` thoát, `:q!` thoát mà không lưu, `:w` lưu file, `:wq` lưu và thoát


### 12 Byobu
Byobu là một tiện ích terminal giúp cho người sử dụng terminal được thuận tiện hơn.

- Cài đặt Byobu

Ubuntu

```sh
apt install -y byobu
```

CentOS

```sh
yum install -y byobu
```

- Enable tự động chạy byobu khi người dùng log on

```sh
# byobu-eable
```

- Ấn `F9` để xem menu. Sau đó chọn `help` để xem các chức năng cũng như hướng dẫn của byobu.

Byobu cho phép ta sử dụng nhiều terminal. Tạo một terminal mới bằng phím `F2`

  ![Imgur](https://i.imgur.com/zbaXUYf.png)

Ta có 2 cửa sổ terminal

- Chuyển qua lại giữa các terminal. Sử dụng phím `F3 / F4` hoặc `alt + Right arrow / alt + Leght arrow`

- Đóng 1 terminal, dùng tổ hợp phím `ctrl + d`

- Sử dụng `F7` kết hợp với `pg up` hoặc `pg dn` để kéo lên kéo xuống terminal thay cho dùng chuột như trước đây.

- Byobu cho phép đặt tên terminal để có thể nhớ task đang làm trên terminal đó. Dùng phím `F8` để đổi tên.
