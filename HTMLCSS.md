<!--
author: Gruppe A – HTML & CSS Lorenz Haase, Samuel Rietdorf, Daniel Stiehler
language: de
version: 1.0.0
comment: Kurs über HTML, CSS und die Verbindung zu regulären Sprachen
import: https://raw.githubusercontent.com/liaTemplates/WebDev/master/README.md
import: https://raw.githubusercontent.com/liaTemplates/skulpt/master/README.md
import: https://raw.githubusercontent.com/LiaScript/CodeRunner/master/README.md
-->


# Reguläre Sprachen & HTML & CSS

# 📐 Kapitel 1 – Reguläre Sprachen

### 1.1 Formale Sprachen – Grundbegriffe

**Alphabet**: Endliche Menge von Zeichen, aus denen Wörter gebildet werden.
*Beispiel: A-Z, 0-9*

**Wort**: Endliche Folge von Zeichen aus einem Alphabet.
*Beispiel: "Hallo"*

**Formale Sprache**: Menge von Wörtern, die nach bestimmten Regeln gebildet werden.
*Beispiel: Alle gültigen E-Mail-Adressen*

**Syntax**: Regeln, die beschreiben, wie gültige Wörter strukturiert sind.
*Beispiel: `<h1>Text</h1>` in HTML*

**Semantik**: Bedeutung oder Auswirkung eines syntaktisch korrekten Wortes.
*Beispiel: `<h1>` wird als Überschrift angezeigt*

### 1.2 Reguläre Ausdrücke – Syntax
||||
| __Metazeichen__ | __Bedeutung__ | __Beispiel__ |
| `.` | Ein beliebiges Zeichen | `a.c` passt auf "abc", "aXc" |
| `*` | 0 bis beliebig oft | `ab*c` passt auf "ac", "abc", "abbc" |
| `+` | Mindestens 1 Mal | `ab+c` passt auf "abc", "abbc" |
| `?` | Optional (0 oder 1 Mal) | `ab?c` passt auf "ac", "abc" |
| `{n}` | Genau n Mal | `a{3}b` passt auf "aaab" |
| `{n,m}` | n bis m Mal | `a{2,4}b` passt auf "aab", "aaab", "aaaab" |
| `[abc]` | Eines der Zeichen | `[aeiou]` passt auf Vokale |
| `[^abc]` | Nicht diese Zeichen | `[^0-9]` passt auf Nicht-Ziffern |
| `^` | Anfang der Zeile | `^Hello` passt nur am Anfang |
| `$` | Ende der Zeile | `world$` passt nur am Ende |
| `\d` | Ziffer (0-9) | `\d{3}` passt auf "123" |
| `\w` | Wortzeichen | `\w+` passt auf "Hello_123" |
| `\s` | Whitespace | `a\sb` passt auf "a b" |
| `\|` | Oder | `cat\|dog` passt auf "cat" oder "dog" |
| `(...)` | Gruppe | `(ab)+` passt auf "ab", "abab" |

### 1.3 Reguläre Ausdrücke – Semantik
{{0}}
**Beispiel 1: Postleitzahl** <br>
Muster: `^\d{5}$` <br>
Passt auf: "88888", "00000", "33333" <br>
Passt NICHT auf: "1111", "444444", "aaaaa", "22322" 


{{1}}
**Beispiel 2: E-Mail** <br>
Muster: `^[\w.+]@[\w.+]\.[\w+]$` <br>
Passt auf: "max@example.com", "user.name@domain.co.uk" <br> 
Passt NICHT auf: "max@.com", "maxatexample.com" 


{{2}}
**Beispiel 3: Telefonnummer (DE)** <br>
Muster: `^\+?49\d{3,5}-?\d{3,7}$` <br>
Passt auf: "+493045-83950", "4909-9919" <br> 
Passt NICHT auf: "03041-2345", "+49012967-3985" 


{{3}}
Die **Syntax** beschreibt, wie der Regex geschrieben werden muss. <br> 
Die **Semantik** beschreibt, was er bedeuten bzw. ausführen soll.

--{{0}}--
**Beispiel 1: Postleitzahl** <br>
Muster: `^\d{5}$` <br>
Passt auf: "88888", "00000", "33333" <br>
Passt NICHT auf: "1111", "444444", "aaaaa", "22322" 


--{{1}}--
**Beispiel 2: E-Mail** <br>
Muster: `^[\w.+]@[\w.+]\.[\w+]$` <br>
Passt auf: "max@example.com", "user.name@domain.co.uk" <br>
Passt NICHT auf: "max@.com", "maxatexample.com" 
<!--niemand weiß, warum es nicht umgebrochen wurde, nicht mal die KI Es gibt in so einem *"(§Z( halt immer mal ein paar komische Sachen--> 

--{{2}}--
**Beispiel 3: Telefonnummer (DE)** <br>
Muster: `^\+?49\d{3,5}-?\d{3,7}$` <br>
Passt auf: "+493045-83950", "4909-9919" <br>
Passt NICHT auf: "03041-2345", "+49012967-3985" 


--{{3}}--
Die **Syntax** beschreibt, wie der Regex geschrieben werden muss. <br> 
Die **Semantik** beschreibt, was er bedeuten bzw. ausführen soll.

### 1.4 Anwendungen

**Anwendungsfall 1: Formularvalidierung**

``` python
import re

muster = r"^\d{5}$"
eingabe = input("Gib deine Postleitzahl ein: ")

if re.match(muster, eingabe):
    treffer = "Treffer"
else:
    treffer = "kein Treffer"

print(treffer + " -> " + eingabe)
```
@LIA.python3

Das Muster `^\d{5}$` akzeptiert nur 5 Ziffern. "12345" passt, "1234" nicht.


**Anwendungsfall 2: Dateien filtern**

```python
import re
muster = r"^foto_.*\.(jpg|png)$"
dateien = ["foto_urlaub.jpg", "screenshot.png", "foto_001.png", "bild.gif"]

for datei in dateien:
    if re.match(muster, datei):
        treffer = "Bild"
    else:
        treffer = "Andere Datei"
    print(treffer + " -> " + datei)
```
@LIA.python3

Das Muster findet nur Dateien, die mit "foto_" beginnen und mit ".jpg" oder ".png" enden.

### 1.5 Verbindung zu HTML & CSS


HTML5 erlaubt einfache Eingabeprüfungen über das pattern‑Attribut. Dabei wird ein vereinfachter Regex verwendet: ^ und $ fehlen, \d wird nicht unterstützt.
Ein Muster wie ^\d{5}$ (genau fünf Ziffern) wird in HTML daher als [0-9]{5} geschrieben.

```html
<input type="text" pattern="[0-9]{5}" required>
```

Das Muster ist JavaScript-Regex, funktioniert aber fast identisch wie Python-Regex!

