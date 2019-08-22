# Ajax笔记

使用函数请求（Callback）的方式进行调用

HTTP

- Hypertext transfer protocol

- How requests are made on the internet
  - different request type：GET/POST/PUT/DELETE
  - different parts to a request:
    - headers: request metadata
    - body: data of the request 
    - request URL

JSON

- JavaScript Object Notation
- Consist of key value pairs, separated by colons and brackets
- Why is JSON useful
  - used to transfer data between frontedns and backends

Making an AJAX request 

## 相关操作

`var oReq = new XMLHttpRequest();`

`oReq.addEventListener("load",reqListener);`reqListener指的是返回函数 

`oReq.open("GET",employeeUrl);`

`oReq.send();`