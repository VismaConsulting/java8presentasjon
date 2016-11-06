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

1. Eksempler på hvordan gjøre det med for-løkker, deretter hvordan gjøre det med streams
2. Deep-dive
3. ...

---

# Innhold

```javascript
function makeIterator(array){
    var nextIndex = 0;
    
    return {
       next: function(){
           return nextIndex < array.length ?
               {value: array[nextIndex++], done: false} :
               {done: true};
       }
    }
}
```

---
class: contrast-page, left, middle

# Title
## Subtitle

---
class: values-page