### 1.6 Quiz 1
__1. Was ist die Definition für ein Alphabet?__

[( )] So viele Zeichen wie man will, aus denen Wörter gebildet werden können
[(X)] Endliche Menge von Zeichen, aus denen Wörter gebildet werden.
[( )] Irgendwelche Buchstaben in irgendeiner Anordnung

---

**Frage 2:** Was sind KEINE Beispiele für Formale Sprachen?

- [(X)] Englisch
- [( )] C++
- [( )] Binärsprache

---

**Frage 3:** Was ist Semantik?

- [( )] Wie ein Code geschrieben werden muss
- [(X)] Was ein Code macht
- [( )] 271.000

---

**Frage 4:** Was macht dieser Ausdruck `+` ?

- [( )] Genau ein mal
- [(X)] Mindestens ein mal
- [( )] Mehrmals

---

**Frage 5:** Was macht dieser Ausdruck `$` ?

- [( )] Ka
- [( )] Wie ein Code geschrieben werden muss
- [(X)] Ende der Zeile

---

### 1.7 Quiz 2

**Frage 6:** Was macht dieser Ausdruck `\|` ?

- [( )] Leerzeichen
- [(X)] Oder
- [( )] Gruppe

---

**Frage 7:** Was passt auf diesen Code `^\d{5}$` ?

- [(X)] 12345
- [( )] abhsg
- [( )] 555555

---

**Frage 8:** Was passt auf diesen Code NICHT `^[\w.+]@[\w.+]\.[\w+]+$` ?

- [( )] Big@Bibi.il
- [(X)] Max@Mustermen,com
- [( )] Jeffry@XTrmp.us

---

**Frage 9:** Wer ist der/die beste Infolehrer/in?

- [( )] Frau Hempel
- [( )] Herr Völkel
- [(X)] Herr Engel

