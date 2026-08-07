# Pipeline: Dalla Annotazione al Training

---

## Panoramica

Il dataset prodotto attraverso l'annotazione CVAT e la segmentazione del manuale alimenta parallelamente i due sistemi oggetto di confronto — fine-tuning e RAG — a partire dalla stessa sorgente verificata.

```
Annotazione CVAT          Manuale di Stockhausen
      │                          │
      ▼                          ▼
  JSON export            Segmentazione per paragrafo
      │                  (vision-augmented indexing)
      └──────────┬────────────────┘
                 │
         Dataset comune verificato
                 │
        ┌────────┴────────┐
        ▼                 ▼
   Fine-tuning           RAG
   (coppie Q&A)    (knowledge base)
        │                 │
        └────────┬────────┘
                 ▼
          Confronto comparativo
```

---

## Fase 1 — Export e strutturazione

- **CVAT** → export JSON nativo
- **Manuale** → chunk per paragrafo numerato con immagini associate (LlamaIndex/LlamaParse)
- La chiave di correlazione è `riferimento_istruzione` (stessa chiave nel JSON CVAT e nei chunk del manuale)

---

## Fase 2 — Generazione automatica delle tuple

Dal JSON CVAT viene generato automaticamente uno script Python che produce tuple strutturate per ogni unità annotata.

**Tuple tipo operatori 1–2:**
```json
{"versione": "II", "sezione": "B", "periodo": 7, "operatore": 1, 
 "canale": "left", "on": true, "perforazioni": 3, 
 "number_semantics": "PERFORATION", "distribution": "AD_LIB"}
```

**Tuple tipo operatore 3:**
```json
{"versione": "II", "sezione": "B", "periodo": 7, "operatore": 3,
 "canale": "left", "on": true, "sovrapposizioni": 2,
 "envelope": "0 0, 1 500, 0 2000", "forma_derivata": "fade_in"}
```

---

## Fase 3 — Costruzione semi-manuale delle coppie per il fine-tuning

Le domande sono formulate **semi-manualmente** dall'autore (scelta delle domande musicalmente rilevanti). Le risposte sono estratte **meccanicamente** dalle tuple — non inventate.

Questa asimmetria garantisce che le risposte abbiano la stessa affidabilità della ground truth annotata.

**Formato output:** JSONL standard (instruction, input, output)

```json
{"instruction": "Cosa fa l'operatore 1 al periodo 7 della versione II sul canale sinistro?",
 "input": "",
 "output": "Il fader è aperto con 3 perforazioni, distribuzione ad libitum."}
```

Ogni coppia porta i metadati di provenienza: versione, periodo, etichetta sorgente.

---

## Fase 4 — Biforcazione

| Sistema | Modalità | Modello |
|---------|----------|---------|
| **RAG** | Consulta il JSON + chunk manuale in tempo reale | Non modificato |
| **Fine-tuning** | Adatta i pesi del modello sulle coppie Q&A | Modificato |

La biforcazione su sorgente comune garantisce che le differenze di prestazione siano attribuibili **esclusivamente all'architettura**, non ai dati.

---

## Fase 5 — Misurazione e confronto

- **Metriche quantitative:** accuratezza, F1, BLEU (per risposte strutturate)
- **Valutazione qualitativa:** condotta dall'autore per risposte che richiedono ragionamento contestuale
- **Tracciabilità:** ogni risposta è tracciabile alla sua fonte nel dataset

L'esito atteso non è una preferenza tecnica ma un **criterio epistemologico**: quale architettura è più compatibile con la responsabilità di preservazione che il progetto si assume.
