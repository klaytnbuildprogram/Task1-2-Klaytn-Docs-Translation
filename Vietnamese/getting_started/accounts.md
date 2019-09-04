**`CHÚ Ý`**: Chắc  chắn  rằng  bạn  phải  nhớ  password của bạn. Nếu bạn mất password của tài khoản, bạn sẽ không thể truy cập vào tài khoản đó. **Không có tùy chọn_forgot my password_ở đây. Đảm bảo rằng không bao giờ quên.**

Klaytn provides two handy command-line tools, `ken` and `JavaScript console`,  for developers to manage accounts. Lưu ý rằng xuất private key của bạn ở định dạng không được mã hóa sẽ KHÔNG được hỗ trợ.

## ken

Các `ken nhị phân` của Node Endpoin cung cấp quản lý tài khoản thông qua lệnh `acoount`.
Lệnh `account` để tạo một tài khỏa mới, liệt kê các tài khoản hiện có, nhập một private key
vào một tài khoản mới, cập nhật tới môt định dang key mới, và thay đổi password.

### Cách dùng

```bash
$ ken account <command> [options...] [arguments...]
```

**Lệnh**

```bash
$ ken account -help
...
COMMANDS:
     list    Print summary of existing accounts
     new     Create a new account
     update  Update an existing account
     import  Import a private key into a new account
...
```

Bạn có thê nhân thông tin về lệnh con bằng `ken account <command> --help`.

```shell
$ ken account list --help
list [command options] [arguments...]

In một bản tóm tắt ngắn của tất cả các tài khoản

Các tùy chọn KLAY:
  --dbtype value                        Loại cơ sở dữ liệu lưu trữ Blockchain ("leveldb", "badger") (default: "leveldb")
  --datadir "/Users/ethan/Library/KEN"  Thư mục dữ liệu cho database và keystore
  --keystore                            Thư mục của keystore (default = inside the datadir)

Tùy chọn DATABASE:
  --db.no-partitioning  Tắt phân vùng database để lưu trữ liên tục
```

### Thư mục dữ liệu

Các tệp keystore được lưu trữ dưới `<DATADIR>/keystore`. Bạn có thể chỉ định thư mục dữ liệu như dưới đây. Rất khuyến khích thực hiện lệnh `ken account` với tùy chọn `--datadir`. Làm cho thư mục dữ liệu trỏ đến `DATA_DIR` được thiết lập trong `kend.conf` để chia sẻ liền mạch các tài khoản với Node Endpoint của bạn. 

```bash
$ ken account new --datadir <DATADIR>
$ ken account new --datadir "~/kend_home"
```

Nếu bạn không chỉ định thư mục dữ liệu, vị trí mặc định như sau.

- Mac: `~/Library/KEN`
- Linux: `~/.ken`

## Console JavaScript

Để kết nối với JavaScript Console, một EN phải ở trạng thái running. Thông tin nhiều hơn, xem [Triển khai một EN](quick_start/launch_en.md).
Bắt đầu một EN và gắn vào Console như sau.

### Sử dụng

```bash
$ kend start
Starting kend: OK

$ ken attach ~/kend_home/klay.ipc
Welcome to the Klaytn JavaScript console!

instance: Klaytn/vX.X.X/XXXX-XXXX/goX.X.X
 datadir: ~/kend_home
 modules: admin:1.0 debug:1.0 governance:1.0 istanbul:1.0 klay:1.0 miner:1.0 net:1.0 personal:1.0 rpc:1.0 txpool:1.0

>
```

**Lệnh**

Sử dụng `personal` hay `klay` để hiên thị các function đang có. Trong bài hướng dẫn này, chúng ta sẽ truy cập các function sau đây.

```bash
> personal.newAccount()
> personal.importRawKey()
> personal.unlockAccount()
> klay.accounts
> klay.getBalance()
```

### Thư mục dữ liệu

Khi bạn tạo một tài khoản, tập tin keystore được lưu trữ bên dưới`<DATADIR>/keystore`. `<DATADIR>`là `DATA_DIR` được cài đặt trong `kend.conf`. Nếu bạn làm theo hướng dẫn theo hướng nhan hơn với ví dụ đã cho, thì nó phải `~/kend_home`.  
