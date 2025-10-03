# Bug-lang docs

Assalomu Alaykum `bug-lang` haqida qisqacha malumot. Buglang `interpreter` dasturlash tili, `golangda` yozilgan. Bu tilni yaratishdan asosiy maqsad yo’q 😁 to’g’ri o’zim  o’rganish uchun yaratdim lekin sizga foydasi yo’q ko’dini ko’rib chiqsangiz foydasi tegishi mumkun

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

Buglangda o’zgaruvchi yaratish uchun chunchaki `key = value` dan foydalaniladi

```jsx
name = "Samandar"
age = 20
.....
```

### List

```jsx
// yangi list yaratish
numbers = [20.4324, 324.423432, 10.21];
// listda ikki dona method mavjud add va size

// yangi element qo'shish
numbers.add(100);

// List o'lchamini olish
numbers.size();

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
- `math.round(number, decimals)`: sonni ko'rsatilgan onalik (desimal) darajagacha yaxlitlaydi.

```python
println(math.round(20.4324, 2)); // Chiqarish: 20.43
```
