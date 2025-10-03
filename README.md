# Bug-lang docs

Assalomu Alaykum `bug-lang` haqida qisqacha malumot. Buglang `interpreter` dasturlash tili, `golangda` yozilgan. Bu tilni yaratishdan asosiy maqsad yo’q 😁 to’g’ri o’zim  o’rganish uchun yaratdim lekin sizga foydasi yo’q ko’dini ko’rib chiqsangiz foydasi tegishi mumkun

> Documentatsiyani yozishdan avval zerikishni boshladim biror nima qolib ketgan bo’lishi mumkun lekin barchasi examples papkasida yozilgan ko’rib chiqishingiz mumkun
> 

# O’rnatish

O’rnatishni `ikkita usuli` mavjud biri `source code` ni clone qilib olib build qilish yoki `release`dan kerakli binary fayilni yuklab olish. Hozir biz ikkinchi usuldan foydalanamiz

Binary fayilni yuklab olish

```bash
# Ubuntu
curl -O https://github.com/UzStack/bug-lang/releases/download/v1.1.7/buglang-ubuntu
```

```bash
# Mac
curl -O https://github.com/UzStack/bug-lang/releases/download/v1.1.7/buglang-macos
```

```bash
# Windows
curl -O https://github.com/UzStack/bug-lang/releases/download/v1.1.7/buglang-windows.exe
```

foydalanish juda oddiy shunchaki binary joylashgan papkaga o’ting va .`/buglang-<system> ./main.bug`. Masalan `./buglang-ubuntu ./main.bug`

# Foydalanish

## O’zgaruvchilar

Buglangda o’zgaruvchi yaratish uchun shunchaki `key = value` dan foydalaniladi

```jsx
name = "Samandar"
age = 20
.....
```

### List

```jsx
// yangi list yaratish
numbers = [20.4324, 324.423432, 10.21];

// yangi element qo'shish
numbers.append(100);

// List o'lchamini olish
numbers.size();

/// Element mavjud ekanligini tekshirish
numbers.contains(100); 

// List ichidan elementni olish uchun index dan foydalanish mumkun to'rtburchak qavslar yordamida
println(numbers[0]);
```

### Dict

```jsx
// dictionary yaratish
users = [
    { "name": "Samandar", "age": 20, "id": 1 },
    { "name": "Nomalum", "age": 100, "id": 2 }
]; 

// yangi element qo'shish
users[0]["new_item"] = "salom";

// Elementni olib tashlash
users[0].remove("age");

// Element qiymatini olish
println(users[0]["name"]);
```

## Loop

Faqatgina for loop mavjud boshqa loop yo’q

```python
i = 0;
for (i < users.size()) {
    user = users[i];
    println("name: ", user["name"]);
    i = i + 1;
}
```

## Funcsiyalar

Funcsiya yaratish uchun `func` kalit so’zidan foydalaniladi

```python
func getName(){
	return "Samandar";
}
```

## Classlar

Buglangda classlar ham mavjud `class` kalit so’zi yordamida yaratiladi

```python
class ClassName() {
}
```

`Konstructor method` class yaratilganda ishga tushadigan funcsiya `init` nomli funcsiya pythonda o’g’irladim 😁

```python
class ClassName() {
    func init() {
	      this.name = "A";
	  }
}
```

`Desctructor` mavjud emas chunki `garbage collection` ni o’zi yo’q 

### Nasil olish

```jsx
// Define class A
class A() {
    func init() {
        this.name = "A";
    }
    func getName() {
        return this.name;
    }
}

// Define class B
class B() {
    func init() {
        this.name = "B";
    }
    func getName() {
        return this.name;
    }
}

// Define class C inheriting from B and A
class C(B, A) {
    func init() {
        super(A).init(); // super yordamida ota classdagi funcsiyani chaqirish mumkun
        println(this.name); // Chiqarish: A
        super(B).init();
        println(this.name); // Chiqarish: B
        this.name = "C";
    }
    func getName() {
        return this.name;
    }
}
```

## Ichki (built-in) funksiyalar

- `println(...)`: konsolga argumentlarni chiqaradi, bir nechta argumentlarni bo'sh joy bilan birlashtiradi.
- `header(”Content-Type”, “application/json”)`: web requestlar uchun response uchun header yuboradi

## Built-in kutubxonalar

- requests
- math
- json
- pgsql

### requests

```jsx
import "requests";

response = requests.request("POST", "https://blog.jscorp.uz/api/project/?page=1");

print(response.json());
```

### math

```jsx
println(math.round(10.2121, 2));
```

### json

```jsx
import "json";

json.decode("{\"name\":\"Samandar\"}"); // result: {"name": "Samandar"} type: dict
json.encode({"name":"Samandar"}); //result: {\"name\":\"Samandar\"} type: string
```

### pgsql

```jsx
import "psql";

db = new psql.DB("db");

query = db.query("select * from users");
print(query.findAll());
```

## Global o’zgaruvchilar

- `_GET`: request get params
- `_POST`: request post data
- `_REQUEST`: request
- `_GLOBALS`: Barcha global o’zgaruvchilar

## Module import

ko’dlarni bir nechta faytillarga bo’lib yozilganda import qilish uchun `import` kalit so’zidan foydalaniladi

```jsx
// utils.bug
func getHello(name="Samandar"){
	return "Salom "+name;
}
```

```jsx
// main.bug
import "utils.bug";

println(getHello());
println(getHello("Polonchi"));
```

# Bug-fpm

`bug-fpm` bu php-fpm alternativi yani buglangni web uchun ishlatishga yordam beradigan dastur

`examples` papkasida `api example` ko’rsatilgan

## O’rnatish

```bash
curl -O https://github.com/UzStack/bug-lang/releases/download/v1.1.7/fpm-ubuntu
```

Dasturni yuklab olganingizdan keyin ishga tushurib qo’ying avtomatik backgroundda ishga tushmaydi.

### nginx sozlash

`bug-fpm` `php-fpm` kabi ishlaydi nginx config ham birxil bo’ladi `fastcgi_pass` ga `bug-fpm` sock beriladi default sock path `/tmp/bug-fpm.sock`

```bash
    server {
        listen       80;
        server_name  _;
        root /project/path/;
        
        index index.bug index.html index.php;

        location / {
          try_files $uri $uri/ /index.bug?$args;
        }

        location ~ \.bug$ {
		      include fastcgi_params;
		      fastcgi_pass unix:/tmp/bug-fpm.sock;
        }
    }

```

# Bog’lanish

**Azamov Samandar**

**Telegram**: [@Azamov_Samandar](https://t.me/Azamov_Samandar)

**Web**-Site: https://jscorp.uz

**Telefon no’mer**: +998 88 811-23-09

**email**: admin@jscorp.uz
