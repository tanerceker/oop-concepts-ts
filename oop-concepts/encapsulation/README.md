# Encapsulation — Kapsülleme

Kapsülleme, nesne yönelimli programlamada (OOP) temel bir kavramdır ve verilerin (öznitelikler) ve bu veriler üzerinde çalışan yöntemlerin (fonksiyonlar) tek bir birim, tipik olarak bir sınıf içinde bir araya getirilmesi uygulamasını ifade eder.

<br/>

---

<br/>

## TypeScript'te Kapsülleme

Kapsülleme (Encapsulation), endişelerin ayrılmasını (separation of concerns) ve verilerin gizlenmesini teşvik ederek kod hakkında mantık yürütmeyi, kodu korumayı ve yeniden kullanmayı kolaylaştırır.

Kapsüllemede, bir nesnenin dahili durumu (internal state) harici kod (external code) tarafından doğrudan manipülasyona veya erişime karşı korunur. Bunun yerine, nesnenin durumuna erişim, genellikle getter ve setter yöntemleri şeklinde iyi tanımlanmış bir arayüz (interface) aracılığıyla sağlanır. Bu, verilerin daha iyi kontrol edilmesine ve doğrulanmasına olanak tanır ve nesnenin dahili durumunun tutarlı kalmasını sağlar.

Typescript kullanarak bir kapsülleme (encapsulation) örneği:

```tsx
class BankAccount {
  private _balance: number;

  constructor(initialBalance: number) {
    this._balance = initialBalance;
  }

  // balance için Getter yöntemi
  public get balance(): number {
    return this._balance;
  }

  // Para yatırma yöntemi
  public deposit(amount: number): void {
    if (amount < 0) {
      console.log("Invalid deposit amount");
      return;
    }
    this._balance += amount;
    return true;
  }

  // Para çekme yöntemi
  public withdraw(amount: number): void {
    if (amount < 0) {
      console.log("Invalid withdrawal amount");
      return;
    }
    if (this._balance - amount < 0) {
      console.log("Insufficient funds");
      return;
    }
    this._balance -= amount;
    return true;
  }
}

const myAccount = new BankAccount(1000);
myAccount.deposit(500);
myAccount.withdraw(200);

console.log("Current balance:", myAccount.balance);
```

Bu örnekte, BankAccount sınıfı \_balance veri özniteliğini kapsüller (encapsulate) ve bununla etkileşim için yöntemler sağlar (deposit, withdraw ve balance için bir getter).
\_balance özniteliği (attribute) private olarak işaretlenerek doğrudan sınıf dışından erişilememesi veya değiştirilememesi sağlanır. Bunun yerine sınıf, nesnenin durumuyla etkileşimde bulunmak için kullanılabilecek public yöntemleri aracılığıyla iyi tanımlanmış bir arayüz (interface) sağlar.

Deposit ve withdraw yöntemleri (methods) ayrıca nesnenin dahili durumunun (internal state) tutarlı kalmasını sağlamak için bazı temel doğrulamaları da zorunlu kılar (örneğin, negatif tutarlara veya mevcut bakiyeyi aşan para çekme işlemlerine izin vermemek gibi). Bu, veri bütünlüğünün korunmasına yardımcı olduğu ve kodu daha sağlam hale getirdiği için kapsülleme (encapsulation) işlemine bir örnektir.
<br/>

---

<br/>

## Date sınıfı örneği

Date sınıfı, zaman içinde tek bir anı temsil eden, tarih ve saat bilgilerini oluşturmak, işlemek ve almak için çeşitli yöntemler sağlayan yerleşik bir nesnedir. Date sınıfı, temel zaman damgasını (yani, Unix döneminden bu yana geçen milisaniye sayısını) kapsüller: 1 Ocak 1970, 00:00:00 UTC) ve onunla etkileşim için bir dizi genel yöntem sunar.

Date sınıfını nasıl kullanabileceğinize dair bir örnek:

```tsx
const now = new Date();
console.log("Current date and time:", now.toString());

const specificDate = new Date("2023-10-01T00:00:00");
console.log("Specific date:", specificDate.toString());

console.log("Current year:", now.getFullYear());
console.log("Current month (0-based):", now.getMonth());
console.log("Current date:", now.getDate());

now.setFullYear(2024);
console.log("Modified date:", now.toString());
```

Bu örnekte, iki Date nesnesi oluşturuyoruz: geçerli tarih ve saati temsil eden now ve belirli bir tarih ve saati temsil eden specificDate. Date sınıfı, iç durumuna (internal state) erişmek ve bu durumu değiştirmek için getFullYear, getMonth, getDate ve setFullYear gibi çeşitli getter ve setter yöntemleri sağlar. Bu yöntemler, kapsüllenmiş zaman damgası (timestamp) ile etkileşim kurmak için bir arayüz (interface) görevi görür.

Perde arkasında, Date sınıfı private bir özellik (property) olarak saklanan zaman damgasını (timestamp) kapsüller. Bu özelliğe sınıf dışından doğrudan erişilemez veya değiştirilemez. Bunun yerine, sınıf kapsüllenmiş veriyi değiştirmek için getter ve setter yöntemleri sağlar. Bu, dahili uygulama detaylarını gizlediği ve tarih ve saat bilgileriyle çalışmak için iyi tanımlanmış bir arayüz (interface) sağladığı için bir kapsülleme (encapsulation) örneğidir.

