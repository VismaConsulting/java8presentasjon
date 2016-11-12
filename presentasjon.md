class: first-page, right, middle

# Funksjonell programmering
# i Java 8
## PGR-200

???

Hei, alle sammen, og takk for at vi fikk lov til å komme å snakke om Java 8, og
funksjonell programmering for dere.

---
class: contrast-page, middle

# Hvem er vi?

???

Dere lurer kanskje på hvem vi er?

---

class: leo

# Leo-Andreas Ervik

* Visma Consulting
* Konsulent hos NAV
* Gikk ut av Westerdals i år

???

Jeg heter Leo, og var akkurat som dere for bare noen få måneder siden.
Nå er jeg på den andre siden...

---
class: andersemil, right
# Anders Emil Salvesen

* Visma Consulting
* Konsulent hos Skatteetaten
* Gikk ut fra NTNU i 2012

???

... og jeg heter Anders Emil. Jeg har jobbet som konsulent i 
Visma Consulting siden jeg gikk ut fra NTNU i 2012.

Til daglig er jeg på prosjekt hos Skatteetaten, der jeg jobber med modernisering
av skatteberegning. Der lager jeg de programmene som: 

* Lager og sender deg skattetrekksmelding (skattekort)
* Regner ut det som står nederst på selvangivelsen din.
* Regner ut skatteoppgjøret som man får fra juni og utover.

Selv om jeg jobber med dette, må jeg dessverre betale skatt som alle andre :/

Jeg er også fagsjef i Visma Consulting. Det vil si at jeg har ansvaret for den faglige
utviklingen som foregår utenfor prosjekt. Det er ganske viktig for en konsulentbedrift
å hele tiden ha ansatte med oppdatert kunnskap. Derfor har vi mange faggrupper som
arrangerer fagkvelder hele tiden.

---

class: liten-tekst
# Læringsmål

Emnet gir også en smakebit på funksjonell programmering som et alternativt programmerings-paradigme til objekt-orientert programmering. 
I den anledning vil det være naturlig å se hvordan også Java SE, fra versjon 8, inneholder funksjonelle elementer.

Kunnskaper – kandidaten skal 
* kjenne til forskjeller i objekt-orientert og funksjonell programmering
* vite når det kan være fornuftig å benytte Lambda Expressions i Java
* kjenne til streams-APIet, og når det er hensiktsmessig å benytte dette

Ferdigheter – kandidaten skal kunne
* lese og skrive Java-kode som benytter Lambda expressions med relevante interface fra java.util.function-pakken som Predicate, Supplier, Consumer og Function
* benytte funksjonelle operasjoner på en strøm av elementer, deriblant map-reduce.

---

# Agenda

1. Hva er funksjonell programmering?
2. Eksempler på funksjonell programmering i Java 8
3. Refaktorere til Java 8 i IntelliJ - med innspill fra studentene
4. Hvordan er dette implementert i Java 8? (Default Methods in Interfaces)
5. Spesifikke interfacer: Predicat, Function, Supplier, Consumer
6. Liste opp hva vi har lært
7. Øving

---
class: contrast-page, middle
# Hva er funksjonell programmering?

???

Så hva er funksjonell programmering? 

Er det noen som kan forklare hva det er?

. 
.

Ikke det, nei.

Funksjonell programmering er et paradigme innen programmering, på samme måte
som objektorientert programmering. Det stammer fra en del av matematikken kalt
Lambda Calculus.

De siste årene har funksjonell programmering blitt mer og mer populært, så det
er mange som tror at det er veldig nytt og moderne. Faktisk har det eksistert i over
50 år, hvor Lisp var et av de første språkene med funksjonelle trekk.

---

### Lisp (1958)

```lisp
(DEFUN HELLO ()
  "HELLO WORLD"
)
```

???

**Lisp** er det nest eldste språket som er i bruk i dag (Fortran er eldst).
 Lisp er ikke et fullstendig funksjonelt språk, og har blant annet også elementer
 av prosedyreorientering i seg.

