# 🧠 Flashcards Extended per Obsidian

**Flashcards Extended** è un plugin professionale e ad altissime prestazioni progettato per sincronizzare in modo bidirezionale, ultra-robusto ed elegante le tue note Obsidian con **Anki**. 

Grazie al motore di parsing sequenziale **Space-Masking**, il plugin garantisce l'esclusione assoluta da falsi positivi all'interno di blocchi di codice e formule matematiche LaTeX, offrendo al contempo un'esperienza premium con design allo stato dell'arte e integrazione nativa dei modelli Anki.

---

## 🚀 Funzionalità Chiave

### 1. 🛡️ Parser Sequenziale "Space-Masking"
Il parser del plugin utilizza un'architettura a **mascheramento sequenziale dei caratteri**. Prima di analizzare i separatori o le delezioni a comparsa (cloze), il motore crea una copia mascherata del testo in cui vengono progressivamente azzerati (sostituiti con spazi, preservando i caratteri di a capo `\n` per mantenere l'allineamento 1-a-1 degli indici):
* Blocchi di codice delimitati da tre triple virgolette (\`\`\`python ... \`\`\`).
* Codice in linea racchiuso tra backtick (\`codice :: in linea\`).
* Formule matematiche LaTeX multilinea (`$$ ... $$`).
* Formule matematiche LaTeX in linea (`$ ... $`).

> [!TIP]
> Questo significa che puoi includere liberamente parentesi graffe matematiche (es. `A = \{ x \in \mathbb{R} \}`), formule MathJax o codice sorgente senza temere che vengano erroneamente scambiati per flashcards o clozes!

---

### 2. 🎴 4 Modelli di Nota Semplificati & Puliti
Tutti i suffissi complessi come `-source` sono stati eliminati. Il plugin gestisce 4 modelli fissi in Anki che rimangono stabili, puliti e completamente aggiornabili dal plugin:
1. **Obsidian-basic:** Modello classico Fronte/Retro.
2. **Obsidian-basic-reversed:** Modello Fronte/Retro e Retro/Fronte bidirezionale.
3. **Obsidian-spaced:** Modello a visualizzazione singola per ripasso attivo (Prompt).
4. **Obsidian-cloze:** Modello Cloze nativo Anki con supporto a delezioni multiple.

---

### 3. 🕊️ Supporto Source Avanzato (Origami Link)
Attivando `"sourceSupport": true` nel file di configurazione avanzata `data.json`, il plugin:
* Aggiunge un campo `Source` pulito in Anki popolato esclusivamente dall'URI raw di Obsidian (`obsidian://open?vault=...`).
* Inserisce automaticamente sul retro delle carte Anki un'**icona Origami SVG ultra-moderna e responsive** al posto del testo statico del link.

#### Stile & Micro-animazioni Premium
L'icona Origami eredita transizioni HSL avanzate che offrono una magnifica esperienza utente:
* **Stato Normale:** Colore grigio neutro elegante (`#a0a0a0`).
* **Stato Hover (passaggio mouse):** Transizione fluida in 0.35s verso un blu vivido (`#3b82f6`) con un leggero effetto di scala geometrica (`scale(1.05)`).
* **Click:** Apre istantaneamente Obsidian posizionandoti esattamente sulla nota sorgente.

---

### 4. 🔠 Sincronizzazione Cloze Nativa Ultra-Flessibile
Il plugin supporta qualsiasi sintassi per le delezioni Cloze e le mappa direttamente sul tipo di nota nativo di Anki (`modelType: "cloze"`):
* **Sintassi Standard:** `{c1:testo}` o `{C2:testo}` (con indici multipli nello stesso paragrafo).
* **Sintassi Graffe Semplici:** `{testo}` (mappato automaticamente su `c1`).
* **Evidenziazione Markdown:** `==testo evidenziato==` (mappato automaticamente su `c1`).
* **Cloze con Formule Interno:** Supporto eccezionale a clozes contenenti formule matematiche come `{c1:$$ A = \pi r^2 $$}`!

---

### 5. 📂 Gestione Mazzi Dinamica & Parent-Folder
Il plugin assegna in modo intelligente le carte al mazzo corretto:
1. **Override Frontmatter:** Se la nota contiene `cards-deck: NomeMazzo` nel frontmatter YAML, le carte andranno in quel mazzo.
2. **Folder-Based Deck:** Se abilitato, le carte prendono il nome della cartella genitore della nota, convertendo le sottocartelle in sottomazzi Anki (es. cartella `Medicina/Cardiologia` $\rightarrow$ mazzo `Medicina::Cardiologia`).
3. **Mazzo Predefinito:** Se nessuna delle precedenti è soddisfatta, viene usato il mazzo definito in configurazione (es. `default`).

---

### 6. 🔄 Sincronizzazione Vault-Wide (Tutto il Vault)
È disponibile un comando avanzato registrato esclusivamente nel **Riquadro dei Comandi (Command Palette)** di Obsidian:
* **Nome Comando:** `Generate for all files in the vault (Backup recommended)`
* **Comportamento:** Scansiona in sequenza tutte le note del vault mostrando un indicatore di progresso in tempo reale per evitare blocchi o congestioni di rete.

> [!WARNING]
> **Consiglio di Backup:** Prima di avviare la scansione globale di tutte le note del vault, si raccomanda caldamente di effettuare un backup manuale della cartella del tuo vault Obsidian (es. una copia `.zip` veloce). Il comando richiederà una conferma esplicita prima di partire.

---

### 7. 🩹 Allineamento Automatico degli ID & Prevenzione Duplicati
Se un ID Anki inserito in una nota markdown viene cancellato, modificato per errore o se la carta viene eliminata su Anki:
* Il plugin effettua una ricerca fuzzy su Anki basandosi sul testo del Fronte della carta.
* Se trova una corrispondenza univoca, **recupera e aggiorna l'ID corretto all'interno del file markdown** in modo totalmente silente, evitando la duplicazione delle carte e mantenendo allineate le statistiche di studio!

---

## 🛠️ Configurazione Avanzata (`data.json`)

Le impostazioni più avanzate destinate ai Power User sono configurabili direttamente nel file [data.json](file:///.obsidian/plugins/flashcards-extended/data.json) situato nella cartella del plugin:

```json
{
  "//_POWER_USER_SETTINGS_//": "WARNING: The following settings are for power users and only modifiable directly in data.json before the first use of the plugin.",
  "sourceSupport": true,
  "basicModel": "Obsidian-basic",
  "reversedModel": "Obsidian-basic-reversed",
  "spacedModel": "Obsidian-spaced",
  "clozeModel": "Obsidian-cloze",
  "contextAwareMode": true,
  "inlineID": true,
  "contextSeparator": ", ",
  "deck": "default",
  "folderBasedDeck": true,
  "flashcardsTag": "card",
  "inlineSeparator": "::",
  "inlineSeparatorReverse": ":::",
  "defaultAnkiTag": "obsidian",
  "ankiConnectPermission": true,
  "ankiConnectUrl": "http://localhost:8765"
}
```

---

## 📝 Sintassi dei Test e Esempi

Per testare tutte le funzionalità del plugin in modo interattivo e convalidare la robustezza del parser, puoi consultare o creare i file di test inclusi nella suite di collaudo:
* **Tipi di Nota:** [test_note_types.md](file:///c:/Users/giuly/OneDrive/Documenti/Obsidian/github/test_note_types.md) (Inline, Multiline, Cloze Multipli).
* **Gestione Errori:** [test_error_handling.md](file:///c:/Users/giuly/OneDrive/Documenti/Obsidian/github/test_error_handling.md) (Esclusione di blocchi di codice, formule con graffe LaTeX e cloze matematici).
* **Media & Audio:** [test_media.md](file:///c:/Users/giuly/OneDrive/Documenti/Obsidian/github/test_media.md) (Sincronizzazione di immagini e registrazioni audio).
