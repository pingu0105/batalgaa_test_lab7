# BUG-06: POST /api/books эвдэрсэн JSON биед 400 биш «200 OK» буцаадаг

Орчин:  Уншлагын жагсаалт v2.0, curl 8.x, Windows 10 Pro (19045), 2026-10-20
Урьдчилсан нөхцөл: node app.js-ийг шинээр асаасан (анхны 3 ном)

## Дахин гаргах алхам
1. Хаалт нь дутуу, эвдэрсэн JSON илгээнэ:
   ```
   curl -i -X POST localhost:3000/api/books -H "Content-Type: application/json" -d '{"title": "Test", "author": "Me",'
   ```
   (Windows cmd: `{"title": "Test", "author": "Me",`-ийг body.json-д хадгалаад `curl.exe -i -X POST http://localhost:3000/api/books -H "Content-Type: application/json" --data-binary "@body.json"`)
2. Статусын мөр болон хариуг харна.
3. `curl -i localhost:3000/api/books` — ном нэмэгдсэн эсэхийг шалгана.

Хүлээгдэж байсан: `HTTP/1.1 400 Bad Request` — спецификаци: «API: буруу JSON биетэй POST хүсэлтэд 400 алдаа буцаана».
Бодит үр дүн:     `HTTP/1.1 200 OK`, бие нь `{"result":"OK"}`. Ном нэмэгдээгүй ч сервер амжилттай гэж хариулдаг тул клиент алдааг мэдэх боломжгүй.

Ноцтой байдал: Major — өгөгдөл чимээгүй алдагдана; API хэрэглэгч хүсэлт амжилтгүй болсныг илрүүлж чадахгүй.
Хавсралт:      evidence/bug-06-curl.txt
Олдсон аялал:  Saboteur (API түвшний довтолгоо)
