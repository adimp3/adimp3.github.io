# Statische Website mit PaaS

## Die Website

Vor ein Paar Tagen fand ich mich auf der GitHub Copilot website, als ich mir überlegte ob ich diesen kleinen helfer kaufen sollte oder nicht, fielen mir die schönen scroll Animationen auf. Ich fragte mich ob ich das auch könne. Danach entschied ich mich, selbst eine Website mit solchen scroll Animationen zu machen. Ich habe nur wenige Kenntnisse in HTML, CSS und Javascript, dennoch habe ich mich dazu entschieden diese Website als Projekt für das Modul 346 zu machen.


Zuerst musste ich herausfinden, wie ich überhaupt Animationen auf einer Website anzeigen kann. Ich fand dazu eine CSS funktion, @scroll-timeline, die genau das macht, was ich gerne hätte faul wie ich bin habe ich mir überlegt, ob ich sie nutzen sollte. Ich fand aber bald heraus, dass die Funktion von fast keinem Modernen Browser unterstützt wird und habe mich deshalb dagegen entschieden. 

Danach habe ich mich weiter umgeschaut, und die "Intersection-Observer" API gefunden, welche überprüft, ob ein Element der Website für den Enduser sichtbar ist. Wenn das Element sichtbar ist kann mann neue CSS Klassen darauf anwenden, welche das Element dann Animieren.

### HTML

Mit dem Snippet "!" habe ich diesen Boilerplate code von HTML generiert:

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
</body>
</html>

```

Danach habe ich im Head des Dokuments ein Stylesheet verlinkt (style.css) und ein Script hinzugefügt (app.js).

Den Inhalt der Website habe ich mir etwas aus der Nase gezogen... Der ist ja auch nicht wichtig, wichtig sind die Scroll-Animationen
Ich wollte diese Scroll-Animationen aber nicht nur mit Text machen, sondern wollte auch animierte Bilder haben. Deshalb habe ich mir auf dicebar einige Avatare erstellt, welche ich dann jeweils als div in das dokument eingefügt habe.

### CSS

Im style.css file habe ich dann eine Google-Font importiert und einen Schwärzlichen hintergrund eingefügt. Dann habe ich die Div's zentriert.
Folgende Klassen habe ich ebenfalls definiert und jedem HTML-Element die show klasse assigned.
```CSS

.hidden {
    opacity: 0;
    filter: blur(6px);
    transform: translateX(-100%);
    transition: all 1s;
}

.show {
    opacity: 1;
    filter: blur(0);
    transform: translateX(0);

```

### JavaScript

Um den Intersection-Observer einzubauen habe ich folgenden JavaScript Code geschrieben:

```JavaScript
const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
        console.log(entry)
        if (entry.isIntersecting) {
            entry.target.classList.add('show');
        } else {
            entry.target.classList.remove('show');
        }
    });
});

const hiddenElements = document.querySelectorAll('.hidden');
hiddenElements.forEach((el) => observer.observe(el));
```

Dieser Code "Aktiviert" den IntersectionObserver und überprüft für jedes Element, ob es sichtbar ist oder nicht, wenn es sichtbar ist, gibt es ihm die klasse "show", wenn es nicht sichtbar ist, gibt es ihm die Klasse "hidden". Diese klassen habe ich oben im CSS definiert.

Danach habe ich eine Domain "qreq.ch" gekauft(!) und die website mit diesem befehl: `scp -r ./ jeremy@qreq.ch:/home/jeremy/public_html/qreq.ch/` auf das Webhosting kopiert. "jeremy" ist hierbei der Username und "qreq.ch" der server, das -r steht für rekursiv (so konnte ich alle 3 files auf einmal kopieren) scp steht für "ssh-copy".
