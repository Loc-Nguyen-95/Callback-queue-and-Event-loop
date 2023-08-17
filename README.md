# Callback queue and Event loop

JS là ngôn ngữ lập trình đơn luồng (1 câu lệnh được thực thi tại 1 thời điểm) và thực thi đồng bộ (thực thi theo thứ tự) </br>
Trong core JS engine, có 3 phần (stack) chính:

1. Thread execution
2. Memory (varible enviroment)
3. Call stack

Nay thêm 1 số thành phần mới 

4. Web browser APIs
5. Promise 
6. Event loop, callback queue , micro stack queue 
