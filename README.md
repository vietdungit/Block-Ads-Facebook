# Trình chặn quảng cáo trên bảng tin Facebook

- đơn giản chỉ là việc xoá những bài viết có quảng cáo [Được tài trợ]
- Cũng có thể thay thế vị trí bài viết đó bằng những gì bạn muốn

### Extension có những gì ?
- 1 File manifest.json để khai báo, 1 File content.js để thực hiện  xoá bài viết có quảng cáo
- Chúng ta khai báo những gì trong manifest.json
```sh
{
  "name": "Getting Started Example",
  "version": "1.0",
  "description": "Build an Extension!",
  "content_scripts": [
   {
     "matches": ["https://*.facebook.com/*"],
     "js": ["content.js"],
     "run_at": "document_end"
   }],
  "manifest_version": 2
}
```

```sh
Giải thích một chút về khai báo content_scripts
- matches : khai báo url mà file content.js có thể hoạt động
- js : khai báo file content.js
```

```sh
Ý tưởng để viết file content.js
- lấy ra tất cả bài viết đang hiển thị trên màn hình
- tìm những bài viết có nội dung quảng cáo [Được tài trợ]
- Xoá những bài viết đó
```
- Trong file content.js có gì?
```sh
window.onscroll = function (e) {
// called when the window is scrolled.
    let elements = document.querySelectorAll("[data-pagelet='FeedUnit_{n}']");
    elements.forEach(function (ele, i) {
        if (elements[i].innerHTML.indexOf("Được tài trợ") !== -1) {
            elements[i].remove();
        }
    })
}
```

```sh
Giải thích 1 chút về file content.js
let elements = document.querySelectorAll("[data-pagelet='FeedUnit_{n}']"); // tìm ra tất cả các bài viết
elements.forEach(function (ele, i) {... // vòng lặp để  duyệt qua các bài viết
    if (elements[i].innerHTML.indexOf("Được tài trợ") !== -1) {... // tìm bài viết chứa quảng cáo
       elements[i].remove();  //xoá các bài viết đó
window.onscroll //phát hiện ra hành động lăn chuột
```
