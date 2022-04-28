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

- [ ] Stack 
- [ ] Heap
- [ ] Ownership
- [ ] Borrowing
- [ ] Lifetimes

##### Stack
Een stack is een deel van het computergeheugen met een die tijdelijke variabelen opslaat
Een stack is een datastructuur voor de opslag van een wisselend aantal elementen, waarvoor geldt dat, net als
bij een gewone stapel, het element dat het laatst werd teogevoegd, het eerst weer wordt opgehaald. Dit principe
wordt ook wel LIFO (Last in First Out) genoemd.

##### Heap
Een heap is een abstracte datastructuur 

stack sneller

heap trager

met ownership hoef niet zo vaak meer over de stack en heap na te denken

String wordt opgeslagen op de heap sinds we de grootte niet kennen voor het compileren


ownership rules
- Elke waarde in Rust heeft een variabel dat zijn *owner* wordt genoemd
- Er kan maar een owner teglijk zijn
- Wanneer een owner buiten zijn scope gaat, zal de waarde wegvallen

```rust
{
    let s = String::from("hello"); // s is valid from this point forward

    // do stuff with s
}                                  // this scope is now over, and s is no
                                   // longer valid
```

##### Ownership
Ownership is een set van regels die bepalen hoe een Rust programma omgaat met geheugen. 
Als een van de regels overtreden wordt zal het programma niet compileren.

##### Lifetimes

##### Borrowing

Rust is ontworpen om geheugenveilig te zijn. Het staat geen null pointers, dangling pointers, of data races toe. Waarden
kunnen alleen geinitialiseerd worden door middel een vaste set van 
Wat Rust uniek maakt is het *Ownership* systeem dat geheugenveiligheid kan garanderen zonder een garbage collector
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

- [ ] history
- [ ] wat is het?
- [ ] hoe werkt het?
- [ ] waarvoor wordt het gebruikt?
  - [ ] wasmer
  - [ ] wasi

#### bronnen
-
-
-


## Welke front- & backend frameworks zijn er ter beschikking?

Om efficient web applicaties te bouwen heb je natuurlijk een goed framework nodig die voor jou al 
het zware werk doet. Gelukkig heeft Rust mits zijn jonge jaren, al een aardig aantal frameworks
ter beschikking voor het bouwen van web applicaties. Dit zijn de top 3 front- en backend frameworks. 
Gerankschikt naar mate van hun popularitiet.


### Front-end 

#### yew - 21k
**Yew** is momenteel het populairste front-end framework met over 21k github stars. Het is een 
component gebaseerd framework vergelijkbaar met React en Elm, met support voor multi-threading, 
component gebaseerde patronen. Het ondersteunt JavaScript-interoperabiliteit, waardoor 
ontwikkelaars NPM packages kunnen gebruiken en integreren met bestaande JavaScript applicaties.

#### dixous - 3.4k
**Dioxus** is een UI library die elegant is ontworpen om React-achtig te zijn - het is 
gebouwd rond een virtuele DOM ter ondersteuning van het bouwen van platformonafhankelijke apps 
voor web, mobiel en desktop. Het biedt ondersteuning voor op componenten gebaseerde architectuur, 
concurrency en async, props, een ingebouwde foutafhandelaar, state management en meer.

#### seed - 3.2k
**Seed** is een frontend-framework voor het maken van prestatiegerichte en betrouwbare web-apps 
die ook een Elm-achtige architectuur heeft. Het heeft een minimale configuratie en boilerplate,
en heeft duidelijke documentatie die het voor iedereen gemakkelijk maakt om mee te beginnen.

### Back-end

#### actix-web
Actix heeft een architectonisch patroon gebaseerd op Rust's acteurssysteem en is goed uitgerust 
voor het bouwen van schrijfservices en micro-apps. Het heeft ondersteuning voor routering, 
middleware, testen, WebSockets, databasea en automatisch herladen van de server, en kan worden 
gehost op NGINX. Actix kan worden gebruikt om volledige web-app en API te bouwen.

#### warp
#### axum

Reden dat ik Yew gekozen heb is github stars, popularitiet en eigenlijk excate clone van React.
- populariteit -> meer packages
- community +
- functional components 
- hooks


