## Research

### Wat is Rust?

#### Intro

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

Hier een simpel voorbeeld dat "Hello World!" schrijft naar de standaard output.
Merk op dat `println!` geen functie is maar een *macro*. Geïnspireerd door de functionele programmeertaal **Scheme**, zijn
macros een manier van code schrijven dat andere code schrijft, wat bekend staat als *metaprogramming*. 
[[3]](https://doc.rust-lang.org/reference/influences.html)[[4]](https://doc.rust-lang.org/book/ch19-06-macros.html)

```rust
fn main() {
    println!("Hello, World!");
}
```

[comment]: # (TODO: dit klopt niet)

Voor programmeurs die zich niet herkennen in programmeertalen zoals **C++**, **Haskell** en **OCaml** lijkt Rust
een aparte syntax te hebben in tegenstelling tot conventionele talen. 
[[2]](https://doc.rust-lang.org/reference/influences.html) 

```rust
fn factorial(i: u64) -> u64 {
    match i {
        0 => 1,
        n => n * factorial(n-1)
    }
}
```
Rust heeft geen null pointers [[5]](https://doc.rust-lang.org/std/option/#options-and-pointers-nullable-pointers) 
tenzij men een null pointer wilt dereferentieren (dan moet die in een onveilig blok worden geplaatst).
Als alternatief voor `null` maakt Rust gebruik van een `Option` type waarmee gekeken kan worden of een pointer 
wel `Some` of geen `None` waarde bevat. Dit kan afgehandeld worden door syntactische sugar, zoals de `if let`
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

#### Geheugen

Wat Rust uniek maakt is het *Ownership* systeem dat geheugen veiligheid kan garanderen zonder een garbage collector
nodig te hebben. Hiervoor gebruikt Rust een lijst van regels dat bepaald hoe een Rust programma zijn geheugen beheert 
tijdens het uitvoeren: 
- Elke waarde in Rust heeft een variabel dat zijn *owner* wordt genoemd
- Er kan maar een owner teglijk zijn
- Wanneer een owner buiten zijn scope gaat, zal de waarde wegvallen


Alle programma's moeten de manier beheren waarop ze het geheugen van een computer gebruiken tijdens het draaien

Het meest unieke eigenschap van Rust is hoe het geheugen veiligheid garandeerd.
Rust maakt gebruik van een *Ownership* model dat geheugen veiligheid garandeerd zonder 

- Ownership
- Borrowing
- Lifetimes


#### Ecosysteem

- packages / modules
- cargo
- crates.io

- correct geen null values
- structs
- match control flow
- functioneel programmeren
  - closures
- marcros



#### Slot
- stack overflows meest geliefde taal
- waar wordt het momenteel gebruikt?
  - discord, AWS
- voor wie is Rust?

De programmeertaal is al 5 jaar op een rij als "meest geliefde programmeertaal" verkozen in de Stack 
Overflow Developer Survey. Wat maakt Rust zo geliefd bij programmeurs? Laat ons eens

## Wat is WebAssembly & hoe werkt het?



## Welke front- & backend frameworks zijn er ter beschikking?

## Hoe bouw je een Web applicatie in Rust?

## Hoe bouw je een API in Rust?

## Is Rust klaar voor productie?
