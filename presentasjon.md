class: first-page, right, middle

# Title
## Subtitle

---

# Agenda

1. Introduction
2. Deep-dive
3. ...
---

# Introduction

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
