class: first-page, right, middle

# Java 8
## PGR-200

---

class: leo

# Leo-Andreas Ervik

* Visma Consulting
* Konsulent hos NAV
* Gikk ut av Westerdals i år

---
class: andersemil, right
# Anders Emil Salvesen

* Visma Consulting
* Konsulent hos Skatteetaten
* Gikk ut fra NTNU i 2012

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

0. Hvem er vi, hvor kommer vi fra, hva gjør vi til vanlig osv
1. Hva er funksjonell programmering? (Historietime)
2. Eksempler på funksjonell programmering i Java 8 - på slides
3. Refaktorere til Java 8 i IntelliJ - med innspill fra studentene
4. Hvordan er dette implementert i Java 8? (Default Methods in Interfaces)
5. Spesifikke interfacer: Predicat, Function, Supplier, Consumer
6. Liste opp hva vi har lært
7. Øving

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
