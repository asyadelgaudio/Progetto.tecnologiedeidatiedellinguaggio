# Il Calderone delle Allucinazioni · Quando un'intelligenza artificiale inventa

*Progetto ad opera di Asia Del Gaudio* · Tecnologie dei dati e del linguaggio – Università degli Studi di Milano

Quanto spesso un'intelligenza artificiale inventa informazioni quando le chiediamo dettagli su un universo narrativo? E cambia qualcosa se le chiediamo le fonti o le diamo il testo dei libri da consultare?

---

## Il progetto in breve

- **151 domande** sulla saga *La corte di rose e spine* di Sarah J. Maas (5 libri), ognuna con la risposta verificata sui libri: domande reali, **trabocchetti** con una premessa falsa preparata apposta (per esempio sul fratello di Feyre, che non esiste) e domande di controllo.
- **Gemma 4** (Google), un modello aperto, ha risposto a ogni domanda in **3 modi diversi**: A con la sola domanda, B chiedendo di indicare libro e capitolo, C dandole i 4 estratti dei libri più simili alla domanda.
- **Claude Opus 5.5** (Anthropic) ha risposto alle stesse domande nella condizione A, aprendo una chat nuova per ogni domanda.
- In tutto **604 risposte**, valutate a mano: corretta, allucinazione o astensione, con tono e tipo di errore.
- Un **test di familiarità** (nomi dei personaggi nascosti in 30 passi dei libri) misura quanto ciascun modello conosce già i libri.

Le domande sono sempre le stesse: se la risposta cambia, dipende dal modello o da quello che gli diamo da leggere.

---

## Domande di ricerca

1. **RQ1** · Davanti a una domanda con una premessa falsa, il modello la asseconda invece di correggerla?
2. **RQ2** · Le citazioni sono la categoria più critica, con frasi inventate attribuite a personaggi coerenti con il tono?
3. **RQ3** · Chiedere di indicare le fonti riduce le invenzioni?
4. **RQ4** · Dare al modello gli estratti dei libri da consultare riduce le invenzioni?

Risultati, grafici ed esempi sono nel notebook.

---

## Che cosa c'è nella repository

| File o cartella | Contenuto |
|---|---|
| `Il_Calderone_delle_Allucinazioni.ipynb` | **Il notebook**: come sono state raccolte le risposte, poi l'analisi domanda per domanda, con grafici ed esempi di risposte |
| `requirements.txt` | le librerie Python usate |
| `ACOTAR/01_domande/ACOTAR_domande_v3.xlsx` | le 151 domande con categoria, tipo, risposta verificata e libro e capitolo di riferimento |
| `ACOTAR/02_risposte/risposte_gemma-4-31B-it.csv` | le 453 risposte di Gemma, con il prompt inviato e gli estratti usati nella condizione C |
| `ACOTAR/03_annotazione/ACOTAR_da_annotare_gemma-4-31B-it.xlsx` | la valutazione a mano delle 604 risposte di Gemma e Claude, con la legenda delle etichette |
| `ACOTAR/04_familiarita/` | il test di familiarità di Gemma e di Claude |
| `ACOTAR/06_risultati/` | le tabelle e i grafici prodotti dal notebook |

---

## Preparare la cartella su Google Drive

Il notebook legge e salva i file in Google Drive, nella cartella `ACOTAR`. Questa cartella deve stare direttamente in **Il mio Drive** (non dentro un'altra cartella) e avere esattamente questa struttura, con gli stessi nomi:

```
Il mio Drive/
└── ACOTAR/
    ├── 01_domande/
    │   └── ACOTAR_domande_v3.xlsx
    ├── 02_risposte/
    │   └── risposte_gemma-4-31B-it.csv
    ├── 03_annotazione/
    │   └── ACOTAR_da_annotare_gemma-4-31B-it.xlsx
    ├── 04_familiarita/
    │   ├── test_familiarita_gemma-4-31B-it.csv
    │   └── Cloze_Claude.xlsx
    └── 06_risultati/
```

Come prepararla:

1. Scaricare la repository da GitHub (**Code → Download ZIP**) ed estrarre lo ZIP sul computer.
2. Aprire [Google Drive](https://drive.google.com) e trascinare la cartella `ACOTAR` dentro **Il mio Drive**.
3. Controllare che i nomi di cartelle e file non siano cambiati durante il caricamento (Drive a volte aggiunge "(1)" ai nomi se esiste già un file uguale).

La cartella `06_risultati` può anche mancare: il notebook la crea da solo e ci salva tabelle e grafici. Per rigenerare le risposte di Gemma serve anche una cartella `ACOTAR/libri/` con i 5 libri in EPUB o PDF, che non sono inclusi. Se la cartella `ACOTAR` viene messa in un altro posto del Drive, basta cambiare la variabile `CARTELLA` nella sezione 2 del notebook.

---

## Come aprire il notebook

1. Preparare la cartella su Google Drive come descritto sopra.
2. Aprire **`Il_Calderone_delle_Allucinazioni.ipynb`** in Google Colab (**File → Carica notebook**).
3. Eseguire le sezioni **1 e 2** (autorizzando l'accesso a Drive), poi tutte le sezioni **dalla 8 alla 16**. Non serve la GPU e bastano pochi minuti.

Le sezioni 3–7 mostrano come sono state raccolte le risposte di Gemma: sono già state eseguite e i loro risultati sono sotto le celle. Per rigenerarle servono una GPU A100, una chiave Hugging Face (`HF_TOKEN`) nei secreti di Colab e i libri, che non sono inclusi. Le sezioni 3b e 7b si possono eseguire anche senza GPU.

---

## Limiti

- 151 domande su una sola saga e una sola risposta per condizione: i risultati sono indicativi.
- Valutazione a mano fatta da una sola persona.
- Claude è stato provato solo nella condizione A.

---

## Note

- I testi dei libri non sono inclusi perché protetti da diritto d'autore; le risposte e il test di familiarità ne contengono brevi estratti, usati solo a scopo di studio.
- Modelli usati: `google/gemma-4-31B-it` (pesi aperti, da Hugging Face), Claude Opus 5.5 (claude.ai) e `intfloat/multilingual-e5-base` per la ricerca degli estratti.
- Codice scritto con il supporto di un assistente AI.