--

### APL (1962)
```apl
'Hello World'
``` 

???

**APL** kom i 1962.

--

### Haskell (1987)

```haskell
 main = do putStrLn "Hello, world."
 ```

???

**Haskell** kom i 1987, og var et forsøk på å lage en åpen standard for forskning på
funksjonell programmering. Haskell regnes som et fullt funksjonelt språk.

De siste årene har det kommet flere språk med funksjonelle elementer på JVM-plattformen. 
Disse kompilerer altså til Java-bytecode, og kan kjøres av alle som har Java installert.

---

### Javascript (1995)

```javascript
alert("Hello World!")
```

???

**JavaScript** ble laget på 10 dager i 1995, og er i dag veldig populært. JavaScript
har en del elementer av funksjonalisme i seg, men kan ikke kalles et helt funksjonelt
språk.

--

### Scala (2001)

```scala
object HelloWorld {
  def main(args: Array[String]): Unit = {
    println("Hello, world!")
  }
}
```

???

Det mest populære av disse, er nok **Scala**, som kom i første versjon i 2001. 
Det er både et objektorientert og funksjonelt språk.

--

### Clojure (2007)

```clojure
(println "Hello world!")
```

???

Hvis man vil ha et fullstendig funksjonelt språk som fortsatt kjører på JVM, gå for
**Clojure**. Det er en variant av Lisp, og ble startet i 2007. Clojure er en favoritt
blant hipsterne i JVM-miljøet, og brukes på flere prosjekter rundt omkring.

---
# Begreper i funksjonell programmering

???

Hva er det som gjør et språk funksjonelt, da? Har dere noen forslag?

Det er noen egenskaper som gjør et språk mer eller mindre funksjonelt.
De viktigste av disse egenskapene er:

--

* First-class functions

???

**Førsteklasses funksjoner**, som betyr at funksjoner kan brukes på samme måte som variabler.
Man kan sende inn en funksjon som et parameter til en annen funksjon, og den funksjonen kan
igjen returnere en funksjon.

En funksjon som tar inn eller returnerer en funksjon, kalles en **higher-order function**.

--
* Immutable Values

???

Når en variabel er **immutable**, ikke-muterbar, betyr det at den ikke kan forandres. Verdien settes én
gang, og hvis du vil endre den siden, er du shit out of luck, og må heller nøye deg med å
lage en ny variabel av samme typen med en annen verdi.

Dette gjør det mye lettere å vite hva som foregår i en klasse, siden den kun blir instansiert 
ett sted.

--
* Pure functions

???

**Pure functions**, eller rene funksjoner, betyr at outputen fra funksjonen kun er avhengig av inputen,
og at det ikke er noen sideeffekter. I objektorientert programmering har man 
mange urene funksjoner, siden man aksesserer feltene til klassen. Siden funksjoner i Java
ofte modifiserer staten til klassen, kalles de egentlig metoder, ikke funksjoner.

Konseptet om rene funksjoner går hånd-i-hanske med immutable verdier.

--
* Anonyme funksjoner (lambda)

???

Et annet viktig konsept er **anonyme funksjoner**, også kalt **lambda-funksjoner**. Det er
en av tingene som har kommet til Java i versjon 8, og er sammen med det vi kaller streams
noe av det viktigste.

---

# FP vs OO

???

Hva er forskjellen mellom funksjonell og objekt-orientert programmering?

* Scala er både objekt-orientert og funksjonelt
* Java 8 har funksjonelle elementer
* Forskjellen er hvordan du bruker verktøyene du har til rådighet.

I rene funksjonelle språk går det ikke an å programmere objekt-orientert. Det
er ikke mulig å ha side-effekter, alle verdier er ikke-muterbare, 
og du komponerer programmene dine ved hjelp av lambda-funksjoner i mye større grad.

