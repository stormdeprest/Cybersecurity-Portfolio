# JavaScript Essentials Cheat Sheet

**Variables:**
Gebruik variabelen om data op te slaan.

**Declaratie:** var (function scope), let (block scope), const (block scope)

**Data Types:**
string, number, boolean, null, undefined, object (arrays, objecten)

**Functions:**
Herbruikbare codeblokken voor specifieke taken.

Voorbeeld: function PrintResult(rollNum) { alert("Username with roll number " + rollNum + " has passed the exam"); }

**Loops:**
Voert herhalend code uit zolang een conditie waar is.

**Types:** for, while, do...while

Voorbeeld: for (let i = 0; i < 100; i++) { PrintResult(rollNumbers[i]); }

**JavaScript (JS)** is een **geïnterpreteerde taal**: je code wordt direct uitgevoerd in de browser, zonder aparte compilatie.

## Voorbeeldcode – Belangrijke Concepten

// Hello, World! programma

console.log("Hello, World!");

// Variabele en data type

let age = 25; // Number

// Control flow statement

if (age >= 18) {
console.log("You are an adult.");
} else {
console.log("You are a minor.");
}

// Functie

function greet(name) {
console.log("Hello, " + name + "!");
}

// Functie aanroepen

greet("Bob");

**Belangrijkste concepten:**

- **Variabelen** slaan data op, zoals `let age = 25;`
- **Data Types**: Number, String, Boolean, etc.
- **Control Flow**: Gebruik `if/else` voor beslissingen
- **Functies**: Herbruikbare blokken code

## Je eerste JS-programma in Chrome Console

**Stappen:**

1. Open **Google Chrome**
2. Druk op **Ctrl + Shift + I** (of rechtsklik → Inspect)
3. Klik op het tabblad **Console**

**Plak deze code:**

let x = 5;

let y = 10;

let result = x + y;

console.log("The result is: " + result);

**Uitleg:**

- `x` en `y` zijn variabelen met getallen
- `x + y` telt ze op
- `console.log` print het resultaat

**Druk op Enter → Output:** `The result is: 15`

## Internal vs External verificieren (Pentesting)

**Methode:** Rechtsklik op pagina → View Page Source

**Internal JS:** `<script> zonder src attribuut`

**External JS:** `<script src="script.js"></script> met src attribuut`

## JavaScript Dialog Boxes & Security

JS biedt interactie met gebruikers via ingebouwde functies. ⚠️ Kunnen misbruikt worden voor XSS aanvallen.

**Drie Belangrijke Functies**

1. **Alert** 

Toont een bericht met "OK" knop.

alert("Hello THM");

2. **Prompt**

Vraagt gebruiker om input. Geeft waarde terug of null.

name = prompt("What is your name?");

alert("Hello " + name);

3. **Confirm**

Vraagt bevestiging. Geeft true (OK) of false (Cancel) terug.

confirm("Do you want to proceed?");

**Security Risk – Misbruik door Hackers**

Voorbeeld aanval:

``` <!DOCTYPE html> <html> <head>

<title>Hacked</title>

</head> <body>

<script>

    for (let i = 0; i < 500; i++) {

        alert("Hacked");

    }

</script>

</body> </html> 
```

Resultaat: 500 alert boxes die je moet sluiten → zeer irritant!

## Control Flow in JavaScript

Control flow bepaalt de volgorde waarin code wordt uitgevoerd op basis van condities.

**Belangrijkste structuren:**

- if-else - Beslissingen maken

- switch - Meerdere opties afhandelen

- for, while, do...while - Acties herhalen (loops)

- Conditional Statements – if-else

Voert verschillende code uit afhankelijk van of een conditie true of false is.

Voorbeeld: Age Verification

``` <!DOCTYPE html> <html> <head>

<title>Age Verification</title>
</head> <body>

<h1>Age Verification</h1>


<p id="message"></p>


<script>


    age = prompt("What is your age")


    if (age >= 18) {


        document.getElementById("message").innerHTML = "You are an adult.";


    } else {


        document.getElementById("message").innerHTML = "You are a minor.";


    }


</script>
</body> </html>
```

Hoe het werkt:

Prompt vraagt om je leeftijd

Als age >= 18 → toont "You are an adult."

Anders → toont "You are a minor."

**Security Risk – Bypassing Login Forms**

Als authenticatie in client-side JavaScript wordt geïmplementeerd, kunnen aanvallers de logica omzeilen.

Voorbeeld: Een login form die username "admin" en een specifiek wachtwoord checkt in JS → Aanvaller kan de source code bekijken en de check omzeilen.

⚠️ Belangrijke les: Authenticatie moet altijd server-side gebeuren, nooit client-side!

## JavaScript Minification & Obfuscation

**Minification:**

Comprimeert JS bestanden door onnodige characters te verwijderen (spaties, line breaks, comments). Maakt code kleiner en sneller, maar moeilijker leesbaar.

**Obfuscation:**

Maakt JS code opzettelijk moeilijk leesbaar door:

- Variabelen hernoemen naar betekenisloze namen

- Dummy code toevoegen

- Code structuur verhullen

Belangrijk: Geobfusceerde code werkt exact hetzelfde, maar is niet meer menselijk leesbaar.

Voorbeeld:

**Originele code:**

function hi() {

alert("Welcome to THM");

}

hi();

**Geobfusceerde code:**

(function(_0x114713,_0x2246f2){var _0x51a830=_0x33bf,_0x4ce60b=_0x114713();while(!![]){try{var _0x51ecd3=-parseInt(_0x51a830(0x88))/(-0x1bd3+-0x9a+0x2*0xe37)...

**Deobfuscation (Pentesting)**

Je kunt geobfusceerde code terug omzetten naar leesbare code met online tools.

Tools:

Obfuscate: https://codebeautify.org/javascript-obfuscator

Deobfuscate: https://obf-io.deobfuscate.io/

⚠️ Security les: Obfuscation is geen echte beveiliging - aanvallers kunnen code makkelijk deobfuscaten en analyseren!

## JavaScript Security Best Practices

Best practices om aanvalsoppervlak te verkleinen en risico's te minimaliseren.

1. Avoid Client-Side Validation Only

❌ Fout: Alleen client-side validatie met JS

✅ Goed: Altijd server-side validatie toevoegen

Reden: Gebruikers kunnen JS uitschakelen of manipuleren in hun browser.

2. Refrain from Adding Untrusted Libraries

❌ Fout: Willekeurige JS libraries includen via src attribute

✅ Goed: Alleen libraries van vertrouwde bronnen gebruiken

Reden: Kwaadwillenden uploaden malicious libraries met namen die lijken op legitieme libraries.

3. Avoid Hardcoded Secrets

❌ Fout:

const privateAPIKey = 'pk_TryHackMe-1337';

✅ Goed: Gevoelige data (API keys, tokens, credentials) nooit in client-side JS code

Reden: Iedereen kan de source code bekijken en credentials stelen.

4. Minify and Obfuscate Your Code

✅ Goed: Minify en obfuscate JS code in productie

Voordelen:

- Verkleint bestandsgrootte

- Verbetert laadtijd

- Maakt reverse engineering moeilijker (maar niet onmogelijk)

⚠️ Belangrijk: Obfuscation is geen echte beveiliging, maar maakt aanvallen wel lastiger.