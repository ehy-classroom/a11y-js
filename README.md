# a11y-js

# ♿ Barrierefreiheit (a11y) mit JavaScript & ARIA

Dieses Repository bietet eine praktische Einführung in das Thema **Barrierefreiheit (Accessibility, kurz a11y)** im Zusammenspiel mit **JavaScript** und **ARIA (Accessible Rich Internet Applications)**.

Zielgruppe: Entwickler:innen mit HTML/CSS/JS-Grundkenntnissen, die lernen wollen, wie man interaktive Web-Komponenten barrierefrei umsetzt.

---

## 🌍 Warum ist Barrierefreiheit wichtig?

Barrierefreiheit sorgt dafür, dass digitale Inhalte von **allen Menschen** genutzt werden können – unabhängig von körperlichen, sensorischen oder kognitiven Einschränkungen.  
Gerade **JavaScript-basierte, dynamische Webinhalte** können dabei schnell Barrieren aufbauen, wenn sie nicht richtig umgesetzt werden.

---

## 🧠 Grundidee: Was macht JavaScript (un)barrierefrei?

### JavaScript kann:
- den **Fokus verändern** (z. B. auf Modals oder nach Fehlern)
- **Inhalte dynamisch laden oder verstecken**
- neue **interaktive Komponenten erzeugen** (z. B. Tabs, Slider, Dialoge)
- **Formulare validieren** und Feedback geben

➡️ Ohne zusätzliche Maßnahmen bekommt ein Screenreader davon **nichts mit**.

---

## 🔧 Lösung: ARIA + gutes Fokus- und Tastaturmanagement

ARIA ergänzt HTML um **semantische Hinweise** für assistive Technologien.  
JavaScript übernimmt dabei die **Zustandsverwaltung**, z. B.:

- `aria-expanded`, `aria-hidden`, `aria-live`, `role`, …
- Fokus gezielt setzen: `element.focus()`
- Tastaturnavigation implementieren

---

## 📦 Beispiel: Barrierefreies Accordion

```html
<h3>
  <button aria-expanded="false" aria-controls="panel1" id="accordion1">
    Abschnitt 1
  </button>
</h3>
<div id="panel1" role="region" aria-labelledby="accordion1" hidden>
  <p>Inhalt des Abschnitts.</p>
</div>
```

```javascript
document.querySelectorAll('button[aria-controls]').forEach((btn) => {
  btn.addEventListener('click', () => {
    const expanded = btn.getAttribute('aria-expanded') === 'true';
    btn.setAttribute('aria-expanded', String(!expanded));
    document.getElementById(btn.getAttribute('aria-controls')).hidden = expanded;
  });
});
```
Erklärungen:

aria-expanded: Gibt den Zustand des Buttons an (offen/geschlossen)

aria-controls: Verweist auf das zugehörige Panel

role="region" & aria-labelledby: Machen das Panel für Screenreader verständlich

hidden: Macht den Bereich auch für Screenreader unsichtbar