# 🌐 Kapitel 2 – HTML
![HTML & CSS Logo](https://www.agenturro.co/wp-content/uploads/2024/03/1_OlyP02fRFe8pEkJgb6vGTQ.png)

### 2.1 Was ist HTML?

HTML (**HyperText Markup Language**) ist die Standardsprache für Webseiten.

- Erstellt die Struktur einer Webseite
- Enthält Texte, Bilder, Links und Überschriften
- Beschreibt den Inhalt einer Seite
- Wird von Webbrowsern gelesen und dargestellt
- Bildet die Grundlage moderner Webseiten

> 💡 HTML ist das Grundgerüst jeder Webseite.

### 2.2 Wozu braucht man eine Auszeichnungssprache für Webseiten?

- Sie strukturiert die Inhalte einer Webseite.
- Sie kennzeichnet verschiedene Elemente wie Überschriften, Texte und Bilder.
- Sie ermöglicht Browsern, Inhalte korrekt darzustellen.
- Sie sorgt für eine einheitliche Darstellung auf verschiedenen Geräten.
- Sie erleichtert die Entwicklung und Pflege von Webseiten.
- Sie bildet die Grundlage für Design (CSS) und Interaktivität (JavaScript).

> 💡 Sie beschreibt, welche Inhalte auf einer Webseite vorhanden sind und wie sie aufgebaut sind.

### 2.3 Grundstruktur eines HTML-Dokuments

Jede HTML-Datei folgt einem festen Grundaufbau.

```html
<!DOCTYPE html>
<html>
<head>
    <title>Meine Webseite</title>
</head>
<body>
    Hallo Welt!
</body>
</html>
```
![HTML-Grundgerüst](https://www.schulhomepage.de/images/webdesign/html-verstaendlich-erklaert.png)

| Element | Bedeutung |
|----------|----------|
| `<!DOCTYPE html>` | Gibt an, dass es sich um ein HTML5-Dokument handelt. |
| `<html>` | Umschließt den gesamten Inhalt der Webseite. |
| `<head>` | Enthält Informationen über die Webseite (Metadaten). |
| `<title>` | Legt den Titel fest, der im Browser-Tab angezeigt wird. |
| `<body>` | Enthält alle sichtbaren Inhalte der Webseite. |

> 💡 Jede HTML-Seite besteht aus einem **Head-Bereich** für Informationen und einem **Body-Bereich** für den sichtbaren Inhalt.


### 2.4 Wichtige HTML-Elemente

HTML bietet viele verschiedene Elemente, mit denen Webseiten strukturiert und gestaltet werden
können. Die folgende Tabelle zeigt einige der wichtigsten HTML-Elemente und ihre Aufgaben.


| Element | Bedeutung |
|----------|------------|
| `<html>` | Legt HTML als Dokumententyp fest |
| `<head>` | Enthält Informationen, die nicht im Browser angezeigt werden |
| `<title>` | Definiert den Titel der Webseite |
| `<base>` | Legt die Basis-URL für relative Links fest |
| `<body>` | Enthält alle sichtbaren Inhalte der Webseite |
| `<h1>`, `<h2>`, `<h3>` ... | Kennzeichnen Überschriften verschiedener Ebenen |
| `<p>` | Markiert einen Absatz bzw. Inhaltsabschnitt |
| `<ul>` | Erstellt eine ungeordnete Liste |
| `<ol>` | Erstellt eine nummerierte Liste |

---
Beispiele:

**HTML-Dokument (`<html>`)**

```html
<html>
...
</html>
```

**Kopfbereich (`<head>`)**

```html
<head>
  <title>Meine Webseite</title>
</head>
```

**Seitentitel (`<title>`)**

```html
<title>Meine Webseite</title>
```

**Basis-URL (`<base>`)**

```html
<base href="https://example.com/">
```

**Seiteninhalt (`<body>`)**

```html
<body>
  <h1>Willkommen!</h1>
</body>
```

**Überschrift (`<h1>`)**

```html
<h1>Meine Webseite</h1>
```

**Absatz (`<p>`)**

```html
<p>Das ist ein Absatz.</p>
```

**Ungeordnete Liste (`<ul>`)**

```html
<ul>
  <li>Punkt 1</li>
  <li>Punkt 2</li>
</ul>
```

**Geordnete Liste (`<ol>`)**

```html
<ol>
  <li>Schritt 1</li>
  <li>Schritt 2</li>
</ol>
```


### 2.5 Formulare und das `pattern`-Attribut

Formulare ermöglichen es Nutzern, Daten auf einer Website einzugeben. Typische Beispiele sind Kontaktformulare, Registrierungen oder Anmeldungen.

Damit Nutzer ihre Daten im richtigen Format eingeben, kann das `pattern`-Attribut verwendet werden. Es überprüft die Eingabe direkt im Browser und verhindert das Absenden des Formulars, wenn die Eingabe nicht dem vorgegebenen Muster entspricht.

<br>

Beispiel:

```html
<form>
    <label for="plz">Postleitzahl:</label>
    <input type="text" id="plz" pattern="[0-9]{5}" required>

    <button type="submit">Absenden</button>
</form>
```

In diesem Beispiel darf nur eine fünfstellige Zahl eingegeben werden. Die Eingaben `12345` oder `08056` sind gültig. Die Eingaben `123`, `ABCDE` oder `12A45` werden hingegen abgelehnt.

<br>


Die wichtigsten Bestandteile:

| Code | Bedeutung |
|--------|-----------|
| `<form>` | Erstellt ein Formular. |
| `<input>` | Erstellt ein Eingabefeld. |
| `type="text"` | Das Feld akzeptiert Texteingaben. |
| `pattern="[0-9]{5}"` | Es sind nur genau fünf Ziffern erlaubt. |
| `required` | Das Feld muss ausgefüllt werden. |

<br>

Das `pattern`-Attribut verwendet sogenannte **reguläre Ausdrücke**. Diese legen fest, welche Zeichen erlaubt sind.

| Ausdruck | Bedeutung |
|-----------|-----------|
| `[0-9]` | Eine beliebige Ziffer von 0 bis 9 |
| `[A-Za-z]` | Ein beliebiger Buchstabe |
| `{5}` | Genau fünf Wiederholungen |
| `{3,10}` | Zwischen drei und zehn Wiederholungen |

<br>


Weitere Beispiele:

```html
<input type="text" pattern="[A-Za-z]{3}">
```

Erlaubt genau drei Buchstaben:

- ABC
- xyz

Nicht erlaubt:

- AB
- ABCD
- A12

<br>

```html
<input type="text" pattern="[0-9]{4}">
```

Erlaubt genau vier Ziffern:

- 2026
- 1999

Nicht erlaubt:

- 26
- 20265

<br>

```html
<input type="text" pattern="[A-Za-z]{3,10}">
```

Erlaubt zwischen drei und zehn Buchstaben:

- Tim
- Alexander

Nicht erlaubt:

- Al
- Maximilian123

<br>

Vollständiges Beispiel:
```html
<form>
    <label for="name">Name:</label>
    <input
        type="text"
        id="name"
        pattern="[A-Za-z]{3,10}"
        required>

    <br><br>

    <label for="plz">Postleitzahl:</label>
    <input
        type="text"
        id="plz"
        pattern="[0-9]{5}"
        required>

    <br><br>

    <button type="submit">Absenden</button>
</form>
```
@WebDev.HTML

> **Merke:** Das `pattern`-Attribut hilft dabei, Eingaben auf ein bestimmtes Format zu beschränken. Dadurch werden fehlerhafte Eingaben bereits vor dem Absenden des Formulars erkannt. Das `pattern`-Attribut nutzt **JavaScript-Regex** – die Syntax ist fast identisch zu Python!
### 2.6 Semantisches HTML

Semantische HTML-Elemente beschreiben die Bedeutung und Funktion eines Bereichs auf einer
Webseite. Dadurch wird der Aufbau einer Seite leichter verständlich – sowohl für Menschen als auch
für Suchmaschinen und Hilfsprogramme.

Schauen wir uns semantisches HTML anhand eines Beispiels an:

Beispiel einer Webseite ohne semantisches HTML:

```html
<div>
<div>Meine Webseite</div>
<div>Willkommen auf meiner Seite!</div>
</div>
```

Beispiel einer Webseite mit semantischem HTML:

```html
<header>
  <h1>Meine Webseite</h1>
</header>

<main>
  <p>Willkommen auf meiner Seite!</p>
</main>
```
Was ist der Unterschied?

Im ersten Beispiel werden nur `<div>`-Elemente verwendet. Diese geben keine Auskunft darüber, welche Funktion die einzelnen Bereiche der Webseite haben.

Im zweiten Beispiel werden semantische Elemente wie `<header>` und `<main>` verwendet. Bereits am Namen des Elements erkennt man, welche Aufgabe der jeweilige Bereich erfüllt.

Dadurch wird der Code:

- leichter lesbar
- einfacher zu warten
- besser von Suchmaschinen verstanden
- zugänglicher für Hilfsprogramme wie Screenreader

Semantisches HTML beschreibt also nicht nur den Inhalt einer Webseite, sondern auch dessen Bedeutung und Funktion.

Vollständiges Beispiel für semantisches HTML:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Meine Webseite</title>
</head>
<body>

  <header>
    <h1>Meine Webseite</h1>
  </header>

  <nav>
    #
    #
    #
  </nav>

  <main>
    <article>
      <h2>Mein erster Beitrag</h2>
      <p>Hallo Welt!</p>
    </article>
  </main>

  <footer>
    <p>© 2026 Meine Webseite</p>
  </footer>

</body>
</html>
```
### 2.7 Zusammenfassung
Zum Abschluss kannst du dein Wissen mit diesem Video noch einmal wiederholen und überprüfen, wie
sicher du die HTML-Grundlagen bereits beherrschst.

!?[Zusammenfassung Html](https://www.youtube.com/watch?v=jEHYBXe3sMU)



### 2.8 HTML – Quiz

---

**Frage 1: Wofür steht HTML?**

- [( )] Hyperlink Text Machine Language  
- [(X)] HyperText Markup Language  
- [( )] Home Tool Markup Language  

---

**Frage 2: Welches Element gehört in den `<head>`‑Bereich?**

- [(X)] `<title>`  
- [( )] `<h1>`  
- [( )] `<p>`  

---

**Frage 3: Welches Element enthält die sichtbaren Inhalte einer Webseite?**

- [( )] `<head>`  
- [(X)] `<body>`  
- [( )] `<meta>`  

---

**Frage 4: Welches Element ist semantisch korrekt für den Hauptinhalt?**

- [( )] `<div>`  
- [(X)] `<main>`  
- [( )] `<section>`  

---

**Frage 5: Welches Attribut wird genutzt, um Eingaben in Formularen zu validieren?**

- [( )] `check`  
- [(X)] `pattern`  
- [( )] `validate`  

---

**Frage 6: Welcher reguläre Ausdruck erlaubt genau fünf Ziffern?**

- [( )] `[0-9]{1,5}`  
- [(X)] `[0-9]{5}`  
- [( )] `[A-Za-z]{5}`  

---

**Frage 7: Welches Element ist semantisch für eine Navigation?**

- [( )] `<menu>`  
- [(X)] `<nav>`  
- [( )] `<navigate>`  

---

**Frage 8: Welches Element beschreibt einen eigenständigen Inhalt wie einen Blog‑Beitrag?**

- [( )] `<section>`  
- [(X)] `<article>`  
- [( )] `<aside>`  

---

**Frage 9: Welches Attribut beschreibt ein Bild für Screenreader?**

- [(X)] `alt`  
- [( )] `title`  
- [( )] `aria-img`  

---

**Frage 10: Welcher Teil eines HTML‑Dokuments enthält Metadaten?**

- [(X)] `<head>`  
- [( )] `<body>`  
- [( )] `<footer>`  

---



# 🌐 Kapitel 2 – CSS

CSS steht für Cascading Style Sheets und ist die Sprache, die das Aussehen von HTML-Elementen bestimmt. Sie legt fest, wie Farben, Abstände, Schriftarten und Layouts auf einer Webseite wirken.



---

__Wie ist CSS entstanden?__

CSS entstand Mitte der 1990er-Jahre, weil HTML immer stärker mit Design-Informationen überladen wurde. 1994 stellte Håkon Wium Lie erstmals die Idee einer Stylesheet-Sprache für das Web vor. Gemeinsam mit Bert Bos entwickelte er das Konzept weiter. 1996 veröffentlichte das W3C CSS Level 1 als offiziellen Standard.



---

__Warum ist CSS heute unverzichtbar?__

- Trennt Inhalt und Gestaltung sauber voneinander
- Ermöglicht responsives Design für alle Bildschirmgrößen
- Erlaubt Animationen und Übergänge ohne JavaScript
- Eine CSS-Datei steuert das Design der gesamten Website



---

__Was ist CSS?__

Durch die Trennung von Struktur (HTML) und Design (CSS) entsteht übersichtlicher, gut wartbarer Code. Eine einzige CSS-Datei kann das Aussehen von hunderten HTML-Seiten gleichzeitig steuern.

```css
/* CSS-Regel: Selektor + Deklarationsblock */
p {
color: #e8eaf6; /* Schriftfarbe */
font-size: 1rem; /* Schriftgröße */
margin-top: 1rem; /* Abstand oben */
}
```



---

__Wie funktioniert CSS?__

Browser lesen HTML von oben nach unten ein und bauen das DOM auf. Anschließend kombinieren sie das DOM mit den CSS-Regeln und erzeugen den Render-Tree, der festlegt, wie jedes Element dargestellt wird. Damit Webseiten überall gleich aussehen, müssen Browser gemeinsame Standards befolgen, die vom W3C festgelegt werden.



---

> 💡 **Hinweis:**
> Das „Cascading" in CSS bedeutet, dass mehrere Regeln auf dasselbe Element zutreffen können. Welche gewinnt, bestimmt die Spezifität und die Reihenfolge im Code.



## Einbindungsmethoden

CSS kann auf drei Arten in HTML eingebunden werden.
Sie unterscheiden sich in Wiederverwendbarkeit, Übersichtlichkeit und Einsatzgebiet.



---

__1. Inline CSS__

CSS direkt im `style`-Attribut eines Elements.
Schnell, aber nicht wiederverwendbar und schwer wartbar.

```html
<p style="color: red; font-size: 1.5rem;">Hallo Welt</p>
```


<p style="color: red; font-size: 1.5rem;">Hallo Welt</p>

> ⚠️ **Hinweis:**
> Inline CSS vermischt Struktur und Design. Nur für schnelle Tests oder
> dynamisch per JavaScript gesetzte Styles verwenden.



---

__2. Internal CSS__

CSS im `<style>`-Block im `<head>` der HTML-Datei.
Styles können auf der Seite wiederverwendet werden, gelten aber nur für diese eine Datei.

```html
<head>
  <style>
    p {
      color: red;
      font-size: 1rem;
    }
  </style>
</head>

```

Gut für kleine Projekte oder einzelne Seiten.
Bei größeren Websites wird es schnell unübersichtlich.



---

__3. External CSS__

CSS in einer separaten `.css`-Datei, die per `<link>` eingebunden wird.
Das ist der Standard im modernen Web.

```html
<!-- Im <head> der HTML-Datei: -->
<link rel="stylesheet" href="style.css">
```

```css
/* In style.css: */
p {
color: red;
font-size: 1rem;
}
```

> ✅ **Empfehlung:**
> External CSS ist die empfohlene Methode: Struktur und Design sind sauber getrennt,
> und eine CSS-Datei kann für beliebig viele HTML-Seiten gelten.



---

__Vergleich__

| Methode | Wiederverwendbar | Mehrere Seiten | Empfehlung |
|----------|-----------------|----------------|-------------------|
| Inline | ✗ | ✗ | Nur für Ausnahmen |
| Internal | ✓ (eine Seite) | ✗ | Kleine Projekte |
| External | ✓ | ✓ | Standard |



### 🧠 Teste dich – Einbindungsmethoden

__1. Welche Einbindungsmethode ist für größere Projekte empfohlen?__

[( )] Inline CSS (style-Attribut)
[( )] Internal CSS (<style> im <head>)
[(x)] External CSS (separate .css-Datei)
[( )] Alle sind gleichwertig

---

__2. Wie bindet man eine externe CSS-Datei namens `style.css` ein?__

[( )] <css src="style.css">
[(x)] <link rel="stylesheet" href="style.css">
[( )] <style href="style.css">
[( )] <import url="style.css">

---

__3. Was ist der Vorteil von External CSS gegenüber Internal CSS?__

[( )] External CSS lädt schneller
[(x)] Eine CSS-Datei kann für mehrere HTML-Seiten gelten
[( )] External CSS unterstützt mehr Eigenschaften
[( )] Internal CSS funktioniert nur in Chrome

---

__4. Welche Einbindungsmethode hat die höchste Spezifität?__

[( )] External CSS
[( )] Internal CSS
[(x)] Inline CSS
[( )] Alle gleich

## Selektoren

Selektoren bestimmen, welche HTML-Elemente von einer CSS-Regel angesprochen werden.

---

__Element-Selektor__

Spricht alle Elemente eines bestimmten Typs an.

```css
p {
  css
}

/* Gilt für alle <p>-Elemente auf der Seite */
```

---

__Klassen-Selektor__

Spricht alle Elemente mit einer bestimmten Klasse an.

Klassen werden mit einem Punkt (`.`) eingeleitet.

Ein Element kann mehrere Klassen haben.

```html
<p class="hinweis">Achtung!</p>
<p class="hinweis">Noch ein Hinweis.</p>
```

```css
.hinweis {
  css
}
```

---

__ID-Selektor__

Spricht ein einzelnes Element mit einer bestimmten ID an.

IDs werden mit einer Raute (`#`) eingeleitet.

Eine ID darf pro Seite nur einmal vorkommen.

```html
<p id="haupttitel">Das ist der Haupttitel.</p>
```

```css
#haupttitel {
  css
}
```

---

__Pseudo-Klassen__

Pseudo-Klassen sprechen Elemente in einem bestimmten Zustand an.

```css
a:hover {
color: white;
}

a:focus {
outline: 2px solid blue;
}

li:first-child {
font-weight: bold;
}

li:nth-child(2) {
color: red;
}
```

---

__Kombinations-Selektoren__

```css
/* Nachfahren-Selektor */
nav a {
color: white;
}

/* Kind-Selektor */
ul > li {
list-style: none;
}

/* Mehrere Selektoren */
h1, h2, h3 {
font-family: 'Inter', sans-serif;
}
```

---

> 💡 Für eine vollständige Referenz:
>
> [Offizielle CSS Dokumentation](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_selectors)

---

### 🧠 Teste dich – Selektoren

__1. Welcher Selektor spricht alle Elemente mit der Klasse `highlight` an?__

[( )] #highlight
[(x)] .highlight
[( )] highlight
[( )] *highlight

---

__2. Was macht der Selektor `nav a`?__

[( )] Spricht nur `<nav>`-Elemente an
[(x)] Spricht alle `<a>`-Elemente an, die sich irgendwo in einem `<nav>` befinden
[( )] Spricht nur direkte Kinder `<a>` von `<nav>` an
[( )] Spricht `<nav>` und `<a>` gleichzeitig an

---

__3. Welche Pseudo-Klasse greift bei Mausbewegung über ein Element?__

[( )] :focus
[( )] :active
[(x)] :hover
[( )] :visited

---

__4. Was macht der Selektor `h1, h2, h3`?__

[( )] Spricht nur h1 an, das h2 und h3 enthält
[(x)] Spricht h1, h2 und h3 gleichzeitig an
[( )] Spricht h3 an, das in h2 ist, das in h1 ist
[( )] Ungültig

## Box-Modell

Im Web wird jedes HTML-Element als rechteckige Box dargestellt.

Das Box-Modell beschreibt, wie diese Box aufgebaut ist und wie viel Platz sie einnimmt.

---

__Aufbau des Box-Modells__

Jede Box besteht von innen nach außen aus vier Schichten:

- Content
- Padding
- Border
- Margin

---

__Padding__

Padding ist der Abstand zwischen dem Inhalt (Content) und der Border.

Er gehört zum Element – Hintergrundfarbe und Klickfläche erstrecken sich über das Padding.

```css
p {
padding: 20px;

padding: 10px 20px;

padding: 5px 10px 15px 20px;

padding-top: 10px;
padding-right: 20px;
padding-bottom: 10px;
padding-left: 20px;
}
```

---

__Border__

Die Border ist der Rahmen um das Element.

Sie besteht aus:

- Dicke
- Stil
- Farbe


border-radius gibt an, wie viel die Ecken abgerundet sind.
```css
p {
border: 2px solid red;
border: 3px dashed blue;
border: 4px dotted green;
border: 6px double purple;

border-width: 2px;
border-style: solid;
border-color: red;

border-bottom: 3px solid #6c63ff;

border-radius: 8px;
}
```

---

__Margin__

Margin ist der Abstand zwischen dem Element und seinen Nachbarn.

Er liegt außerhalb der Border und hat keine Hintergrundfarbe.

```css
p {
margin: 20px;

margin: 10px auto;

margin-top: 2rem;
margin-bottom: 1rem;
}
```

---

__box-sizing__

Standardmäßig wird Padding und Border zur Breite addiert.

Mit `box-sizing: border-box` sind sie bereits enthalten.

```css
*, *::before, *::after {
box-sizing: border-box;
}

.box {
width: 200px;
padding: 20px;
border: 2px solid red;
}
```

---

### 🧠 Teste dich – Box-Modell

__1. Das Box-Modell von innen nach außen:__

Content → [[ Margin | Color | (Padding) ]] → Border → [[ (Margin) | Color | Padding ]]

__2. Ein Element hat `width: 200px`, `padding: 20px` und `border: 5px`. Wie breit ist es mit `box-sizing: content-box`?__

[( )] 200px
[( )] 225px
[(x)] 250px
[( )] 270px

---

__3. Wie zentriert man ein Block-Element horizontal?__

[( )] padding: auto
[(x)] margin: 0 auto
[( )] border: center
[( )] align: center

---

__4. Was ist der Unterschied zwischen `visibility: hidden` und `display: none`?__

[( )] Kein Unterschied
[(x)] visibility: hidden nimmt Platz ein, display: none entfernt das Element
[( )] display: none ist nur für Screenreader
[( )] visibility: hidden entfernt das Element aus dem DOM

## Farben

CSS bietet mehrere Möglichkeiten, Farben anzugeben.
Alle funktionieren mit Eigenschaften wie `color`,
`background-color`, `border-color` und vielen mehr.

---

__Benannte Farben__

CSS kennt vordefinierte Farbnamen. Praktisch für Tests,
aber für präzises Design oft zu ungenau.

```css
p { color: red; }
p { color: steelblue; }
p { color: mediumvioletred; }
p { color: moccasin; }
```

---

__RGB__

Drei Zahlen von 0–255 stehen für Rot, Grün und Blau.
Mit `rgba()` kommt Transparenz dazu (0 = unsichtbar, 1 = sichtbar).

```css
p { color: rgb(30, 144, 255); }
p { color: rgb(50, 205, 50); }
p { color: rgba(108, 99, 255, 0.5); }
```

---

__Hexadezimal__

Sechs Hex-Zeichen (0–9, A–F) für Rot, Grün und Blau.
Optional mit Transparenz: `#RRGGBBAA`.

```css
p { color: #1e90ff; }
p { color: #9400d3; }
p { color: #40e0d0; }
p { color: #ff000080; }
```

---

__HSL__


HSL steht für Farbton, Sättigung und Helligkeit.
Der Farbton ist ein Winkel (0° = Rot, 120° = Grün, 240° = Blau).

![Farbkreis](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/hue/color_wheel.svg)<!-- style="height: 250px" -->
```css
p { color: hsl(210, 100%, 56%); }
p { color: hsl(120, 61%, 50%); }
p { color: hsl(300, 76%, 72%); }
p { color: hsla(210, 100%, 56%, 0.6); }
```

---

__Custom Properties (Variablen)__

Farben einmal definieren und überall verwenden.

```css
:root {
--color-accent: #6c63ff;
--color-text: #e8eaf6;
}

h1 { color: var(--color-accent); }
p { color: var(--color-text); }
```

---

### 🧠 Teste dich – Farben

__1. Welcher Hex-Code ergibt reines Grün?__

[( )] #ff0000
[( )] #0000ff
[(x)] #00ff00
[( )] #ffffff

---

__2. Was bedeuten die Werte in `hsl(120, 100%, 50%)`?__

[( )] Rot, Grün, Blau
[(x)] Farbton, Sättigung, Helligkeit
[( )] Helligkeit, Sättigung, Transparenz
[( )] Farbton, Transparenz, Helligkeit

---

__3. Wie macht man eine Farbe halb transparent mit `rgba()`?__

[( )] rgba(255, 0, 0, 100)
[( )] rgba(255, 0, 0, 50%)
[(x)] rgba(255, 0, 0, 0.5)
[( )] rgba(255, 0, 0, 0)

---

__4. Was ist der Vorteil von CSS-Variablen bei Farben?__

[( )] Sie laden schneller
[(x)] Eine Änderung wirkt sich auf die gesamte Seite aus
[( )] Sie unterstützen mehr Farben
[( )] Sie funktionieren nur in modernen Browsern

## Schriften

Typografie ist einer der stärksten Einflussfaktoren auf Lesbarkeit und Wirkung einer Webseite.
CSS bietet Kontrolle über Schriftart, Größe, Stärke, Zeilenabstand und Ausrichtung.

---

__font-family – Schriftart__

Legt die Schriftart fest. Man verwendet eine Fallback-Kette.

```css
body {
font-family: 'Inter', Arial, sans-serif;
}

p.serif {
font-family: Georgia, 'Times New Roman', serif;
}

code {
font-family: 'Fira Code', 'Consolas', monospace;
}
```

---

__font-size – Schriftgröße__

Bestimmt die Größe des Textes. Unterschiedliche Einheiten haben verschiedene Einsatzbereiche:

| Einheit | Bedeutung | Empfehlung |
|--------|-----------|------------|
| px | Feste Pixel | Für Borders, Icons |
| em | Relativ zum Elternelement | Für Abstände |
| rem | Relativ zur Root-Größe | Für Schriftgrößen |
| % | Relativ zum Elternelement | Für Breiten |
| clamp() | Dynamisch skalierend | Für responsive Texte |

```css
p { font-size: 1rem; }
h1 { font-size: 2rem; }
small { font-size: 0.875rem; }

h1 { font-size: clamp(1.5rem, 4vw, 3rem); }
```

---

__font-weight – Schriftstärke__

Steuert die Dicke der Schrift (100–900).

```css
p { font-weight: 300; }
p { font-weight: 400; }
p { font-weight: 600; }
p { font-weight: 700; }
```

---

__font-style – Kursiv__

```css
p { font-style: normal; }
p { font-style: italic; }
```

---

__line-height – Zeilenabstand__

Einheitenloser Wert wird empfohlen (skaliert automatisch).

```css
p { line-height: 1.0; }
p { line-height: 1.6; }
p { line-height: 2.0; }
```

👉 Für Fließtext: **1.5 – 1.8**

---

__text-align – Textausrichtung__

```css
p { text-align: left; }
p { text-align: center; }
p { text-align: right; }
p { text-align: justify; }
```

---

__Google Fonts – externe Schriften__

Webfonts lassen sich extern einbinden:

```css
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap');

body {
font-family: 'Inter', sans-serif;
}
```
### 🧠 Teste dich – Schriften
??[Spiel zum zuordnen von Begriffen](https://liascripthtmlcss.h5p.com/content/1292923853918130777)


## Flexbox

Flexbox (Flexible Box Layout) ist ein CSS-Layoutmodell, das Elemente in einer
Zeile oder Spalte anordnet, ausrichtet und den verfügbaren Platz verteilt.

> 💡 Hinweis:
> Flexbox wirkt auf zwei Ebenen:
> Container-Eigenschaften steuern das Layout der Kinder,
> Item-Eigenschaften steuern das einzelne Kind-Element.

---

__display: flex – Flexbox aktivieren__

Alles beginnt damit, einem Container `display: flex` zu geben.
Alle direkten Kinder werden automatisch zu Flex-Items und legen sich nebeneinander.

```css
.container {
display: flex;
}
```

---

__flex-direction – Richtung__

Legt die Hauptachse fest: horizontal (`row`) oder vertikal (`column`).

```css
.container { flex-direction: row; }
.container { flex-direction: column; }
.container { flex-direction: row-reverse; }
```

---

__justify-content – Hauptachse__

Verteilt die Items entlang der Hauptachse (bei `row`: horizontal).

```css
.container {
justify-content: flex-start;
justify-content: flex-end;
justify-content: center;
justify-content: space-between;
justify-content: space-evenly;
}
```

---

__align-items – Querachse__

Richtet die Items senkrecht zur Hauptachse aus (bei `row`: vertikal).

```css
.container {
align-items: flex-start;
align-items: center;
align-items: flex-end;
align-items: stretch;
}
```

---

__gap – Abstände__

Setzt den Abstand zwischen allen Items – ohne Margins an jedem einzelnen Element.

```css
.container {
display: flex;
gap: 1rem;
}
```

```css
.container {
gap: 0.5rem 2rem;
}
```

---

__flex-wrap – Umbruch__

Standardmäßig quetscht Flexbox alle Items in eine Zeile.
Mit `flex-wrap: wrap` dürfen Items umbrechen.

```css
.container {
display: flex;
flex-wrap: wrap;
}
```

---

__flex – Wachsen und Schrumpfen__

Die `flex`-Eigenschaft auf einem Item legt fest,
wie viel Platz es im Verhältnis zu anderen Items einnimmt.

```css
.container { display: flex; }

.item-a { flex: 1; }
.item-b { flex: 2; }
.item-c { flex: 1; }
```

---

__Praxisbeispiel: Navigation__

```css
nav {
display: flex;
justify-content: space-between;
align-items: center;
padding: 0 1rem;
}

.nav-logo {
font-weight: 700;
}

.nav-links {
display: flex;
gap: 1.5rem;
}
```

---

### 🧠 Teste dich – Flexbox

__1. Mit welcher Eigenschaft aktiviert man Flexbox auf einem Container?__

[( )] flex: 1
[(x)] display: flex
[( )] position: flex
[( )] layout: flex

---

__2. Welche Eigenschaft richtet Flex-Items entlang der Querachse aus (bei flex-direction: row also vertikal)?__

[( )] justify-content
[( )] flex-wrap
[(x)] align-items
[( )] flex-direction

---

__3. Ein Container hat 3 Items. Item A hat flex: 1, Item B hat flex: 2, Item C hat flex: 1. Wie viel Prozent des Platzes bekommt Item B?__

[( )] 25%
[( )] 33%
[(x)] 50%
[( )] 66%

---

__4. Welcher Wert für justify-content verteilt Items mit gleichem Abstand zwischen ihnen (aber nicht an den Rändern)?__

[( )] space-evenly
[( )] space-around
[(x)] space-between
[( )] center

# Barrierefreiheit

Barrierefreiheit (englisch: *Accessibility*, kurz *a11y*) bedeutet,
dass Webseiten für alle Menschen nutzbar sind – unabhängig von körperlichen
oder kognitiven Einschränkungen. Das betrifft Menschen, die Screenreader benutzen,
nur die Tastatur verwenden, farbenblind sind oder schlecht sehen.

> ⚖️ Hinweis:
> Barrierefreies Web ist in vielen Ländern gesetzlich vorgeschrieben
> und verbessert die Nutzererfahrung für alle.

---

__Alt-Texte für Bilder__

Screenreader können Bilder nicht sehen. Das `alt`-Attribut liefert
eine Textbeschreibung. Bei dekorativen Bildern setzt man `alt=""`.

```html
<!-- Inhaltliches Bild -->
<img src="diagramm.png" alt="Balkendiagramm: Umsatz 2024 nach Quartal">

<!-- Dekoratives Bild -->
<img src="trennlinie.png" alt="">
```

> 💡 Ein guter Alt-Text beschreibt *was* und *warum*.

---

__ARIA-Attribute__

ARIA (*Accessible Rich Internet Applications*) ergänzt HTML um zusätzliche
Informationen für Screenreader.

> ⚠️ Regel:
> Immer zuerst natives HTML verwenden. ARIA nur wenn nötig.

---

___aria-label___

Gibt einem Element einen lesbaren Namen:

```html
<button>✕</button>

<button aria-label="Menü schließen">✕</button>
```

---

___aria-hidden___

Versteckt Inhalte für Screenreader:

```html
<span aria-hidden="true">🎉</span>
<span>Herzlichen Glückwunsch!</span>
```

---

___aria-expanded___

Zustand von aufklappbaren Elementen:

```html
<button aria-expanded="false" aria-controls="nav-menu">
☰ Menü
</button>

<nav id="nav-menu" hidden>
...
</nav>
```

---

___role___

Definiert semantische Rollen:

```html
<nav>...</nav>

<div role="navigation" aria-label="Hauptnavigation">
...
</div>

<div role="alert">
Bitte fülle alle Pflichtfelder aus.
</div>
```

---

___aria-describedby___

Verknüpft Zusatzinformationen:

```html
<label for="passwort">Passwort</label>

<input
id="passwort"
type="password"
aria-describedby="pw-hinweis">

<p id="pw-hinweis">
Mindestens 8 Zeichen, ein Großbuchstabe und eine Zahl.
</p>
```

---

__Kontraste__

Ausreichender Farbkontrast ist entscheidend.

- AA: 4.5 : 1 (Standard)
- AAA: 7 : 1 (hoch)

```css
/* ✗ schlecht */
p {
color: #aaa;
background: #bbb;
}

/* ✓ gut */
p {
color: #e8eaf6;
background: #05071a;
}
```

---

__Tastaturnavigation__

Viele Nutzer verwenden nur die Tastatur.

```css
/* ✗ falsch */
:focus {
outline: none;
}

/* ✓ richtig */
:focus-visible {
outline: 2px solid #6c63ff;
outline-offset: 3px;
}
```

---

__Semantisches HTML__

Gutes HTML ist die Grundlage für Barrierefreiheit.

```html
<!-- ✗ schlecht -->
<div class="nav">...</div>
<div onclick="...">Klick mich</div>
<img src="logo.png">

<!-- ✓ gut -->
<nav>...</nav>
<button>Klick mich</button>
<img src="logo.png" alt="Firmenlogo">
```


### Quiz – Barrierefreiheit

__1. Ein Button enthält nur ein ✕-Icon. Welches Attribut gibt ihm einen lesbaren Namen für Screenreader?__

[( )] aria-hidden="true"
[(x)] aria-label="Schließen"
[( )] title="Schließen"
[( )] role="button"

---

__2. Welches WCAG-Kontrastverhältnis ist der Mindeststandard (Level AA) für normalen Text?__

[( )] 2 : 1
[( )] 3 : 1
[(x)] 4,5 : 1
[( )] 7 : 1

---

__3. Was sollte man bei einem dekorativen Bild als alt-Attribut angeben?__

[( )] alt="dekorativ"
[( )] Das alt-Attribut weglassen
[(x)] alt="" (leerer String)
[( )] alt="Bild"

---

__4. Warum sollte man `:focus { outline: none }` vermeiden?__

[( )] Es macht die Seite langsamer
[(x)] Es entfernt den Fokus-Indikator – Tastaturnutzer sehen nicht mehr, welches Element aktiv ist
[( )] Es funktioniert nicht in allen Browsern
[( )] Es beeinflusst das Box-Modell

# Ausgabeformate

Eine Webseite wird nicht nur im Desktop-Browser angezeigt.
Sie kann auf Smartphones, Tablets, großen Monitoren oder als Druckversion dargestellt werden.

CSS bietet dafür gezielte Mechanismen, um Layout und Darstellung
kontextabhängig zu steuern.

---

__Responsives Design__

Responsives Design bedeutet, dass sich eine Webseite automatisch an unterschiedliche Bildschirmgrößen anpasst – eine Codebasis für alle Geräte.

---

__Das viewport-Meta-Tag__

Ohne dieses Meta-Tag behandeln mobile Browser die Seite wie eine verkleinerte Desktop-Seite.
Das führt zu falschen Skalierungen.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

👉 Wichtig:

- `width=device-width` → nutzt die echte Gerätebreite
- `initial-scale=1.0` → keine automatische Zoom-Anpassung

> 💡 Gehört in jede moderne Webseite!

---

__Media Queries__

Mit `@media` lassen sich CSS-Regeln nur unter bestimmten Bedingungen anwenden –
z. B. abhängig von der Bildschirmbreite.

```css
/* Mobile First: Basis */
.container {
flex-direction: column;
}

/* Tablet */
@media (min-width: 600px) {
.container {
flex-direction: row;
}
}

/* Desktop */
@media (min-width: 1024px) {
.container {
max-width: 1200px;
margin: 0 auto;
}
}
```

👉 Prinzip:

- Erst einfache Styles
- Dann schrittweise erweitern

---

__Mobile First vs. Desktop First__

__✓ Mobile First (empfohlen)__

```css
/* Basis: Mobile */
.box {
width: 100%;
}

/* Erweiterung */
@media (min-width: 600px) {
.box {
width: 50%;
}
}
```

__Desktop First__

```css
/* Basis: Desktop */
.box {
width: 50%;
}

/* Anpassung nach unten */
@media (max-width: 599px) {
.box {
width: 100%;
}
}
```

👉 Unterschied:

- `min-width` → erweitert nach oben (Mobile First)
- `max-width` → überschreibt nach unten (Desktop First)

> ✅ Best Practice: Mobile First

---

__Typische Breakpoints__

- 📱 Mobile: `< 600px`
- 📟 Tablet: `600px – 1024px`
- 🖥️ Desktop: `> 1024px`

👉 Diese Werte sind Richtlinien, keine festen Regeln.

---

__Relative Einheiten__

Feste Pixel reagieren nicht auf Bildschirmgrößen.
Relative Einheiten sind flexibel und responsiv.

```css
/* Prozent */
.box {
width: 80%;
}

/* Viewport */
.hero {
height: 100vh;
}

.banner {
width: 50vw;
}

/* Schriftgröße */
p {
font-size: 1rem;
}

/* Dynamisch */
h1 {
font-size: clamp(1.5rem, 4vw, 3rem);
}
```

👉 Wichtig:

- `vw` / `vh` → abhängig vom Bildschirm
- `rem` → abhängig von der Root-Schriftgröße
- `clamp()` → flexibel mit Grenzen

---

__Druckversion__

Mit `@media print` definierst du Styles speziell für den Druck.

```css
@media print {

body {
background: white;
color: black;
font-size: 12pt;
}

nav,
#sidebar,
button {
display: none;
}

a::after {
content: " (" attr(href) ")";
font-size: 0.8em;
}

h2 {
page-break-after: avoid;
}

pre {
page-break-inside: avoid;
}

}
```

👉 Typische Anpassungen:

- Farben reduzieren
- Navigation ausblenden
- URLs sichtbar machen
- Seitenumbrüche steuern

---

__Weitere @media-Features__

Media Queries können auch auf Systemeinstellungen reagieren.

```css
/* Dark Mode */
@media (prefers-color-scheme: dark) {
body {
background: #111;
color: #eee;
}
}

/* Weniger Animation */
@media (prefers-reduced-motion: reduce) {
* {
transition: none !important;
animation: none !important;
}
}

/* Retina Displays */
@media (min-resolution: 2dppx) {
.logo {
background-image: url('logo@2x.png');
}
}
```

👉 Wichtig:

- verbessert UX und Accessibility
- reagiert auf Nutzerpräferenzen

---

### Quiz – Ausgabeformate

__1. Welches Meta-Tag ist für responsives Design notwendig?__

[( )] `<meta name="mobile" content="yes">`
[(x)] `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
[( )] `<meta name="responsive" content="true">`
[( )] `<meta charset="UTF-8">`

---

__2. Unterschied zwischen `min-width` und `max-width`?__

[( )] Kein Unterschied
[(x)] `min-width` = Mobile First, `max-width` = Desktop First
[( )] `min-width` = Desktop First
[( )] `max-width` = nur Höhe

---

__3. Welche Funktion skaliert zwischen Minimum und Maximum?__

[( )] scale()
[( )] minmax()
[(x)] clamp()
[( )] range()

---

__4. Was macht `prefers-reduced-motion`?__

[( )] Verbessert Performance
[(x)] Reagiert auf reduzierte Animationen im Betriebssystem
[( )] Deaktiviert immer Animationen
[( )] Nur mobil verfügbar

# Quiz – HTML & CSS

**Frage 1**: Welches Element sollte für die Navigation verwendet werden?

- [( )] `<div class="nav">`
- [(X)] `<nav>`
- [( )] `<section>`
---

**Frage 2**: Welches Pattern validiert einen Benutzernamen (3-15 Zeichen)?

- [( )] `pattern="[a-zA-Z0-9]{3-15}"`
- [(X)] `pattern="^[a-zA-Z0-9]{3,15}$"`
- [( )] `pattern="[a-zA-Z0-9]*"`
---

**Frage 3**: Welche CSS-Eigenschaft erzeugt Abstand nach außen?

- [( )] `padding`
- [(X)] `margin`
- [( )] `border`
---



**Frage 4**: Ist das Alt-Attribut wichtig für Suchmaschienenoptimierung?

- [(X)] Ja
- [( )] Nein
---

**Frage 5**: Welche Eigenschaft nutzt Flexbox für Abstände?

- [( )] `margin`
- [( )] `padding`
- [(X)] `gap`
---

**Frage 6**: Welche Media Query ist für Smartphones korrekt?

- [( )] `@media (width: 480px)`
- [(X)] `@media (max-width: 480px)`
- [( )] `@media mobile`
---

**Frage 7**: Welches ARIA-Attribut gibt Screenreadern eine längere Beschreibung?

- [( )] `aria-label`
- [(X)] `aria-describedby`
- [( )] `aria-live`
---

**Frage 8**: Wie verbindet man externe CSS in HTML?

- [( )] `<style src="style.css">`
- [(X)] `<link rel="stylesheet" href="style.css">`
- [( )] `<import href="style.css">`


**Frage 9**: Welches HTML-Element ist semantisch korrekt für den Hauptinhalt?

- [( )] `<section>`
- [(X)] `<main>`
- [( )] `<content>`
---

**Frage 10**: Welche CSS-Eigenschaft ändert die Schriftgröße?

- [( )] `font-weight`
- [(X)] `font-size`
- [( )] `text-style`
---

**Frage 11**: Welches Attribut macht ein Formularfeld verpflichtend?

- [(X)] `required`
- [( )] `mandatory`
- [( )] `force="true"`
---

**Frage 12**: Welche Einheit ist relativ zur Schriftgröße des Elements?

- [( )] `px`
- [(X)] `em`
- [( )] `vh`
---

**Frage 13**: Welcher Selektor wählt alle `<p>`-Elemente innerhalb eines `<div>`?

- [( )] `div + p`
- [(X)] `div p`
- [( )] `div > p`
---

__Lückentext__

Die Farbe Rot schreibt man in CSS als [[red]].  

Hex-Farben beginnen immer mit einem `#` und haben [[6]] Zeichen.  

`rgb(0, 0, 255)` ergibt die Farbe [[Blau]].

---
## 🧩 Anwendungsaufgabe (Kapitel 2)

Erweitere das folgende Startgerüst so, dass:

1. Eine Überschrift **zentriert** dargestellt wird  
2. Ein Absatz mit **blauem Hintergrund** erscheint  
3. Ein Kasten (`div`) mit: 
- eine **Umrandung** die 3px dick, gestrichelt und mit rgb auf grün gesetzt ist
- **Abstand** zur Umrandung von 5px 
- **abgerundeten Ecken** welche einen Radius von 5px haben 

Trage den passenden HTML‑ und CSS‑Code in die Lücken ein.

---

🔧 Startgerüst mit mehrzeiligen Lücken


\<!DOCTYPE html\>  <br>
\<html\>  <br>
\<head\>  <br>
\<title\>Kapitel 2 – CSS Aufgabe\</title\>  <br>
  \<style\>  <br><br>
    h1 {<br>
    [[text-align: center;]]  <br>
    }  <br><br>
    p {<br>
    [[background-color: blue;]]  <br>
    }  <br><br>
    div { <br>
    [[ border: 3px dashed rgb(0, 255, 0); ]]  <br>
    [[ padding: 5px; ]] <br>
    [[ border-radius: 5px; ]] <br>
    }

  \</style\>  <br>
\</head\>  <br>
\<body\>  <br><br>
  [[ <h1> ]] Überschrift [[ </h1>]]  <br><br>
  [[ <p> ]] Ich bin ein Absatz [[ </p> ]]  <br><br>
  [[ <div> ]] Ich bin ein Container [[ </div> ]]  <br><br>
</body>  <br>
</html>
