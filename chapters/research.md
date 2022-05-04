## Research

### Wat is Rust?

#### Intro

- [ ] history
- [x] Rust high level uitleggen
- [ ] ...

[comment]: # "TODO: parafraseren"

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

Merk op dat `println!` geen functie is maar een _macro_. Geïnspireerd door de functionele programmeertaal **Scheme**, zijn
macros een manier van code schrijven dat andere code schrijft, wat bekend staat als _metaprogramming_. Metaprogramming is
handig voor het verminderen van code dat u zelf hoeft to schrijven en onderhouden, wat ook een van de rollen is van functies.
Toch verschillen macros met functies. Zo kunnen macros een variabel aantal parameters hebben en worden ze uitgebreid vooraleer
de compiler de betekenis van de code interpreteert.
[[2]](https://doc.rust-lang.org/reference/influences.html)[[3]](https://doc.rust-lang.org/book/ch19-06-macros.html)

Een _struct_ [[4]](https://doc.rust-lang.org/book/ch05-01-defining-structs.html#defining-and-instantiating-structs)
in Rust is gelijkaardig als een `Object` in object georienteerde programmeertalen.
Het wordt gebruikt om samenhorende waarden te groeperen en optioneel kan men _associated functions_
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

- Elke waarde in Rust heeft een variabel dat zijn _owner_ wordt genoemd
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
Wat Rust uniek maakt is het _Ownership_ systeem dat geheugenveiligheid kan garanderen zonder een garbage collector
nodig te hebben. Hiervoor gebruikt Rust een lijst van regels dat bepaald hoe een Rust programma zijn geheugen beheert
tijdens het uitvoeren:

- Elke waarde in Rust heeft een variabel dat zijn _owner_ wordt genoemd
- Er kan maar een owner teglijk zijn
- Wanneer een owner buiten zijn scope gaat, zal de waarde wegvallen

Alle programma's moeten de manier beheren waarop ze het geheugen van een computer gebruiken tijdens het draaien

Het meest unieke eigenschap van Rust is hoe het geheugen veiligheid garandeerd.
Rust maakt gebruik van een _Ownership_ model dat geheugen veiligheid garandeerd zonder

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
hetzelfde zijn.

Dit zal een praktische kijk zijn met een voorbeeld Todo applicatie op hoe we Yew kunnen gebruiken
voor het bouwen van web-applicaties.

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

Om te verifieren dat het Rust environment juist is opgezet, voer je het initiele project uit met de cargo build tool.
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

`main.rs`

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
  <body></body>
</html>
```

#### Start de development server

Voer het volgende commando uit om de applicatie te builden en lokaal te draaien.

```sh
trunk serve --open
```

Trunk zal nu je applicatie openen in je standaard browser, luisteren naar veranderingen en behulpzaam je
applicatie herbouwen als je source bestanden aanpast.

### Statische pagina

#### Bouwen van HTML

Yew maakt gebruik van de procedurele macro's van Rust en biedt ons een syntax die lijkt op JSX
(een uitbreiding van JavaScript waarmee u HTML-achtige code kunt schrijven in JavaScript) om de opmaak te maken.

#### Converteren van html naar Rust

Aangezien we al een vrij goed idee hebben van hoe onze website eruit zal zien,
kunnen we onze mentale opzet eenvoudig vertalen naar een voorstelling die compatibel is met `html!`.
Als je eenvoudige HTML kunt schrijven, moet het geen probleem zijn om markeringen in `html!` te schrijven.
Het is belangrijk op te merken dat de macro op een paar punten verschilt van HTML:

- Uitdrukkingen moeten tussen accolades staan (`{ }`)
- Er mag maar één root node zijn. Als je meerdere elementen wilt hebben zonder ze in een container te wikkelen,
  wordt een lege tag/fragment (`<> ... </>`) gebruikt
- Elementen moeten goed worden afgesloten.

We willen een layout bouwen die er ongeveer zo uitziet in ruwe HTML:

```html
<main>
  <h1>My todo list</h1>
  <ul>
    <li>
      <input type="checkbox" />
      <label>Take dog out for a walk</label>
    </li>
    <input type="checkbox" />
    <label>Feed the cats</label>
    <li>
      <input type="checkbox" />
      <label>Take out the trash</label>
    </li>
    <li>
      <input type="checkbox" />
      <label>Water plants</label>
    </li>
  </ul>
</main>
```

Laten we nu deze HTML in `html!` omzetten. Type (of kopieer/plak) het volgende knipsel in de body van de app functie,
zodat de waarde van html! wordt geretourneerd door de functie

`app.rs`

```rust
#[function_component]
pub fn App() -> Html {
    html! {
        <main>
            <h1>{ "My todo list" }</h1>
            <ul>
                <li>
                    <input type="checkbox"/>
                    <label> { "Take dog out for a walk" } </label>
                </li>
                    <input type="checkbox"/>
                    <label> { "Feed the cats" } </label>
                <li>
                    <input type="checkbox"/>
                    <label> { "Take out the trash" } </label>
                </li>
                <li>
                    <input type="checkbox"/>
                    <label> { "Water plants" } </label>
                </li>
            </ul>
        </main>
    }
}
```

#### Components

Components zijn de bouwstenen van Yew applicaties. Door components te combineren, die weer uit andere components
kunnen worden opgebouwd, bouwen we onze applicatie. Door onze components te structureren voor herbruikbaarheid en
ze generiek te houden, kunnen we ze in meerdere delen van onze applicatie gebruiken zonder code of logica te hoeven dupliceren.

In feite is de `app` functie die we tot nu toe hebben gebruikt een component, genaamd `App`. Het is een "function component".
Er zijn twee verschillende soorten componenten in Yew.

1. Struct Components
2. Function Components

In deze tutorial zullen we function components gebruiken.

Laten we nu onze `App` component opsplitsen in kleinere componenten. We kunnen onze Todo lijst opspliten in
2 components genaamd `Task` en `TaskList`.

`task.rs`

```Rust
#[derive(Properties, Debug, PartialEq)]
pub struct TaskProps {
    pub id: String,
    pub title: String,
    pub completed: bool,
}

#[function_component]
pub fn Task(
    TaskProps {
        id,
        title,
        completed,
    }: &TaskProps,
) -> Html {
    html! {
        <li>
            <input
                type="checkbox"
                id={id.clone()}
                checked={*completed}
            />
            <label
                for={id.clone()}>{title.clone()}
            </label>
        </li>
    }
}
```

Let op de parameters van onze Task function component. Een function component heeft slechts
één argument dat zijn "props" (kort voor "properties") definieert. Props worden gebruikt om gegevens
door te geven van een ouder component naar een kind component. In dit geval is TaskProps een struct die de props definieert.

`task_list.rs`

```rust
#[derive(Properties, PartialEq)]
pub struct TaskListProps {
    pub children: Children,
}

#[function_component]
pub fn TaskList(TaskListProps { children }: &TaskListProps) -> Html {
    html! {
        <ul>
            { for children.iter() }
        </ul>
    }
}
```

Nu kunnen we onze `App` component updaten met onze nieuwe components `Task` & `TaskList`.

`app.rs`

```rust
#[function_component]
pub fn App() -> Html {
    let tasks = vec![
        html! { <Task id={"1"} title={"Take dog out for a walk"} completed={true} /> },
        html! { <Task id={"2"} title={"Feed the cats"} completed={false} /> },
        html! { <Task id={"3"} title={"Water the plants"} completed={false} /> },
    ];

    html! {
        <main>
            <h1>{ "My todo list" }</h1>
            <TaskList>
                {tasks}
            </TaskList>
        </main>
    }
}
```

#### Interactief

Momenteel doet onze applicatie niet veel anders dan onze voor gedefineerde lijst te tonen.
Uiteindlijk willen we onze taken uit de todo lijst kunnen schrappen. Om deze interactie te laten werken
zullen we een aantal zaken aanpassen.

Om bij te houden of de gebruiker de taak geschrapt heeft al dan niet, zullen we een `completed_state` gebruiken
met de `use_state` hook. Zo verliezen we niet de waarde van de variabele `completed_state` mocht het component re-renderen.

```rust
#[function_component]
pub fn Task(
    ...
) -> Html {
    let completed_state = use_state(|| *completed);
    ...
}
```

Het volgende is natuurlijk het `onclick` event afhandelen als de gebruiker op het label of input element klikt.
Hiervoor hebben we een `Callback` functie nodig die onze `completed_state` aanpast naargelang de vorige state.
Voor we de `completed_state` kunnen gebruiken in onze `Callback` closure functie moeten we die eerst clonen.
De reden hiervoor is het keyword `move` die voor de closure parameters staat, `move` zorgt ervoor dat alle references
die gebruikt worden in de closure scope hun waarden worden verplaatst binnen de scope. Dus om te voorkomen dat we onze
`completed_state` nergens meer kunenn gebruiken clonen we eerst de state.

Daarnaast kunnen we ook een css class meegeven met de `classes!` macro van yew,
die conditioneel het html label zal doorstrepen al dan niet.

`task.rs`

```rust
#[function_component]
pub fn Task(
    TaskProps {
        id,
        title,
        completed,
    }: &TaskProps,
) -> Html {
    let completed_state = use_state(|| *completed);

    let onclick = {
        let completed_state = completed_state.clone();

        Callback::from(move |_| {
            if *completed_state {
                completed_state.set(false);
            } else {
                completed_state.set(true);
            }
        })
    };

    let completed_class = {
        if *completed_state {
            "line-through"
        } else {
            ""
        }
    };

    html! {
        <li>
            <input
                {onclick}
                type="checkbox"
                id={id.clone()}
                checked={*completed_state}
            />
            <label
                class={classes!(completed_class)}
                for={id.clone()}>{title.clone()}
            </label>
        </li>
    }
}
```

#### Data extern ophalen

In de speed typing applicatie komen de code snippets van een API in plaats van hard gecodeerd te zijn in de front-end.
Laten we onze todo lijst ophalen van een externe bron. Hiervoor moeten we de volgende crates toevoegen:

- `reqwasm` voor het maken van de fetch call.
- `serde` met derive functies Voor het de-serialiseren van het JSON antwoord
- `wasm-bindgen-futures` voor het uitvoeren van Rust Future als een Promise

Laten we de afhankelijkheden in het `Cargo.toml` bestand bijwerken:

```toml
[dependencies]
yew = { git = "https://github.com/yewstack/yew/", features = ["csr"] }
serde = { version = "1.0", features = ["derive"] }
wasm-bindgen-futures = "0.4"
```

Pas de `TaskProps` struct aan om de Deserialize trait af te leiden.

```rust
#[derive(Properties, Debug, PartialEq, Deserialize)]
pub struct TaskProps {
    pub id: String,
    pub title: String,
    pub completed: bool,
}
```

Als laatste stap moeten we onze `App` component updaten om de fetch request te maken in plaats van
hardcoded data te gebruiken.

`app.rs`

```rust
#[function_component]
pub fn App() -> Html {
    let tasks = use_state(std::vec::Vec::new);

    {
        let tasks = tasks.clone();
        use_effect_with_deps(move |_| {
            wasm_bindgen_futures::spawn_local(async move {
                let fetched_tasks: Vec<TaskProps> = Request::get("https://jsonplaceholder.typicode.com/todos")
                    .send()
                    .await
                    .unwrap()
                    .json()
                    .await
                    .unwrap();

                tasks.set(fetched_tasks.iter().take(10).map(|props| {
                    html! { <Task id={props.id.clone()} title={props.title.clone()} completed={props.completed} /> }
                }).collect()
                );
            });
            || ()
        }, ());
    }

    html! {
        <main>
            <h1>{ "My todo list" }</h1>
            <TaskList>
                { (*tasks).clone() }
            </TaskList>
        </main>
    }
}

```

Hier gebruiken we de `use_effect_with_deps` hook met lege dependencies als tweede parameter
om de tasks slechts eenmaal op te halen bij de eerste render van het `App` component. In de closure
gebruiken we `wasm-bindgen-futures` om de Javascript Promise die de `Request::get` genereert om te zetten
naar een `Future` type. Met de `Request::get` halen we de JSON todos op en slaan ze op als een `vec` met `TaskProps`.
Vervolgens vullen we onze `tasks` state met de `fetched_tasks` en zullen de tasks worden weergeven in de browser!

## Hoe bouw je een API in Rust?

Volgend op de Todo applicatie die we gebouwd hebben in "Hoe bouw je een Web applicatie in Rust?", zullen we een
REST API bouwen die de taken uit een database zal halen & opslaan. Als API framework zullen we Actix-web gebruiken,
samen met diesel.rs als ORM voor het beheren van de database. Om het simpel te houden gebruiken we net zoals in de
speed typing test applicatie SQLite als database.

### Opzet van het project

Maak een nieuw Rust project aan met de volgende dependencies.

```sh
cargo new api
cd api/
```

`Cargo.toml`

```toml
[dependencies]
diesel = { version = "1.4.8", features = ["sqlite", "r2d2"] }
dotenv = "0.15.0"
actix-web = "4"
actix-cors = "0.6.1"
uuid = { version = "0.8", features = ["serde", "v4"] }
serde = { version = "1.0", features = ["derive"] }
serde_json = "1.0"
log = "0.4"
env_logger = "0.9.0"
```

We zullen uitleggen waarom we deze dependencies nodig hebben als we verder gaan.

#### Database

Diesel biedt een aparte CLI tool om je project te helpen beheren. Omdat het een standalone
binary is, en geen directe invloed heeft op de code van je project, voegen we het niet toe aan
Cargo.toml. In plaats daarvan installeren we het gewoon op ons systeem.

```
cargo install diesel_cli --no-default-features --features sqlite
```

We moeten Diesel vertellen waar ze onze database kan vinden. Dit doen we door de `DATABASE_URL`
environment variabele in te stellen. Op onze development machines zullen we waarschijnlijk meerdere
projecten hebben lopen, en we willen ons environment niet vervuilen. We kunnen de url in plaats daarvan
in een .env bestand zetten. In ons geval is dit de bestandsnaam van de SQLite database.

```sh
echo DATABASE_URL=todo.db > .env
```

Nu kan Diesel CLI alles voor ons opzetten.

```
diesel setup
```

Dit zal onze database aanmaken (als die nog niet bestond), en een lege migrations directory aanmaken
die we kunnen gebruiken om ons schema te beheren.

Diesel support momenteel alleen een database-first aanpak. Hierbij maken we eerst het database schema
om dan met migrations het schema naar Rust om te zetten. Dat gezegd zijnde, laat ons een eerste
migration aanmaken.

```
diesel migration generate create_tasks
```

Diesel CLI zal twee lege bestanden (`up.sql` en `down.sql`) voor ons aanmaken in de vereiste structuur.
In deze bestanden schrijven we SQL voor de `Task` tabel aan te maken in `up.sql` en als we de migration
willen ongedaan maken in `down.sql`.

`up.sql`

```sql
CREATE TABLE tasks (
  id VARCHAR NOT NULL PRIMARY KEY,
  title VARCHAR NOT NULL,
  completed INTEGER NOT NULL DEFAULT 0
)
```

`down.sql`

```sql
DROP TABLE tasks
```

Nu kunnen we onze eerste migration uitvoeren met:

```
diesel migration run
```

Dit zal onze SQL migration uitvoeren op de `todo.db` database en het nodige Rust schema genereren met de
nodige types. In het Rust schema wordt met de `table!` macro een hoop code gegeneerd gebaseerd op het
database schema om alle tabellen en kolommen weer te geven. Zo kunnen we nu gebruik maken van Rust
zijn krachtig typesysteem om volledige SQL queries te gaan bouwen met code. We zullen in het volgende
voorbeeld zien hoe we dat precies kunnen gebruiken.

Telkens wanneer we een migratie uitvoeren of terugdraaien, wordt dit bestand automatisch bijgewerkt.

`schema.rs`

```rust
table! {
    tasks (id) {
        id -> Text,
        title -> Text,
        completed -> Integer,
    }
}
```

### Opzet API

Om de basis functionaliteiten van onze Todo applicatie in de front-end te ondersteunen, zal onze
API een nieuwe taak kunnen aanmaken en de lijst met taken ophalen. Dus zullen we de volgende
endpoints hebben:

- `GET /tasks` - retourneert alle taken
- `POST /tasks` - voegt een nieuwe taak toe

Om onze code overzichtelijklijk te houden, zullen we de volgende structuur hanteren:

`src/`

- `main.rs`
- `models.r`
- `schema.rs`
- `handlers.rs`
- `db.rs`

Bij het opzetten van ons project heeft cargo een al een `main.rs` bestand aangemaakt. Laten we dat bewerken
en onze eerste "Hello World!" route schrijven.

`main.rs`

```rust
use actix_web::{web, App, HttpServer};

#[actix_web::main]
async fn main() -> std::io::Result<()> {
    HttpServer::new(|| {
        App::new()
            .route("/hello", web::get().to(|| async { "Hello World!" }))
    })
    .bind(("127.0.0.1", 5000))?
    .run()
    .await
}
```

Onze main functie heeft nu het `#[actix_web::main]` attribuut, die zal onze `main` functie markeren als start functie
en uitvoeren in de runtime van `actix_web`.

Een belangrijk punt om op te merken is dat we een `Result` type teruggeven.
Dit stelt ons in staat om de `?` operator in `main` te gebruiken, die elke fout die door de geassocieerde functie
wordt teruggegeven naar de aanroeper koppelt.

Het tweede ding om op te merken is `async/await`. Hiermee geven we aan dat Rust onze functies asynchroon kan
uitvoeren zonder andere threads te blokkeren.

In onze `main`, instantiëren we een `HttpServer`, voegen er een `App` aan toe die dient als een Application factory
en voegen onze eerste route er aan toe.

Als alles goed gaat zou je nu de API kunnen opstarten met `cargo run` en bij een GET request naar `localhost:8080/hello`
`Hello world!` als repons te zien krijgen.

`handlers.rs`

```rust
// dependencies

#[get("/task")]
async fn get_tasks() -> Result<HttpResponse, Error> {
  todo!()
}

#[post("/task")]
async fn add_task() -> Result<HttpResponse, Error> {
  todo!()
}
```

In de module `handlers` zullen we onze requests per endpoint afhandelen.
Voorlopig gebruiken we hier nog de `todo!` macro sinds we nog geen communicatie
maken de database. Laat ons dat eerst aanpakken.

Onze eerste migration die we eerder hebben uitgevoerd heeft voor ons al een `schema.rs` module aangemaakt, zodat
diesel onze queries kan controleren tijdens het compileren. Om met queries te kunnen werken in Rust hebben we models
nodig. Zo kunnen we het resultaat van een query mappen naar een model of een model gebruiken voor nieuwe data in te voegen.

Met de traits `Queryable` en `Insertable` zorgen we er voor dat de struct `Task` als resultaat voor een query kan gebruikt
worden en als `struct` om nieuwe data in te voegen.

`Deserialize` en `Serialize` komen van de crate `serde`, zij zorgen ervoor dat we de models kunnen omzetten naar json
en andersom.

`models.rs`

```rust
use serde::{Deserialize, Serialize};

use crate::schema::tasks;

#[derive(Debug, Serialize, Deserialize, Queryable, Insertable)]
pub struct Task {
    pub id: String,
    pub title: String,
    pub completed: bool,
}

#[derive(Debug, Serialize, Deserialize)]
pub struct InputTask {
    pub title: String,
}
```

Nu we onze models hebben kunnen we in `db` functies schrijven om tasks op te vragen en aan te maken.
De functies spreken voorzich, we gebruiken diesel zijn sql implementaties om met onze database te communiceren.

Merk op dat we bij elke functie `schema::tasks::dsl::*` opnieuw toevoegen aan de lokale scope. Dit is puur
conventie sinds we maar 1 tabel hebben `Tasks`, moesten we meerdere tabellen hebben zouden we onze
scope kunnen vervuilen door bijvoorbeeld zelfde kolomnamen die elkaar overschrijven.

`db.rs`

```rust
use diesel::prelude::*;
use uuid::Uuid;

use crate::models::Task;

type DbError = Box<dyn std::error::Error + Send + Sync>;

pub fn list_all_tasks(conn: &SqliteConnection) -> Result<Option<Vec<Task>>, DbError> {
    use crate::schema::tasks::dsl::*;

    Ok(tasks.load::<Task>(conn).optional()?)
}

pub fn insert_new_task(t: &str, conn: &SqliteConnection) -> Result<Task, DbError> {
    use crate::schema::tasks::dsl::*;

    let new_task = Task {
        id: Uuid::new_v4().to_string(),
        title: t.to_owned(),
        completed: false,
    };

    diesel::insert_into(tasks).values(&new_task).execute(conn)?;

    Ok(new_task)
}
```

Nu we onze helper functies geschreven hebben kunnen we de requests afhandelen in `handlers` als volgt:

Elke handler functie krijgt een connection pool als parameter, die we later zullen definieren in `main`.
De connection pool zal verschillende connecties met de database openhouden zodat ze efficient kunnen hergebruikt
worden door anderen. Om te voorkomen dat een andere thread de connectie gebruikt tijdens het uitvoeren van een `db`
functie blokkeren we deze thread met `web::block`. Als alles goed verloopt geven we de resultaten terug, indien niet
geven we een `InternalServerError` terug.

`handlers`

```rust
use actix_web::{web, get, post, HttpResponse, Error};

use crate::{DbPool, db, models};

#[get("/task")]
async fn get_tasks(
    pool: web::Data<DbPool>,
) -> Result<HttpResponse, Error> {
    let tasks = web::block(move || {
        let conn = pool.get()?;
        db::list_all_tasks(&conn)
    })
    .await?
    .map_err(actix_web::error::ErrorInternalServerError)?;

    if let Some(tasks) = tasks {
        Ok(HttpResponse::Ok().json(tasks))
    } else {
        let res = HttpResponse::NotFound().body("No tasks found!".to_string());
        Ok(res)
    }
}

#[post("/task")]
async fn add_task(
    pool: web::Data<DbPool>,
    form: web::Json<models::InputTask>,
) -> Result<HttpResponse, Error> {
    let task = web::block(move || {
        let conn = pool.get()?;
        db::insert_new_task(&form.title, &conn)
    })
    .await?
    .map_err(actix_web::error::ErrorInternalServerError)?;

    Ok(HttpResponse::Created().json(task))
}
```

Wat ons nu nog rest te doen, is onze connection pool instantiëren en de handler functies
linken aan onze `App`. Vooraleer dat we dat doen laden we eerst ons `.env` bestand in het
enviroment met de `dotenv` crate en loggen we `info` over de applicatie naar `stdout` met
`env_logger`. Daarna kunnen we onze connection pool opzetten met de `DATABASE_URL` uit het
enviroment. Ten slotte voegen we onze hanlder functies toe aan een nieuwe `service` met als
scope `/api` zodat al onze routes worden ge prefixed met `/api`.

`main.rs`

```rust
// dependencies

type DbPool = r2d2::Pool<ConnectionManager<SqliteConnection>>;

#[actix_web::main]
async fn main() -> std::io::Result<()> {
    dotenv::dotenv().ok();

    env_logger::init_from_env(env_logger::Env::new().default_filter_or("info"));

    let server_port = if let Ok(port) = std::env::var("PORT") {
        port.parse::<u16>().expect("Could not convert PORT env to string!")
    } else {
        5000
    };

    // set up database connection pool
    let conn_spec = std::env::var("DATABASE_URL").expect("DATABASE_URL");
    let manager = ConnectionManager::<SqliteConnection>::new(conn_spec);
    let pool = r2d2::Pool::builder()
        .build(manager)
        .expect("Failed to create pool.");


    log::info!("{}", format!("starting HTTP server at http://localhost:{server_port}"));

    // Start HTTP server
    HttpServer::new(move || {
        App::new()
            .app_data(web::Data::new(pool.clone()))
            .wrap(middleware::Logger::default())
            .service(
                web::scope("/api")
                .service(get_tasks)
                .service(add_task)
            )
        })
    .bind(("127.0.0.1", server_port))?
    .run()
    .await
}
```

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

wat ging er niet goed geen tijd voor error, handling, authentication, complexere database, etc..
