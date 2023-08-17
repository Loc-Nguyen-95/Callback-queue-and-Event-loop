# Callback queue and Event loop

JS là `ngôn ngữ lập trình đơn luồng` (1 câu lệnh được thực thi tại 1 thời điểm) và thực thi đồng bộ (thực thi theo thứ tự)

Trong core JS engine, có 3 phần (stack) chính:

1. Thread execution
2. Memory (varible enviroment)
3. Call stack

Nay thêm 1 số thành phần mới 

4. Web browser APIs
5. Promise 
6. Event loop, callback queue , micro stack queue

## 🎃 VD
```swift
function printHello() {
  console.log(“hello”);
}
setTimeout(printHello, 1000)
console.log(“me first”);
```
Khi ta chạy chương trình nó sẽ thực thi lần lược như sau:

1. Khai báo function ở `Global memory`
2. Thực thi setTimeout: nhiệm vụ được chyển sang `Web browser feature`: **Timer** (duration: 1000ms và function:  printHello) -> lúc này (khi mới vừa chuyển qua, ban đầu là 1ms) thì status của Timer chưa hoàn thành -> quay lại global 
3. Ở global: `Thread execution` đi tiếp và thực thi in ra “me first” ở thời điểm 2ms

**Lưu ý:** Timer vẫn đang chạy 

4.Khi đạt đến 1000ms On completion xác nhận hoàn thành, printHello được đẩy vào `Call stack` và thực thi in ra “hello”

## 🎉 Tổng kết 

JS engine ưu tiên thực hiện code như thế nào ?

- Code golobal thực thi trước, theo thứ tự 
- Sau đó kiểm tra call stack có trống không, nếu trống -> lấy code từ callback queue (nơi thêm vào các callback function) để thực thi
  
➡️ Sau khi global đã thực thi hết code -> kiểm tra call stack -> nếu trống -> callback queue lấy callback function -> đưa vào call stack để thực thi 

➡️ event loop làm tất cả những việc trên 

Event loop sẽ làm nhiệm vụ kiểm tra ở `Global execution context` đã thực thi hết code chưa, `Call stack` có đang trống không -> nếu 2 điều kiện trên thoả mãn thì đi đến callback queue để lấy code thực hiện (từ cái cũ nhất) 
