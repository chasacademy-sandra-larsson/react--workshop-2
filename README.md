
# React workshop #2: React Hooks, useState och useEffect  


👋 Denna workshop behandlar s 53-67, 79-81 i kursboken "The road to React" av Robin Wieruch ⚛️ 

### Innehåll denna workshop:
* Hantera events i React
* Använda de två vanligaste React Hooks, useState och useEffect 
* Side-effects
* Callback handlers
* Använda CSS i React


### Redovisning:
* Du/gruppen redovisar svaren på instuderingsfrågorna muntligt under workshop. 
* Du redovisar slutresultat av övningen Memory (se nedan) 

***Om du inte kan delta på workshopen, redovisar du ovanstående nästkommande workshop***

### 💬 Diskussionsfrågor

Diskutera följande frågor i studiegruppen medan ni jobbar, redovisa sedan för lärare. Gör egna anteckningar i syfte för kommande teorihandbok om React.

* Vad är skillnaden mellan useState och useEffect?
* Vad menas med lifting state?
* Vad är en side-effect?
* Vad är en callback handler?

### Gotcha!

Detta visar inte Robin i boken, men det bör tänkas på när uppdaterar ett state:s värde utifrån det tidigare värdet. Exempelvis: 

``` 
setCount(prevCount => prevCount + 1)  
```
Läs mer här: [https://reactjs.org/docs/hooks-reference.html](https://reactjs.org/docs/hooks-reference.html)

# 🏃 Uppvärmning 

Använd useState för att:

1. Öka en räknare med + 1. 
2. Toggla. Klicka på knappen => Dölj/visa något


# 👩🏽‍💻 Övning: Memory

Syftet med övningen är lära sig att bygga en enkel reactapp med flera komponenenter, använda props, men framförallt använda sig av de två mest viktiga Hooks i React - useState och useEffect.

### Din uppgift:

Skapa ett memoryspel med valfritt kort (exempelvis 10 st) där användaren kan starta spelet med en knapp för att sedan visa spelytan. Om kortet visar baksidan ska användaren kunna vända kortet. Efter att användaren vänt två kort, ska de vändas tillbaka igen. Om användaren får en match ska dessa kort ligga kvar med framsidan och inte kunna klickas på. 
 

## 1. Sätta upp ett Reactprojekt med Vite 

Se s 11-18 i kursboken

* Se till att du har Node.js installerat [https://nodejs.org](https://nodejs.org) 
* Navigera i terminalen där du vill installera din reactapplikation.
* Kör sedan du följande instruktion i terminalen

```
npm create vite@latest my-app -- --template react
```


## 2. Initiera memoryspelet

### Listan på bilder, ikoner

Välj bilder och placera dem i `/public`-mappen. Använd dig av ett objekt för att hantera sökvägen för dina bilder. Exempelvis:

```
	[
	  {'src':  '/card-1.png  },
	  {'src':  '/card-2.png  },
	  {'src':  '/card-3.png  },
	  {'src':  '/card-4.png  },
	  {'src':  '/card-5.png  },
	]
```

Bilder som ligger i publicfoldern kan alltså nås från App.jsx genom ovanstående url.
Se [https://vitejs.dev/guide/assets.html](https://vitejs.dev/guide/assets.html)


### Duplicera och shuffla 

Börja i App-komponenten. Skapa en funktion för att hantera duplicering och slumpande av kort. Den nya arrayen ska också innehålla ett id för varje kort. 

```
 const doubled = [...cardImages, ...cardImages] // Dublett med ES6 spread operator
 const shuffled = shuffled.sort(() => Math.random() - 0.5)) // Slumpa med sort
 const memoryCards = shuffled.map((card) => {{...card, id: Math.random()}); // Lägga till ett id för varje kort

```

Gör även en knapp "New game" som initierar arrayen av memorykort


## 3. Skapa state för memorykorten

Använd Reacts Hook useState, se boken på sidan 55.

* Initial state: En tom array
* State updater function: Använd denna för att intiera de shufflade korten
* State: Värdet som innehåller de nuvarande korten

Tänk på att använda konventionell namngivning, som `[cards, setCards] = ...`


## 4. Rendera ut memorykorten

* Varje "kort" ska ha varsin fram- och en baksida, d.v.s 2 st <img>. 
* Använd `map()` för att rendera ut varje kort (framsidan som slumpad bild, baksidan som fast bild) 
* Använd dig av lämplig CSS strategi - CSS modules, styled components, Tailwind)



## 5. Card komponenten

Bryt ner App komponenten så att memorykortet blir till en egen komponent.


## 6. Hantera när användaren klickar på ett kort

1. Lägg ett klickevent på kortet (baksidebilden) och en handler funktion inuti Card komponenten. 

2. Vi vill kunna hantera våra states i Appkomponenten, men hur löser vi det när användaren klickar på ett kort? Hur kan vi veta vilket kort vi klickar på i Appkomponenten? D.v.s hur kan vi kommunicera uppåt i trädet?
Läs sidan 57-59 i boken om callback handlers och använd dig av samma metod. 

D.v.s du ska skapa en funktion i Appkomponenten som kan ha information om vilket kort som klickats på. Döp den till `handleCardChoice(card)`

## 7. Hantera om första eller andra kortet är klickat 
 
 1. Definera två nya states i App som hanterar det första eller andra kortet (exempelvis setCardOne, setCardTwo). Använd `null` som initialt värde för båda.
 
 2. Skapa logik (exempelvis ternary operator) som avgör om det klickade kortet ska sättas till setCardOne eller setCardTwo. Detta kan göras för att se om nuvarande värde är satt eller inte. 

 
## 8. Kolla match av kort

1. För att veta om två kort har valts använder du istället useEffect. Ta första kortet och andra kortet innanför [] för att trigga funktionen när någon av dessa korts värde förändras. Använd dig av denna hook och kolla om de två korten matchar.

2. Utöka arrayen av kort med en property `matched` som är satt false till en början. Uppdaterade de matchade korten med `true

Se sidan 79-80 i boken.


## 9. Gör en reset efter varje dragning
 
Efter att användaren har dragit två kort så ska cardOne och cardTwo återställas till null igen. Skapa en funktion för den hanteringen och anropa den efter varje match-kontroll. Lägg gärna in en fördröjning på någon sekund (setTimeout) tills användaren kan vända nya kort.

## 10. Jobba med fler states 

1. Utöka memoryspelet med states för att hålla reda på hur många vändningar en användare gjort. 

2. Utöka med ett state som styr att kort är disablade under matchning

## 11. Finlir

Skapa ett win-condition, exempelvis att man klarar memoryt under visst antal dragningar. 

Gör en flipanimation :-)
