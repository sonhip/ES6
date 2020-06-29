bài viết được tham khảo từ  [Vilbo của tác giả Trần Văn Mỹ](https://viblo.asia/p/ecmascript-es6-la-gi-overview-es6-gAm5y9RA5db)
## 1. ES6 là gì?
ES6 là chữ viết tắt của ECMAScript 6, đây được coi là một tập hợp các kỹ thuật nâng cao của Javascript và là phiên bản mới nhất của chuẩn ECMAScript. ES6 là một tập hợp kỹ thuật nâng cao của javascript và nó là 1 chuẩn mực để làm theo. Thì ES6 cũng thế nó là một chuẩn mực để cho các framework từ đó mà phát triển lên hay để cho các lập trình viên code js một các tốt ưu và clear nhất.

## 2. Điều kiện để học ES6 là gì?
Điều kiện để học được nó bạn chỉ cần biết chút ít kiến thức căn bản về javascript và môt thứ không thể thiếu nữa đó là Browser phiên bản 2015 trở lên các bạn nhé! Vì sao ư??? Vì ES6 ra đời vào năm 2015 nên những trình duyện phiên bản 2015 mới hỗ trợ ES6.
## 3. Tổng quát các tính năng cơ bản của ES6

 - Block - Scoped Constructs Let and Cont
 -  Arrow Function
 -  Rest Parameter
 -  Destructuring Assignment in ES6
 -  Default Parameters in ES6
 -  Template Literals in ES6
 -  Multi-line String in ES6
 -  Enhanced Object Literals in ES6
 -  Promises in ES6
 -  Classes in ES6
## 4. Tìm hiểu về các tính năng
Copy đến đây thôi, giờ là những thứ mình chắt lọc được từ việc học ES6 trên freecodecamp.
 1.  Sự khác nhau giữa từ khóa **var** và **let**
```js
var camper = 'James';
var camper = 'David';
console.log(camper);
// logs 'David'
```
Như bạn thấy thì biến camper có giá trị ban đầu 'Jame' đã bị khai báo đè bởi giá trị 'David', trong các đoạn code nhỏ dường như nó sẽ không phải là vấn đề. Nhưng trong một đoạn code lớn, bạn lỡ vô tình ghi đè lên một biến đã tồn tại, hành vi này không xuất ra lỗi nên rất khó để phát hiện và chỉnh sửa. Vậy nên **let** trong ES6 được giới thiệu để giải quyết vấn đề tiềm tàng này.    
```js
let camper = 'James';
let camper = 'David'; // throws an error
```
> Lỗi này có thể xuất hiện trên console của bạn. Bạn có thể sử dụng 'use strict' để có thể bắt các lỗi thường gặp.

 2. Phạm vi sử dụng của **let** và **var**
```js
var printNumTwo;
for (var i = 0; i < 3; i++) {
  if (i === 2) {
    printNumTwo = function() {
      return i;
    };
  }
}
console.log(printNumTwo());
// returns 3
```
function printNumTwo sẽ in ra 3 chứ không phải là 2, vì giá trị của biến i trong hàm sẽ được update và trả về giá trị của i global chứ không phải giá trị i trong vòng lặp. Trong trường hợp này, việc sử dụng **let** sẽ cho ra kết quả là 2.
```js
'use strict';
let printNumTwo;
for (let i = 0; i < 3; i++) {
  if (i === 2) {
    printNumTwo = function() {
      return i;
    };
  }
}
console.log(printNumTwo());
// returns 2
console.log(i);
// returns "i is not defined"
``` 

biến i nhận giá trị undefined vì khi khai báo i trong vòng lặp với từ khóa let thì biến i chỉ có thể sử dụng trong vòng lặp đó.

3. Cách khai báo và sử dụng const
Khi khai báo từ khóa const trước tên biến, điều đó có nghĩa là biến này sẽ chỉ nhận một giá trị duy nhất và không thể thay đổi.
```js
"use strict";
const FAV_PET = "Cats";
FAV_PET = "Dogs"; // returns error
```
>Thông thường các developers sẽ sử dụng chữ in hoa để làm tên biến cho các giá trị bất biến và sử dụng chữ thường cho các giá trị có thể thay đổi (đối tượng hoặc mảng). 
 
 Tuy nhiên, các đối tượng (mảng và hàm) được gán cho một biến sử dụng const vẫn có thể thay đổi. Việc gán const cho đối tượng chỉ ngăn chặn được việc gán định danh biến đó.
 ```js
"use strict";
const s = [5, 6, 7];
s = [1, 2, 3]; // throws error, trying to assign a const
s[2] = 45; // works just as it would with an array declared with var or let
console.log(s); // returns [5, 6, 45]
```
Như bạn thấy, bạn vẫn có thể thay đổi được mảng đối tượng s = [5,6,7]. Các phần tử tròn s vẫn có thể thay đổi. Nhưng vì const đã được sử dụng, nếu muốn thay đổi ta phải trỏ thẳng đến index của đối tượng mảng s để thay đổi.
Nhưng có một cách ta có thể đảm bảo dữ liệu sẽ khôn bị thay đổi, javascript cung cấp cho ta function ``Object.freeze`` . Một khi object đã được đóng băng, mọi thay đổi sẽ không thể thực hiện.
```js
let obj = {
  name:"FreeCodeCamp",
  review:"Awesome"
};
Object.freeze(obj);
obj.review = "bad"; // will be ignored. Mutation not allowed
obj.newProp = "Test"; // will be ignored. Mutation not allowed
console.log(obj); 
// { name: "FreeCodeCamp", review:"Awesome"}
```
4. Sử dụng hàm mũi tên (Arrow Function) để viết lại ngắn gọn các hàm ẩn danh (Anonymous Function)
```js
const myFunc = function() {
  const myVar = "value";
  return myVar;
}
```
Với ES6 ta có thể viết lại như hàm trên như này: 
```js
const myFunc = () => {
  const myVar = "value";
  return myVar;
}
```
Hoặc với các hàm không có function body như hàm trên thì ta cũng có cách viết gọn hơn nữa là :
```js
const myFunc = () => "value";
```
Cũng như các hàm bình thường, bạn cũng có thể truyền tham số và Arrow function:
```js
// doubles input value and returns it
const doubler = (item) => item * 2;
```
Nếu hàm có 1 tham số duy nhất thì bạn có thể lược bỏ dấu ngoặc đơn đi :
```js
// the same function, without the argument parentheses
const doubler = item => item * 2;
```
Với Arrow function thì bạn cũng có thể truyền vào nhiều tham số :
```js
// multiplies the first input value by the second and returns it
const multiplier = (item, multi) => item * multi;
```
5. Xét tham số mặc định cho function
Để giúp ta linh hoạt hơn trong việc tạo function, ES6 cung cấp cho ta ``default parameters`` cho function.
```js
const greeting = (name = "Anonymous") => "Hello " + name;

console.log(greeting("John")); // Hello John
console.log(greeting()); // Hello Anonymous
```
Tham số mặc định 'Anonymous' sẽ được dùng khi biến name không được định danh (undefined). Bạn cũng có thể tham nhiều tham số mặc định nếu như bạn muốn.

6. Sử dụng Rest Parameter với Function Parameters
 Với Rest Parameter, bạn có thể tạo ra hàm với số lượng lớn tham số truyền vào, các tham số này sẽ được lưu trữ trong một mảng có thể truy cập sau đó từ bên trong hàm.
 ```js
function howMany(...args) {
  return "You have passed " + args.length + " arguments.";
}
console.log(howMany(0, 1, 2)); // You have passed 3 arguments.
console.log(howMany("string", null, [1, 2, 3], { })); // You have passed 4 arguments.
```


    
    
