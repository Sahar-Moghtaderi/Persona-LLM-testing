# Web Frontend Testing mit Claude Code

Automatisiertes UI-Testing mit KI-gestützter Analyse. Claude navigiert durch deine Anwendung, führt User Journeys durch und dokumentiert alle gefundenen Probleme mit Screenshots.

---

## Einmaliges Setup

### 1. Node.js installieren (falls noch nicht vorhanden)
Lade Node.js von https://nodejs.org herunter und installiere es (LTS-Version empfohlen).

### 2. Abhängigkeiten installieren
Öffne ein Terminal in diesem Ordner und führe aus:
```bash
npm install
npm run setup
```

### 3. Claude Code installieren (falls noch nicht vorhanden)
```bash
npm install -g @anthropic-ai/claude-code
```

---

## Workflow: Test ausführen

### Schritt 1: Persona anlegen
- Öffne den Ordner `personas/`
- Kopiere `template-persona.md` und benenne die Kopie nach der Persona, z.B. `max-mustermann.md`
- Fülle alle Felder aus

### Schritt 2: User Journey anlegen
- Öffne den Ordner `journeys/`
- Kopiere `template-journey.md` und benenne die Kopie passend, z.B. `login-und-dashboard.md`
- Beschreibe jeden Schritt so präzise wie möglich

### Schritt 3: Claude Code starten
Öffne ein Terminal in diesem Ordner und starte Claude Code:
```bash
claude
```

### Schritt 4: Test starten
Sage Claude Code zum Beispiel:
> "Führe einen Test durch mit Persona max-mustermann und Journey login-und-dashboard"

oder

> "Teste https://meine-app.de mit der Persona max-mustermann und Journey login-und-dashboard"

Claude liest dann automatisch deine Dateien, öffnet den Browser, führt die Journey durch und erstellt einen Report.

### Schritt 5: Ergebnisse ansehen
- **Reports:** Im Ordner `reports/` findest du den Markdown-Report
- **Screenshots:** Im Ordner `screenshots/` findest du alle gemachten Screenshots

---

## Ordnerstruktur

```
web-frontend-testing/
├── personas/              # Deine Persona-Beschreibungen
│   └── template-persona.md
├── journeys/              # Deine User Journeys
│   └── template-journey.md
├── reports/               # Automatisch erstellte Testreports
├── screenshots/           # Automatisch gemachte Screenshots
├── testplans/             # Funktionale Testpläne (Pass/Fail)
├── CLAUDE.md              # Anweisungen für Claude (nicht ändern)
├── prompts/               # Templates (Report-Format etc.)
├── .mcp.json              # Playwright-Konfiguration (nicht ändern)
└── README.md              # Diese Datei
```

---

## Warum Playwright (und nicht Chrome MCP)?

Wir verwenden den Playwright-MCP-Server, weil er Seitenelemente technisch identifiziert statt per Screenshot-Erkennung. Das macht Klicks zuverlässiger und Tests reproduzierbar, da jeder Lauf mit einem sauberen Browser ohne alte Cookies startet. Mit `--headed` in `.mcp.json` kann man dem Browser trotzdem live beim Testen zuschauen.

---

## Tipps für gute User Journeys

- **Sei konkret:** Statt "gehe zu den Einstellungen" schreibe "klicke auf das Zahnrad-Icon oben rechts"
- **Erwartungen definieren:** Was soll nach jedem Schritt auf dem Bildschirm zu sehen sein?
- **Testdaten angeben:** Wenn Login nötig ist, gib Testnutzer-Daten an
- **Edge Cases:** Beschreibe auch, was bei falschen Eingaben passieren soll

---

## Fehlerbehebung

**Claude kann den Browser nicht starten:**
→ Führe nochmal `npm run setup` aus

**Claude findet Playwright nicht:**
→ Stelle sicher, dass `npm install` ausgeführt wurde

**Screenshots werden nicht gespeichert:**
→ Stelle sicher, dass der `screenshots/` Ordner existiert