bronnen:
- [The current state of Rust web frameworks](https://blog.logrocket.com/current-state-rust-web-frameworks/) 
- [Are we web yet](https://www.arewewebyet.org/)

## Hoe bouw je een Web applicatie in Rust?

Sinds **Yew** het populairste framework is en ook gebruikt is als framework voor het bouwen van de 
speed typing applicatie, zal de vraag "Hoe bouw je een Web applicatie in Rust" beantwoord worden
met Yew als framework. Het bouwen van een web applicatie in een ander framework zal in grote lijnen
hetzelfde zijn. Dit zal een praktische kijk zijn op hoe we Yew kunnen gebruiken voor het bouwen van Web
applicaties.


### Tools installeren
NOTE: de installatie handleiding is geschreven voor UNIX systemen.

Om een web applicatie te bouwen in **Yew** heb je een aantal tools nodig voor het builden, packagen
en debuggen van jouw Yew applicatie.

#### Rust
Om Rust te installeren hebben we de `rustup` toolchain installer nodig. Met het onderstaand script 
kan je het installeren op jouw UNIX machine. Als je Rust al hebt staan maak dan zeker dat je de 
laatste versie hebt door `rustup update` uit te voeren.
```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

#### WebAssembly
Rust kan source codes compileren voor verschillende "targets" (m.a.w verschillende processors).
Het compilatie target voor een browser gebaseerd WebAssembly heet `wasm32-unkown-unkown`. Het
volgende commando zal het WebAssembly target toevoegen aan je development environment.

```sh
rustup target add wasm32-unknown-unknown
```

#### Trunk
De documentatie van Yew raad aan om **Trunk** te gebruiken voor het beheren van deployment en packaging.

```sh
cargo install --locked trunk
```

Nu ons development enviroment opgezet is, kunnen we een nieuw cargo project aanmaken.

```sh
cargo new yew-app
cd yew-app
```

Om te verifieren dat het Rust environment juist is opgezet, voer je het initiele project uit  met de cargo build tool.
Na de output van de het build process, zou je normaal "Hello, world!" te zien krijgen.
```sh
cargo run
```

#### Statische pagina

Om deze simpele command line applicatie naar een basis Yew web applicatie te convertern, zijn er een paar 
aanpassingen nodig. Pas de volgende bestanden aan als volgt:

`Cargo.toml`
```toml
[package]
name = "yew-app"
version = "0.1.0"
edition = "2021"

[dependencies]
yew = "0.19"
```

`src/main.rs`
```rust
use yew::prelude::*;

#[function_component(App)]
fn app() -> Html {
    html! {
        <h1>{ "Hello World" }</h1>
    }
}

fn main() {
    yew::start_app::<App>();
}
```

Maak nu een `index.html` aan in de root folder van het project.

`index.html`
```html
<!DOCTYPE html>
<html lang="en">
    <head> </head>
    <body> </body>
</html>
```

#### Start de development server

Voer het volgende commando uit om de applicatie te builden en lokaal te draaien.
```sh
trunk serve --open
```

Trunk zal nu je applicatie openen in je standaard browser, luisteren naar veranderingen en behulpzaam je 
applicatie herbouwen als je source bestanden aanpast. 

## Hoe bouw je een API in Rust?

- Bouwen van HTML
- Components
  - Interactief
  - State hanlden
Fetching data


## Is Rust klaar voor productie?

#### performance vergelijken met ander propulaire frameworks

- kan DOM niet direct aanspreken
- wordt al in miroservices gebruikt
- WebAssembly wordt ook al in productie gebruikt
- maar om een volledige web applicatie in Rust applicatie te bouwen heeft het nog wat nadelen
- pros 
- cons

#### Slot
- stack overflows meest geliefde taal
- waar wordt het momenteel gebruikt?
  - discord, AWS
- voor wie is Rust?

De programmeertaal is al 5 jaar op een rij als "meest geliefde programmeertaal" verkozen in de Stack 
Overflow Developer Survey. Wat maakt Rust zo geliefd bij programmeurs? Laat ons eens

