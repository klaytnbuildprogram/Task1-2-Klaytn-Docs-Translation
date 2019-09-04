# Tạo tài khoản

## Tạo tài khoản mới

Tạo một tài khoản mới và in địa chỉ lên màn hình. Một tệp keystore được tạo trong thư mục dữ liệu. 

**Tệp Keystore Klaytn**

Khi bạn tạo một tài khoản, đồng nghĩa với một tệp keystore được tạo. Tệp keystore là bản mã hóa duy nhất của private key Klaytn mà bạn sẽ sử dụng để ký vào các giao dịch của mình. Tên của tệp keystore được định dạng như sau:

- `UTC--<created_at UTC ISO8601>-<address hex>`

Nó rất an toàn khi chuyển toàn bộ thư mục hoặc tệp keystore cá nhân giữa các
node Klaytn. Lưu ý trong khi bạn thêm các key tới node từ một node khác,
thứ tự tài khoản có thể bị thay đổi. Vì vậy, hãy chắc chắn bạn không dựa vào chỉ mục trong 
script hay đoạn code của bạn.


### ken

```shell
$ ken account new --datadir <DATADIR>
$ ken account new --password <passwordfile> --datadir <DATADIR>
$ ken account new --password <(echo $mypassword) --datadir <DATADIR>
```

**`CẢNH BÁO`**: Note that using a password file is meant to be used for testing only,  có thể là một ý tưởng tồi khi lưu
password vào một tệp và tuyệt đối không được tiết lộ cho bất cứ ai. Nếu bạn sử dụng cờ password với tệp password, hãy đảm bảo tập tin không thể đọc được hoặc không một ai có thể biết được trừ bạn. Bạn hoàn thành việc này với:

```shell
$ touch /path/to/password
$ chmod 700 /path/to/password
$ cat > /path/to/password
I type my pass here
^D
```

### Console JavaScript

Trên console, bạn có thể chọn function để tạo một tài khoản:

```javascript
> personal.newAccount("passphrase")
```

Tài khoản được lưu dưới dạng mã hóa. Bạn **phải** ghi nhớ cụm mật khẩu này để mở khóa tài khoản của bạn trong tương lai.



## Truy cập tài khoản

Bạn có thể truy cập tài khoản bằng một keyfile. Các keyfile được giả định có chứa một private key được mã hóa như các byte EC nguyên bản được mã hóa thành hex. Hiểu một cách đơn giản, nó là một private key trong một văn bản đơn giản không có `0x` mở đầu. 

Thao tác nhập keyfile có sẵn để mã hóa private key, tạo một tài khoản mới, tạo một tệp keystore trong thư mục dữ liệu, và in địa chỉ trong bảng console. Bạn phải nhớ cụm passphrase để mở khóa tài khoản trong tương lai.

**LƯU Ý**: Nếu bạn có thể sao chép trực tiếp các tệp keystore của mình sang một instance Klaytn khác, cơ chế xuất/nhập này không cần thiết.

### ken

```shell
$ ken account import <keyfile> --datadir <DATADIR>
$ ken account import --password <passwordfile> <keyfile> --datadir <DATADIR>
```

### Console JavaScript

```bash
> personal.importRawKey('{private key}', 'mypassword')
"0xfa415bb3e6231f488ff39eb2897db0ef3636dd32"

// Using a Klaytn wallet key
> personal.importRawKey('{private key}0x000x{address}', 'mypassword')
"0xfa415bb3e6231f488ff39eb2897db0ef3636dd32"
```