JavaScript'in private veya public gibi açık (explicit) erişim değiştiricileri (access modifiers) olmadığını belirtmek gerekir. Kapsülleme (Encapsulation), dil tarafından katı bir şekilde uygulanmak yerine, kurallar ve kapanışlar aracılığıyla gerçekleştirilir. Bununla birlikte, Date sınıfı hala kapsülleme ilkelerine bağlı kalarak dahili durumun (internal state) iyi tanımlanmış bir dizi yöntem aracılığıyla korunmasını ve manipüle edilmesini sağlar.
<br/>

---

<br/>

## NestJS ile Typescript'te Kapsülleme

Kapsülleme sadece verileri gizlemek veya private hale getirmek değildir. İlgili veri ve davranışları tek bir birimde toplamak ve bu verilerle etkileşim için net arayüzler (interfaces) tanımlamakla ilgilidir.

Nesne Yönelimli Programlamanın (OOP) temel ilkelerinden biri kapsüllemedir. Kapsülleme, verilerin ve bu veriler üzerinde çalışan yöntemlerin tek bir birimde toplanması ve bu verilere erişimin kontrol edilmesi anlamına gelir. Bu kavram, bakımı yapılabilir, ölçeklenebilir yazılımlar oluşturmak için temeldir.
<br/>

### Neden NestJS?

NestJS, verimli, ölçeklenebilir Node.js web uygulamaları oluşturmak için bir çerçevedir. Modern JavaScript veya TypeScript kullanır ve OOP (Nesne Yönelimli Programlama), FP (Fonksiyonel Programlama) ve FRP (Fonksiyonel Reaktif Programlama) unsurlarını birleştirir. NestJS, geliştiricilerin son derece test edilebilir, ölçeklenebilir, gevşek bir şekilde bağlanmış (loosely coupled) ve kolayca bakımı yapılabilen uygulamalar oluşturmasına olanak tanıyan kullanıma hazır bir uygulama mimarisi (application architecture) sağlar.

NestJS ile ilgili en iyi şeylerden biri, TypeScript'in güçlü yazım (strong typing) ve dekoratörler (decorators) gibi gelişmiş özelliklerinden tam olarak yararlanmasıdır. NestJS, her biri belirli işlevleri kapsülleyebilen modüller, hizmetler ve kontrolcüler kavramı etrafında inşa edilmiştir.
<br/>

### NestJS'de Kapsülleme

NestJS'de kapsülleme, hizmetlerin ve denetleyicilerin nasıl oluşturulduğu ve kullanıldığı konusunda gözlemlenir. NestJS'deki hizmetler iş mantığını, kontrolörler ise istek işleme mantığını kapsüllemek içindir.
<br/>

#### Hizmetlerde (Services) Kapsülleme

NestJS'deki hizmetler genellikle iş mantığınızın yaşadığı yerlerdir. Üzerinde çalıştıkları yöntemleri ve verileri kapsüllerler. İşte kullanıcıları yöneten bir hizmet (service) örneği

```tsx
import { Injectable } from "@nestjs/common";

@Injectable()
export class UsersService {
  private readonly users: Array<{ id: number; name: string }> = [
    { id: 1, name: "John Doe" },
  ];

  findAll(): Array<{ id: number; name: string }> {
    return this.users;
  }

  findOne(id: number): { id: number; name: string } | undefined {
    return this.users.find((user) => user.id === id);
  }
}
```

UsersService'de, verileri (users dizisi) ve bu veriler üzerinde çalışan yöntemleri (findAll, findOne) kapsüllüyoruz. Bu servis HTTP veya veritabanları hakkında hiçbir şey bilmez; sadece kullanıcıları yönetmekle ilgilenir. Veriler (bu durumda users dizisi) gizli tutulur ve yalnızca hizmet tarafından sağlanan yöntemler aracılığıyla erişilebilir ve değiştirilebilir. Bu, kapsülleme işlemidir.
<br/>

#### Kontrolörlerde (Controllers) Kapsülleme

NestJS'deki kontrolörler gelen HTTP isteklerini işler ve yanıtları döndürür. İstek işleme mantığını (request handling logic) kapsüllerler. İşte kullanıcılar için HTTP isteklerini yöneten bir kontrolör (controller) örneği:

```tsx
import { Controller, Get, Param } from "@nestjs/common";
import { UsersService } from "./users.service";

@Controller("users")
export class UsersController {
  constructor(private usersService: UsersService) {}

  @Get()
  findAll(): Array<{ id: number; name: string }> {
    return this.usersService.findAll();
  }

  @Get(":id")
  findOne(@Param("id") id: string): { id: number; name: string } | undefined {
    return this.usersService.findOne(id);
  }
}
```

UsersController'da, HTTP istek işleme mantığını kapsüllüyoruz. findAll yöntemi '/users' URL'sine yönelik GET isteklerini, findOne yöntemi ise '/users/:id' URL'sine yönelik GET isteklerini ele alır. Bu kontrolör, veriler veya verilerin nasıl depolandığı hakkında hiçbir şey bilmez; yalnızca HTTP isteklerini ve yanıtlarını işlemekle ilgilenir.

---

— Taner Çeker tarafından hazırlanmıştır.
