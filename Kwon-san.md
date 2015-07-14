# Template về cách viết ticket

## Bug
### Khi báo cáo về bug

 [Ticket title]
Nội dung bug phải được viết đơn giản dễ hiểu, dễ truyền đạt

 [Trình tự tái hiện]
1. Thực hiện trình tự tái hiện bug
2. Bằng level thao tác
3. Lưu ý cách làm sao cho người khác nhiều vào có thể hiểu được 1 cách dễ dàng.
4. Ghi theo kiểu gạch đầu dòng(liệt kê)


 [Nội dung bug]  
Đối với trình tự tái hiện bên trên, thì ghi lại hiện tượng nào đang xảy ra trong hiện tại.

 [Nội dung yêu cầu chỉnh sửa]  
    Ghi rõ việc fix như thế nào khi dựa vào nội dung bug

#### Ví dụ
[Title]  
Phát sinh error về việc đăng ký trong màn hình đăng ký thành viên

[Trình tự tái hiện]
1. Hiển thị màn hình TOP
2. Click vào button「đăng ký thành viên」phía trên của màn hình
3. Nhập hoge@hoge.com vào khung mail address, nhập giá trị đúng vào những field input khác. 
3. Nhập nội dung đúng để không phát sinh validation error
4. Click vào button [đăng ký]

[Nội dung bug]  
Dù có nhập đúng giá trị mail address nhưng vẫn phát sinh validation error, không thể đăng ký thành viên được.

### Khi fix bug
[Nguyên nhân của bug]  
Sau khi đã thực hiện trình tự tái hiện như trên, ghi chi tiết tại thời điểm nào 
thì phát sinh error và đó là error như thế nào.

[Phương pháp đối ứng]  
Ghi ra tất cả các nội dung đã đối ứng dựa trên nguyên nhân của bug.

[Pull request URL]  
Nội dung đã chỉnh sửa thì sẽ không commit trực tiếp mà sẽ đối ứng theo kiểu tạo ra pull request. 
Do vậy, nên nhất thiết phải dán pull request URL vào.

Điểm lưu ý
Mặc dù sẽ thành kiểu quản lý 2 lớp, nhưng khi tạo pull request thì cũng cần phải ghi 
nguyên nhân của bug bên trên cũng như phương pháp đối ứng vào.

#### Ví dụ
[Nguyên nhân của bug]  
Validation error message liên quan đến mail address thì đã được định nghĩa bằng controler đăng ký thành viên.
Vì vậy, do có sự khác nhau trong logic phán định mail address này, nên dẫn đến việc phát sinh error.

[Phương pháp đối ứng]  
1. Do có nhầm lẫn trong logic phán định mail trong controler nên sẽ xóa validation error check trong controler tương ứng.

[Pull request URL]  
https://github.com/SekaiLab/Plaim/......

## Task
### Khi tạo task
[Title]  
Ghi đơn giản nội dung của task

[Scenario đơn giản]  
Ghi đơn giản mục đích của việc phát triển chức năng của lần này.

[Normal flow]
1. Sau khi xong thực hiện function lần này
2. Xử lý cần thiết
3. Tại chính thời điểm nào
4. Trong table nào
5. Đăng ký giá trị nào
6. Khi đã input giá trị đúng
7. Flow
8. Viết gạch đầu dòng(kiểu liệt kê)
9. Nếu cần thì sẽ attach thêm hình ảnh hoặc tài liệu vào trong ticket này
10.Attach

[Error handling]
1. Trường hợp đã phát sinh error trong khi thực hiện flow bình thường
2. Thực hiện xử lý error như thế nào
3. Ghi theo từng nội dung error

[Check list đơn giản]
1. Mặc dù chưa được nói đến trong flow bên trên nhưng đương nhiên là phải ghi nội dung cần thực hiện bằng check list

#### Ví dụ
[Title]
Thực hiện chức năng trả tiền(payment) của user

[Scenario đơn giản]
Thực hiện chức năng trả tiền(payment) trên plaim.jp, và những user có trả tiền thì có thể 
sử dụng được chức năng mà user dùng miễn phí không thể sử dụng được.

Sử dụng hệ thống bên ngoài gọi là hệ thống trả tiền paygent, 
có thể thực hiện việc thanh toán bằng credit card và thanh toán tại cửa hàng 24h

[Normal flow]

- Màn hình
    1. Click vào button 「課金登録/đăng ký trả tiền」
    3. Màn hình của Paygent sẽ được hiển thị.
    2. Chọn phương pháp thanh toán (thanh toán bằng credit hay cửa hàng 24h)
    3. Trường hợp thanh toán bằng credit card, nhập mã số của credit card, và hạn sử dụng(định dạng: MM/YY), nhập security code
    4. Trường hợp thanh toán bằng cửa hàng 24h thì chọn cửa hàng sẽ tiến hành thanh toán
    5. Click vào button [登録/đăng ký]


- Xử lý trên server
    1. Từ flow thanh toán bằng credit card và thanh toán bằng cửa hàng 24h, dựa trên phương pháp thanh toán, để thực hiện 1 trong 2 logic thanh toán. 
    2. Trường hợp thanh toán bằng credit card thì sẽ nhập request parameter dùng để thanh toàn bằng credit trong Paygent(Parameter sẽ tham khảo trong file khác) sau đó gửi đi.
    3.Trường hợp response code là 200 và ko có ErrCode, thì sẽ set unique code đã được trả về từ Paygent gồm userID, 
    số tiền thanh toán, ngày thanh toán ở trong table lịch sử thanh toán(t_payment), sau đó thực hiện xử lý đăng ký DB.
    4. Set ON cho flag thanh toán trong user table(t_user) và thực hiện xử lý update.

- Error handling
    * Trường hợp giá trị ko phải là code thanh toán bằng credit và code thanh toán bằng cửa hàng 24h đã được gửi về
        1. Error message do code chi trả bị sai sẽ được hiển thị
    * Trường hợp user đã thực hiện xử lý thanh toán lại 1 lần nữa mà không quan tâm là việc xử lý thanh toán đã hoàn tất hay chưa
        1. Hiển thị error message về nội dung việc đăng ký đã hoàn tất  lên trên màn hình
    * Trường hợp error code được trả về từ Paygent
        1. Hiển thị error message về lỗi thanh toán lên trên màn hình
    * Trường hợp việc đăng ký vào table lịch sử thanh toán đã hoàn tất bình thường rồi nhưng lại phát sinh error sau khi xử lý
        1. Hiển thị error message lỗi xử lý lên trên màn hình
        2. Nội dung đã được đăng ký trong table lịch sử thanh toán sẽ được rollback
        3. Chạy API cancel thanh toán đối với Paygent
    * Trường hợp đã hoàn tất việc đăng ký vào trong table lịch sử user và table lịch sử thanh toán mà phát sinh lỗi sau khi xử lý
        1. Hiển thị error message lỗi xử lý lên trên màn hình
        2. Rollback nội dung đã đăng ký và table user, table lịch sử đăng ký
        3. Chạy API cancel thanh toán đối với Paygent

[簡易チェックリスト]  
1. ユーザー情報は必ずセッションに格納されているユーザーIDからDBアクセスして取得すること
[3:50:17 PM] Kiheng Kwon: ＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝
[3:50:19 PM] Kiheng Kwon: # Plaim 今週の予定

1. Plaimのデプロイ作業
→今まで溜まっていている負債を完済しないと次の施策に映るのが難しい
2. 現在devブランチに上がっていて、本番に上がっていないソースコードの整理
3. テスト仕様書の作成
4. 結合テストが出来る状態