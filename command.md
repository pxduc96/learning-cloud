## Using grep, sed, awk

### 1. grep
grep dùng để tìm một chuỗi. Có thể một chuỗi trong file hoặc trong output.

- 1. Tìm một chuỗi trong một file

```sh
$ grep "chuoi can tim" file_name
```

- 2. Tìm chuỗi có trong nhiều file

```sh
$ grep "chuoi" <danh sách các file>
```

ví dụ: có nhiều file log báo cáo theo ngày với định dạng `report-<date>.log`. Cần tìm các dòng có Error, thực hiện như sau:

```sh
$ grep "Error" report-*.log
```

- 3. Tìm kiếm không phân biệt in hoa in thường

```sh
$ grep -i "chuoi" file_name
```

- 4. Tìm kiếm theo regular expression

```sh
$ grep "regular_here" file
```

- 5. Các cách tìm trên sẽ tìm tất cả các chuỗi con. Ví dụ tìm *no* thì *not, nothing* sẽ xuất hiện ở kết quả. Nếu bạn muốn tìm chính xác, sử dụng `-w`

```sh
$ grep -w "chuoi" file_name
```

- 6. Hiện thị thêm các dòng trước, sau, và xung quanh dòng chứa kết quả

```sh
$ grep -<A, B hoặc C> <n> "chuoi" demo_file
-- A : là after
-- B : là before
-- C : là xung quanh
-- n : là số tự nhiên chỉ định xem hiển thị trước, sau hay xung quang bao nhiêu dòng
```

ví dụ: để hiện thị thêm 3 dòng xung quanh dòng kết quả với kết quả chứa đúng kết quả cần tìm và không phân biệt in hoa in thường

```sh
$ grep -C 3 -iw "chuoi" file_name
```

- 7. Tìm tất cả các file trong thư mục con có chứa chuỗi.

```sh
$ grep -r "chuoi" *
```

lệnh này sẽ tìm `chuoi` trong tất cả các file có trong thư mục con của thư mục hiện tại

- 8. Tìm các dòng không chứa chuỗi, sử dụng option `-v`

```sh
$ grep -v "chuoi" file_name
```

- 9. Đếm số kết quả, sử dụng option `-c`

```sh
$ grep -c "chuoi" file_name
```

- 10. Hiện thị tên file chứa chuỗi

```sh
$ grep -l "chuoi" file_name
```

- 11. Hiện thị dòng của kết quả

```sh
$ grep -n "chuoi" file_name
```


### 2. sed
sed là stream editor. sed được dùng để chỉnh sửa nội dung của file.
Kết quả sẽ được hiện thì lên màn hình. Nếu chuyển hướng kết quả này thì nó sẽ không được hiện thì lên màn hình.

Các ví dụ sau sử dụng file `songs.txt` với nội dung như sau:

```sh
1, Justin Timberlake, Title 545, Price $6.30
2, Taylor Swift, Title 723, Price $7.90
3, Mick Jagger, Title 610, Price $7.90
4, Lady Gaga, Title 118, Price $6.30
5, Johnny Cash, Title 482, Price $6.50
6, Elvis Presley, Title 335, Price $6.30
7, John Lennon, Title 271, Price $7.90
```

- 1. sed có thể được sử dụng để hiện thị nội dung của file

```sh
$ sed '' songs.txt
1, Justin Timberlake, Title 545, Price $6.30
2, Taylor Swift, Title 723, Price $7.90
3, Mick Jagger, Title 610, Price $7.90
4, Lady Gaga, Title 118, Price $6.30
5, Johnny Cash, Title 482, Price $6.50
6, Elvis Presley, Title 335, Price $6.30
7, John Lennon, Title 271, Price $7.90
```

Cách khác sử dụng piping của lệnh cat cho sed

```sh
$ cat songs.txt | sed ''
1, Justin Timberlake, Title 545, Price $6.30
2, Taylor Swift, Title 723, Price $7.90
3, Mick Jagger, Title 610, Price $7.90
4, Lady Gaga, Title 118, Price $6.30
5, Johnny Cash, Title 482, Price $6.50
6, Elvis Presley, Title 335, Price $6.30
7, John Lennon, Title 271, Price $7.90
```

- 2. In ra một số dòng nhất định
In ra dòng đầu tiên

```sh
$ sed -n '1p' songs.txt
1, Justin Timberlake, Title 545, Price $6.30
```

In ra dòng thứ 2 cho đến hết dòng thứ 4

```sh
$ sed -n '2,4p' songs.txt
2, Taylor Swift, Title 723, Price $7.90
3, Mick Jagger, Title 610, Price $7.90
4, Lady Gaga, Title 118, Price $6.30
```

- 3. Xóa các dòng, sử dụng `d`

Ví dụ xóa dòng đầu tiên

```sh
$ sed '1d' songs.txt
2, Taylor Swift, Title 723, Price $7.90
3, Mick Jagger, Title 610, Price $7.90
4, Lady Gaga, Title 118, Price $6.30
5, Johnny Cash, Title 482, Price $6.50
6, Elvis Presley, Title 335, Price $6.30
7, John Lennon, Title 271, Price $7.90
```

- 4. Sử dụng `-i` để sửa nội dung file

```sh
$ cat newfile 
2, Taylor Swift, Title 723, Price $7.90
4, Lady Gaga, Title 118, Price $6.30
6, Elvis Presley, Title 335, Price $6.30

$ sed -i '1d' newfile

$ cat newfile
4, Lady Gaga, Title 118, Price $6.30
6, Elvis Presley, Title 335, Price $6.30
```

- 5. Thay thế nội dung. Nếu muốn sửa nội dung file thêm option `-i`

```sh
$ sed 's/old_word/new_word/' file_name
```

Trên mỗi dòng nếu có 2 old_word, lệnh này chỉ thay thế old_word đầu và bỏ qua các old_word sau đó.

ví dụ thay thế `6.30` thành `7.30` và ghi vào file mới

```sh
$ sed 's/6.30/7.30/' songs.txt > newfile.txt
```

nội dung của newfile.txt như sau:

```sh
1, Justin Timberlake, Title 545, Price $7.30
2, Taylor Swift, Title 723, Price $7.90
3, Mick Jagger, Title 610, Price $7.90
4, Lady Gaga, Title 118, Price $7.30
5, Johnny Cash, Title 482, Price $6.50
6, Elvis Presley, Title 335, Price $7.30
7, John Lennon, Title 271, Price $7.90
```

Để thay thế tất cả các word được tìm thấy, cần thêm `g` như sau:

```sh
$ sed 's/old_word/new_word/g' file_name
```


- 6. Có thể sử dụng để lọc.

```sh
$ sed -n '/John/p' songs.txt
5, Johnny Cash, Title 482, Price $6.50
7, John Lennon, Title 271, Price $7.90
```

- 7. Có thể sử dụng regular thay vì nhập một chuỗi cụ thể


### 3. awk
Awk thường được sử dụng cho việc tìm kiếm và xử lý text

Một số ví dụ về awk

- 1. 






























































