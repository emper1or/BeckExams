
CORS. Preflighted Request.

CORS - cross origin  Resource Sharing, штука которая нужно для того, чтобы отправлять запросы к другому домену со своего домена. По умолчанию в браузере есть SOM (single orugin policy), браузер запрещает делать запросы с одного домена на другой.
Благодаря CORS это условие ослабляется и появляется возможность делать запросы между разными доменами. Перед запросом браузер определяет сложный это запрос или нет. К простым запросам относятся GET, HEAD, POST (сложно сломать сайт этими запросами). 
Если запрос простой, то браузер добавляет у запросу:
```text
Origin: example.com
```
В ответ на это сервер должен вернуть что то из этого:
```text
Access-Control-Allow-Origin: example.com
Access-Control-Allow-Origin: *
```
В противном случает запрос блокируется.

Если запрос не простой или содержит кастомный заголовок (DELETE, включает заговок Autorization тп). При этом в заголовки запроса добавляется Access-Control-Request-Method, в его значение передается название метода, который мы хотим сделать, пример может быть таким.
```http
OPTIONS /api/resource HTTP/1.1
Host: api.example.com
Origin: https://myapp.com
Access-Control-Request-Method: POST
Access-Control-Request-Headers: Content-Type, Authorization
```
Ответ от сервера в таком случаем должен быть таким:
```http
HTTP/1.1 200 OK
Access-Control-Allow-Origin: https://myapp.com
Access-Control-Allow-Methods: POST, GET, OPTIONS
Access-Control-Allow-Headers: Content-Type, Authorization
```
Если все ок (заголовки, методы допустимые), то браузер отправляет уже нормальный запрос.

Простые заголовки
- Connection, User-agent, Content-Length ....  
- Accept  
- Accept-Language  
- Content-Language  
- Content-Type  
- application/x-www-form-urlencoded  
- multipart/form-data  
- text/plain

CORS не влияет на запросы, выполняемые:
- Через серверный код
- С помощью утилит вроде curl или Postman
- и др.