## Research

### Wat is Rust?

#### Intro

- [ ] history
- [x] Rust high level uitleggen
- [ ] ...

[comment]: # (TODO: parafraseren)

Rust is een gecompileerde multi-paradigma programmeertaal bedacht door Graydon Hoare en is begonnen als 
een project van Mozilla Research. Geïnspireerd door de programmeertalen **C** en **C++**, maar kent 
weinig syntactische en semantische gelijkenissen tegenover deze talen. Rust focust zich met
name op snelheid, veiligheid, betrouwbaarheid en productiviteit. Dit wordt gerealiseerd door gebruik te 
maken van een krachtig typesysteem en een borrow checker. Hiermee kan Rust een hoog niveau van 
geheugenveiligheid garanderen zonder een garbage collector nodig te hebben.

Rust beoogt moderne computersystemen efficiënter te benutten. Hiervoor maakt het onder meer gebruik van 
geheugenbeheer dat geheugen in een blok toewijst en daarnaast strikt toeziet op de stacktoewijzing. 
Hierdoor kunnen problemen zoals stackoverflows, bufferoverflows en niet-geïnitialiseerd geheugen voorkomen 
worden. Verder staat Rust ook geen null-pointers, dangling-pointers of data-races toe in veilige code. 
 [[1]](https://nl.wikipedia.org/wiki/Rust_(programmeertaal))


#### Syntax

- [x] marcros
- [x] match control flow
- [x] correct geen null values
- [x] structs
- [ ] traits
- [ ] attributes

Voor velen die zich niet herkennen in programmeertalen zoals **C++**, **Haskell** of **OCaml** lijkt Rust
een aparte syntax te hebben in tegenstelling tot conventionele talen. Laat ons even kijken naar een paar 
syntactische voorbeelden in Rust. [[2]](https://doc.rust-lang.org/reference/influences.html) Hier een 
simpel voorbeeld dat "Hello World!" schrijft naar de standaard output.

```rust
fn main() {
    println!("Hello, World!");
}
```
Merk op dat `println!` geen functie is maar een *macro*. Geïnspireerd door de functionele programmeertaal **Scheme**, zijn
macros een manier van code schrijven dat andere code schrijft, wat bekend staat als *metaprogramming*. Metaprogramming is 
handig voor het verminderen van code dat u zelf hoeft to schrijven en onderhouden, wat ook een van de rollen is van functies.
Toch verschillen macros met functies. Zo kunnen macros een variabel aantal parameters hebben en worden ze uitgebreid vooraleer 
de compiler de betekenis van de code interpreteert.
[[2]](https://doc.rust-lang.org/reference/influences.html)[[3]](https://doc.rust-lang.org/book/ch19-06-macros.html)

Een *struct* [[4]](https://doc.rust-lang.org/book/ch05-01-defining-structs.html#defining-and-instantiating-structs) 
in Rust is gelijkaardig als een `Object` in object georienteerde programmeertalen.
Het wordt gebruikt om samenhorende waarden te groeperen en optioneel kan men *associated functions*
implementeren. Associated functions die geen `self` als hun eerste parameter hebben zijn geen methodes 
en kunnen gebruikt worden als constructors die een nieuwe instantie retourneren van de struct.

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn square(size: u32) -> Rectangle {
        Rectangle {
            width: size,
            height: size,
        }
    }

    fn area(&self) -> u32 {
        self.width * self.height
    }
}

fn main() {
    let rect1 = Rectangle::square(4);

    println!(
        "The area of the rectangle is {} square pixels.",
        rect1.area()
    );
}
```

Rust heeft geen null pointers [[5]](https://doc.rust-lang.org/std/option/#options-and-pointers-nullable-pointers) 
tenzij men een null pointer wilt dereferentieren (dan moet die in een `unsafe` blok worden geplaatst).
Als alternatief voor `null` maakt Rust gebruik van een `Option` type waarmee gekeken kan worden of een pointer 
wel `Some` of geen `None` waarde bevat. Dit kan afgehandeld worden door syntactische sugar, zoals het `if let`
statement om toegang te krijgen tot thet innerlijke type, in dit geval een string:
```rust
fn main() {
    let name: Option<String> = None;
    // If name was not None, it would print here.
    if let Some(name) = name {
        println!("{}", name);
    }
}
```

Naast de `if` en `else` controle structuren is er ook `match` en `if let`. `match` is vergelijkbaar met een `switch` statement
uit andere talen. Het neemt een waarde en test het tegen een serie van patronen. Op basis van welk patroon er overeen komt 
wordt de code uitgevoerd. Patronen kunnen opgemaakt worden uit waarden, variabel namen, wildcards, en veel meer. De power van
`match` komt van het feit dat de compiler zal bevestigen bij het compileren dat alle mogelijke gevallen zijn afgehandeld. 
Soms wil je niet alle gevallen expliciet afhandelen en wil je slechts een patroon afhandelen terwijl je de rest negeert. 
In dat geval kan je `if let` gebruiken, wat minder boilerplate code is dan `match`.
[[4]](https://doc.rust-lang.org/book/ch06-02-match.html)[[5]](https://doc.rust-lang.org/book/ch06-03-if-let.html)
```rust
let message = match maybe_digit {
    Some(x) if x < 10 => process_digit(x),
    Some(x) => process_other(x),
    None => panic!(),
};

let config_max = Some(3u8);
if let Some(max) = config_max {
    println!("The maximum is configured to be {}", max);
}
```




#### Geheugen

- [ ] Ownership
- [ ] Borrowing
- [ ] Lifetimes

Wat Rust uniek maakt is het *Ownership* systeem dat geheugen veiligheid kan garanderen zonder een garbage collector
nodig te hebben. Hiervoor gebruikt Rust een lijst van regels dat bepaald hoe een Rust programma zijn geheugen beheert 
tijdens het uitvoeren: 
- Elke waarde in Rust heeft een variabel dat zijn *owner* wordt genoemd
- Er kan maar een owner teglijk zijn
- Wanneer een owner buiten zijn scope gaat, zal de waarde wegvallen


Alle programma's moeten de manier beheren waarop ze het geheugen van een computer gebruiken tijdens het draaien

Het meest unieke eigenschap van Rust is hoe het geheugen veiligheid garandeerd.
Rust maakt gebruik van een *Ownership* model dat geheugen veiligheid garandeerd zonder 


#### Ecosysteem

- [ ] packages / modules
- [ ] cargo
- [ ] crates.io


## Wat is WebAssembly & hoe werkt het?

## Welke front- & backend frameworks zijn er ter beschikking?

## Hoe bouw je een Web applicatie in Rust?

## Hoe bouw je een API in Rust?

## Is Rust klaar voor productie?

#### Slot
- stack overflows meest geliefde taal
- waar wordt het momenteel gebruikt?
  - discord, AWS
- voor wie is Rust?

De programmeertaal is al 5 jaar op een rij als "meest geliefde programmeertaal" verkozen in de Stack 
Overflow Developer Survey. Wat maakt Rust zo geliefd bij programmeurs? Laat ons eens

