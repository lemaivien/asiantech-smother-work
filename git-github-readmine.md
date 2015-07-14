#Git & Github follow
## Các branches
### branch master
Đây là branch dùng để deploy lên server production, trên này hoàn toàn sạch sẽ không chứa bugs.
### branch dev hoặc staging
Đây là branch dùng để deploy lên server staging, dùng cho khách hàng test trước khi đưa lên production. Các issues phải được test kĩ càng hết bug rồi  mới  được phép merge vào đây. 
###Các branch để giải quyết các issue
Khi có 1 issue trên readmine, các dev checkout từ branch dev ra một branch mới có tên theo định dạng: issue_readmine_id. Các dev tiến hành giải quyết các vấn đề , sau khi hoàn thành thì tạo 1 pull request vào nhánh dev để leader để  review và merge code. 
##Các quy tắc về pull request
- Tên pull request phải bắt đầu bằng tên issue đặt trong  dấu []. Vídụ : [1234] Add new js file.
- Tên pull request phải mô tả rõ được những nội dung chính đã fix 
- Tên pull request không được quá dài
- Nội dung mô tả pull request: ghi rõ đã fix những gì giả pháp ra sao và dán link đến issue trên redmine.
##Quy tắc commit
- Không được add quá nhiều file vào một commit, nên chia nhỏ các task để commit nhằm giúp dễ đọc và review code hơn. Ví dụ  thể commit sau hi hoàn thành 1 function hoặc hoàn thành 1 file view. 
- Message của commit tuyệt đối không được dùng  các từ chung chung  như  "Fix  bug", "Fix comment", "add new file", "delete line"....
## Vòng đời của 1 issue 
1. developer checkout branch từ branch dev đổi trạng thái của issue trên redmine thành "In progress"
2. Tiến hành giải quyết vấn đề trên branch vừa tạo 
3. Tạo pull request vào branch dev và chuyển trạng thái "Resolved " , assign cho leader . Comment rõ vấn đề, lý do, cách giải quyết  và  dán link đến pull request trên github. Đối với task thì không cần mô tả lý do. 
4. Leader vào review code. Nếu chưa ok comment vào các dòng code chuyển trạng thái issue thành "In progress" và assign lại cho member, quay lại B2(làm ngay trên branch đã có). Nếu đã ok thì assign cho Tester. 
5. Khi Tester thấy có issue có trạng thái "Resolved" được aassign cho mình thì pull source code của branch đó về máy local của mình để  test hoặc leader có thể tạo môi trường chứa source code của branch đó để tester vào test. Trường hợp có lỗi thì comment lỗi vào readmine và assign lại cho memeber,quay lại B2(làm ngay trên branch đã có). Trong trường hợp ok thì comment và assign lại cho leader.
6. Leader tiến hành merger branch đã ok vào branch dev, deploy lên môi trường staging, comment và chuyển trạng thái issue thành "On Staging" và xóa branch đã merger khỏi github. Khi có bất kì thay đổi nào trên branch dev, leader phải thông báo cho tất cả các member để merger dev vào các branch các member đang làm.  
7. Khách hàng vào test các issue có trạng thái "On Staging" trên môi trường Staging, nếu Ok sẽ chuyển trạng thái thành "Staging OK", ngược lại sẽ assign lại cho leader, leader vào kiểm tra và assign lại cho member, quay lại B2(Tạo branch mới). 
8. Khi khách hàng có yêu cầu deploy, leader liệt kê các issue đã được merger vào dev gửi cho khách hàng. Tiến hành merger cả branch dev vào master, và deploy trên môi trường production, chuyển trạng thái các issue thành "On Production"
9. Khách hàng test lại trên môi trường production, nếu ok thì chuyển trạng thái issue thành "close" kết thúc vòng đời, ngược lại sẽ assign lại cho leader, leader vào kiểm tra và assign lại cho member, quay lại B2(Tạo branch mới).