Det går også an å programmere funksjonelt i objekt-orienterte språk, men du må holde 
tunga rett i munnen. Vi kan vise det med eksempler fra god gammeldags Java.

--

```java
class IkkeFunksjonellPerson {
    private int alder;
    private String navn;
    
    public IkkeFunksjonellPerson(int alder, String navn) {
        this.alder = alder;
        this.navn = navn;
    }
    
    public void setAlder(int alder) {
        this.alder = alder;
    }
    
    //osv
}
```

???

Det er ikke veldig funksjonelt hvis du gjør det mulig å mutere verdiene i en klasse.
Her gjør `setAlder` klassen om til en muterbar klasse. `setAlder` foretar en side-effekt,
så den er ikke en `pure-function`.

---

# FP vs OO


```java
class FunksjonellPerson {
    private final int alder;
    private final String navn;
    
    public FunksjonellPerson(int alder, String navn) {
        this.alder = alder;
        this.navn = navn;
    }
    
    public int getAlder(int alder) {
        return alder;
    }
    
    // final, og ingen setter
}
```

???

Det er derimot mer funksjonelt hvis du gjør det på denne måten. Medlemmene av
klassen er `final`, og kan ikke endres etter at de først er satt. Hvis denne personen
fyller år eller gifter seg og derfor bytter navn, må man lage en ny instans.

Og det er mye mer funksjonelt.

Man kan altså velge å gjøre ting mer eller mindre funksjonelt i ikke-funksjonelle språk.
La oss nå se litt nærmere på de nye funksjonelle elementene som er kommet i Java 8.

---

class: contrast-page, middle

# Java 8

???

Med Java 8 ble det introdusert flere av konseptene over. Funksjoner er, eller fremstår
 ihvertfall som førsteklasses medlemmer av språket, disse funksjonene er ofte utformet
 som anonyme funksjoner, og de kan være parametre til andre funksjoner, så de blir altså
 higher-order functions.
 
 Noen ville argumentert for at lambdaene egentlig bare er syntaktisk sukker, men det
 trenger vi ikke å bry oss om.

---

# Programmering

* Lambdaer 
* Streams
* Default methods

---

# Programmering

* Lambdaer .green[&#10004;]
* Streams
* Default methods

---

# Programmering

* Lambdaer .green[&#10004;]
* Streams .green[&#10004;]
* Default methods

---

# Programmering

* Lambdaer .green[.green[&#10004;]]
* Streams .green[&#10004;]
* Default methods .green[&#10004;]

---

## Før Java 8

```java
List<String> biltyper = Arrays.asList("VW", "Audi", "Jaguar");
List<String> biltyperSomBegynnerPaaBokstavenA = new ArrayList<>();

for (String biltype : biltyper) {
    if (biltype.startsWith("A")) {
        biltyperSomBegynnerPaaBokstavenA.add(biltype);
    }
}
```
--
## Etter Java 8

```java
List<String> biltyper = Arrays.asList("VW", "Audi", "Jaguar");
List<String> biltyperSomBegynnerPaaBokstavenA = biltyper.stream()
    .filter(biltype -> biltype.startsWith("a"))
    .collect(Collectors.toList());
```

---

## Før Java 8

```java
List<String> frukter = Arrays.asList("eple", "banan", "pære", "eple");
Map<String, Integer> antallPerFrukt = new HashMap<>();

for (String frukt : frukter) {
    if (!antallPerFrukt.hasKey(frukt)) {
        antallPerFrukt.put(frukt, 0);
    }
    antallPerFrukt.put(frukt, antallPerFrukt.get(frukt)++);
}
```
--
## Etter Java 8

```java
List<String> biltyper = Arrays.asList("VW", "Audi", "Jaguar");
List<String> biltyperSomBegynnerPaaBokstavenA = biltyper.stream()
    .groupingBy(Function.identity(), Collectors.counting());
```

---
class: contrast-page, left, middle

# Title
## Subtitle

---
class: values-page
