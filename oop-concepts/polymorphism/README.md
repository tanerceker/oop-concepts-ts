# Polymorphism — Çokbiçimlilik

Çokbiçimlilik, nesne yönelimli programlamada (OOP) farklı sınıflardaki nesnelerin ortak bir üst sınıfın nesneleri olarak ele alınmasını sağlayan temel bir kavramdır.

<br/>

---

<br/>

## Typescript'te Çokbiçimlilik

Tek bir arayüz (interface) veya yöntemin farklı veri türleriyle çalışmasını sağlayarak kodda esneklik ve yeniden kullanılabilirlik sağlar. OOP'deki üç ana çokbiçimlilik türü şunlardır:

<br/>

1. **Alt tür çokbiçimlilik (Subtype polymorphism):**
   <br/>
   Kalıtım (Inheritance) veya Uygulama çokbiçimliliği (Implementation polymorphism) olarak da bilinir.
   <br/>

2. **Parametrik çokbiçimlilik (Parametric polymorphism):**
   <br/>
   Jenerik (Generics) olarak da bilinir).
   <br/>

3. **Ad hoc çokbiçimlilik (Ad hoc polymorphism):**
   <br/>
   Fonksiyon aşırı yükleme (Function overloading) veya Operatör aşırı yükleme (Operator overloading) olarak da bilinir.

<br/>

---

<br/>

## Alt Tür Çokbiçimlilik — Subtype Polymorphism

OOP bağlamında, alt tür çokbiçimliliği (subtype polymorphism) en yaygın kullanılan biçimdir.
Bir alt sınıfın (subclass) bir üst sınıftan (superclass) özellikleri (properties) ve yöntemleri (methods) miras aldığı ve ayrıca miras alınan özellikleri ve yöntemleri geçersiz kılabildiği (override) veya genişletebildiği (extend) kalıtım yoluyla elde edilir.

Kalıtım (Inheritance) yoluyla alt tür çokbiçimliliği göstermek için bir örnek:

```tsx
// Ortak bir yöntem olan 'area' ile bir temel sınıf 'Shape' tanımlayın
abstract class Shape {
  abstract area(): number;
}

// 'Shape' temel sınıfını genişleten bir 'Rectangle' sınıfı tanımlayın
class Rectangle extends Shape {
  constructor(private width: number, private height: number) {
    super();
  }

  // 'Rectangle' için 'area' yöntemini geçersiz kılın
  area(): number {
    return this.width * this.height;
  }
}

// 'Shape' temel sınıfını genişleten bir 'Circle' sınıfı tanımlayın
class Circle extends Shape {
  constructor(private radius: number) {
    super();
  }

  // 'Circle' için 'area' yöntemini geçersiz kılın
  area(): number {
    return Math.PI * this.radius * this.radius;
  }
}

// 'Rectangle' ve 'Circle' örneklerini oluşturun
const rect: Shape = new Rectangle(5, 4);
const circle: Shape = new Circle(3);

// Bir dizi şeklin toplam alanını (area) hesaplamak için ortak arayüzü
// kullanacak bir fonksiyon tanımlayın
function getTotalArea(shapes: Shape[]): number {
  return shapes.reduce((totalArea, shape) => totalArea + shape.area(), 0);
}

// getTotalArea fonksiyonunu farklı şekil nesnelerinden oluşan bir dizi ile kullanın
const totalArea = getTotalArea([rect, circle]);
console.log(`Total area of shapes: ${totalArea}`);
```

Bu örnekte, area soyut yöntemine (abstract method) sahip bir Shape soyut sınıfı (abstract class) tanımlıyoruz. Rectangle ve Circle sınıfları Shape'i genişletir (extend) ve area yöntemini kendi uygulamalarıyla geçersiz kılar (override). Daha sonra Rectangle ve Circle örneklerini (instances) Shape örnekleri olarak ele alabilir ve bir dizi şeklin toplam alanını hesaplamak için getTotalArea fonksiyonunu kullanabiliriz. Bu, farklı şekil nesneleri (shape objects) ortak üst sınıf (common superclass) Shape'in örnekleri (instances) olarak ele alınabildiğinden, çokbiçimliliği eylem halinde gösterir.

<br/>

---

<br/>

## Parametrik Çokbiçimlilik — Parametric Polymorphism

Jenerik (Generics) olarak da bilinen parametrik çokbiçimlilik (parametric polymorphism), bir fonksiyon, sınıf veya arayüzün herhangi bir somut (concrete) türe bağlı olmadan birden fazla türle çalışabildiği bir çokbiçimlilik şeklidir. Aynı kodun farklı veri türleriyle çalışmasına olanak tanıyıp esneklik, yeniden kullanılabilirlik ve tür güvenliği sağlar.

Typescript'teki jenerikler (generics), parametrik çokbiçimliliği uygulamanın bir yoludur.
Tür parametrelerini (Type parameters) kullanarak, tür bilgilerini korurken birden çok türle çalışabilen jenerik fonksiyonlar (generic functions), sınıflar (classes) veya arayüzler (interfaces) oluşturabilirsiniz.

Typescript kullanarak jenerikler (generics) aracılığıyla parametrik çokbiçimliliği (parametric polymorphism) gösteren bir örnek:

```tsx
// Girdi değerini döndüren jenerik bir 'identity' fonksiyonu tanımlayın
function identity<T>(value: T): T {
  return value;
}

// 'identity' fonksiyonunu farklı veri türleriyle kullanın
const numIdentity: number = identity<number>(42);
const strIdentity: string = identity<string>("Hello, TypeScript!");

console.log(`Number identity: ${numIdentity}`);
console.log(`String identity: ${strIdentity}`);

// Aynı türden iki değeri saklayabilen jenerik bir 'Pair' sınıfı tanımlayın
class Pair<T> {
  constructor(public first: T, public second: T) {}

  // Birinci ve ikinci değerleri değiştirin
  swap(): void {
    const temp = this.first;
    this.first = this.second;
    this.second = temp;
  }
}

// 'Pair' sınıfını farklı veri türleriyle kullanın
const numPair: Pair<number> = new Pair(1, 2);
const strPair: Pair<string> = new Pair("Alice", "Bob");

numPair.swap();
strPair.swap();

console.log(`Number pair after swap: (${numPair.first}, ${numPair.second})`);
console.log(`String pair after swap: (${strPair.first}, ${strPair.second})`);
```

Bu örnekte, T türünde bir parametre ve T türünde bir değer kabul eden ve değeri değiştirmeden döndüren jenerik (generic) bir identity fonksiyonu tanımlıyoruz. Bu fonksiyon sayılar (numbers) ve dizeler (strings) gibi farklı veri türleriyle kullanılabilir.

Ayrıca, T türünde bir parametre kabul eden ve aynı türden iki değeri saklayabilen jenerik (generic) bir Pair sınıfı tanımlarız. Pair sınıfının birinci ve ikinci özelliklerinin (properties) değerlerini değiştiren bir swap yöntemi (method) vardır. Pair sınıfı, tür güvenliğini koruyup sayılar (numbers) ve dizeler (strings) gibi farklı veri türleriyle kullanılabilir.

Jenerikleri (Generics) kullanarak, belirli bir somut türe (concrete type) bağlı olmadan farklı türlerle (types) çalışabilen yeniden kullanılabilir ve esnek bir kod oluştururuz. Bu, Typescript'te parametrik çokbiçimliliğin (parametric polymorphism) bir örneğidir.

<br/>

---

<br/>

## Örneklerle Çokbiçimlilik

Javascript ve Typescript alanında, çokbiçimlilik çeşitli kütüphanelerde ve çerçevelerde gözlemlenebilir. Bu kütüphanelerden biri de Node.js için minimalist bir web çerçevesi olan Express.js'dir.

Express.js'deki çokbiçimliliğin güzelliği özellikle ara katman fonksiyonlarının (middleware functions) kullanımında takdir edilebilir.

<br/>

### Ara Katmanın (Middleware) Büyüsü

Ara katman fonksiyonları (Middleware functions), istek nesnesine (request object), yanıt nesnesine (response object) ve uygulamanın istek-yanıt döngüsündeki (request-response cycle) bir sonraki fonksiyona erişimi olan fonksiyonlardır. Ara katman fonksiyonları, herhangi bir kodu yürütmek, istek ve yanıt nesnelerinde değişiklik yapmak, istek-yanıt döngüsünü sonlandırmak ve yığındaki (stack) bir sonraki ara katmanı (middleware) çağırmak gibi çeşitli görevleri yerine getirebilir.

<br/>

#### İstek (Request), Yanıt (Response) ve NextFunction'ı Anlamak

Typescript ile Express.js'de Request, Response ve NextFunction, Express.js tür tanımları tarafından sağlanan arayüzlerdir (interfaces).

<br/>

- **Request (İstek):** İstek sorgu dizesi, parametreler (parameters), gövde (body), HTTP üstbilgileri (HTTP headers) ve daha fazlası için özellikler içeren HTTP isteğini temsil eder.
  <br/>
- **Response (Yanıt):** Bir Express uygulamasının bir HTTP isteği aldığında gönderdiği HTTP yanıtını (HTTP response) temsil eder. HTTP yanıtını göndermek için res.send(), res.json(), res.sendFile() ve daha fazlası gibi yöntemleri vardır.
  <br/>
- **NextFunction:** Kontrolü bir sonraki ara katman fonksiyonuna (next middleware function) geçirmek için çağırdığınız bir sonraki fonksiyonu temsil eder.

<br/>

---

<br/>

#### Express.js Ara Katmanı (Middleware): Çokbiçimlilik için Bir Oyun Alanı

Express.js'de ara katman kullanımı, çokbiçimliliğin iş başındaki en iyi örneğidir. Ara katman fonksiyonları, dahili farklılıklarına rağmen, hepsi aynı arayüze (interface) bağlıdır. Request, Response ve NextFunction parametrelerini kabul ederler, bu da bir Express.js uygulamasının ara katman yığınında (middleware stack) birbirlerinin yerine kullanılabilecekleri anlamına gelir.

Basit bir örneğe bakalım:

```tsx
import express, { Request, Response, NextFunction } from "express";

const app = express();

const middleware1 = (req: Request, res: Response, next: NextFunction) => {
  console.log("Middleware 1");
  next();
};

const middleware2 = (req: Request, res: Response, next: NextFunction) => {
  console.log("Middleware 2");
  next();
};

app.use(middleware1);
app.use(middleware2);

app.listen(3000, () => {
  console.log("Server started");
});
```

Bu kod parçasında, middleware1 ve middleware2 farklı fonksiyonlardır ancak aynı arayüzü (interface) takip ettikleri için her ikisi de Express.js uygulamasında ara katman (middleware) olarak kullanılabilir. Farklı ara katman fonksiyonları (middleware functions) uygulamanın ara katman yığınında (middleware stack) birbirinin yerine kullanılabildiğinden, bu çokbiçimliliğin (polymorphism) bir tezahürüdür.

---

— Taner Çeker tarafından hazırlanmıştır.
