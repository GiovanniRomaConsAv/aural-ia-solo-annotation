# Ground Truth Metodologico — Solo Nr. 19

**Progetto:** Aural-ia  
**Istituzione:** Conservatorio Statale di Musica Domenico Cimarosa  
**Dottorato:** Scienze, Tecnologie Avanzate e Nuovi Paradigmi nella Ricerca Musicologica e nella Musica del Presente — 40° Ciclo, A.A. 2024/2025  
**Opera:** Karlheinz Stockhausen, *Solo für Melodieinstrument mit Rückkopplung* Nr. 19 (1965–66)  
**Documento:** Lavoro ad uso interno — non destinato alla pubblicazione autonoma

---

## Descrizione

Questo repository contiene il ground truth metodologico per il sistema di annotazione di *Solo* di Stockhausen, sviluppato nell'ambito del progetto Aural-ia. Il sistema è progettato per essere implementato in CVAT (Computer Vision Annotation Tool) e alimenta una pipeline di ricerca comparativa tra architetture RAG e fine-tuning.

Il ground truth non indica una verità ontologica dell'opera, ma un riferimento operativo, dichiarato e verificabile, costruito per rendere confrontabili annotazioni, inferenze e procedure di recupero.

---

## Struttura del repository

```
/docs
  README.md                  ← questo file
  PRINCIPLES.md              ← principi metodologici
  NUMBERING.md               ← strategia di numerazione delle etichette
  PIPELINE.md                ← pipeline dalla annotazione al training
  RESEARCH_DESIGN.md         ← disegno della ricerca
/catalogue
  00_editorial.md            ← dominio editoriale (0000–0019)
  10_formschema.md           ← dominio Formschema (1000–1999)
  20_score.md                ← dominio partitura (2000–2999)
  30_manual.md               ← dominio manuale (3000–3099)
/schema
  editorial.schema.json      ← JSON Schema dominio editoriale
  formschema.schema.json     ← JSON Schema dominio Formschema
  score.schema.json          ← JSON Schema dominio partitura
/tools
  formschema_trascrizione.html  ← tool di trascrizione interattivo
```

---

## Contesto musicologico

*Solo* è un sistema chiuso di possibilità strutturali predefinite in cui ogni scelta — dalla selezione del Formschema all'assegnazione delle pagine ai cicli, dalla costruzione della partitura esecutiva alla gestione dei livelli da parte degli assistenti — è una decisione compositiva esercitata entro regole precise. Stockhausen non abdica alla struttura, la delega. La conoscenza delle regole non è prerequisito tecnico: è condizione dell'esecuzione stessa.

La logica compositiva di *Solo* si articola su due livelli distinti e non intercambiabili:

- **Macro-formale** — determinato dai pattern di sovrapposizione elettronica distribuiti sistematicamente attraverso le sei versioni (come dimostrato da Nerenberg 2014)
- **Micro-formale** — determinato dal contenuto musicale e dai parametri interpretativi

La conseguenza più rilevante per il sistema di annotazione è la **mutevolezza semantica contestuale**: lo stesso gesto musicale nella partitura può assumere posizioni, significati e durate differenti a seconda del Formschema scelto.

---

## Architettura dei domini

| Fascia | Dominio | Contenuto |
|--------|---------|-----------|
| 0000–0019 | Editoriale | Copertina, titolo, editore, istruzioni |
| 1000–1999 | Formschema | Versioni, sezioni, periodi, operatori, eventi speciali |
| 2000–2999 | Partitura | Pagine, sistemi, righi, moduli |
| 3000–3099 | Manuale | Diagrammi tecnici annotati in CVAT |

Il testo del manuale di Stockhausen viene segmentato direttamente per il RAG (vision-augmented indexing) senza passare da CVAT.

---

## Riferimenti

- Nerenberg, Mark. "Structure Formation: An Analysis of Electronic Superimpositions in Stockhausen's Solo." *eContact!* 16.3, CEC, 2014.
- Stockhausen, Karlheinz. *Solo für Melodieinstrument mit Rückkopplung* Nr. 19. Vienna: Universal Edition (UE 14789), 1969.
- Roma, Giovanni; Battista, Alba Francesca. "A Modular Annotation Toolset for Electroacoustic Score Preservation." ICAIHE 2026 (AICA) [in corso di pubblicazione].
- Roma, Giovanni; Battista, Alba Francesca. "Supervised Memory: How Machines Can Preserve What We Cannot Hold." ICMC 2026.
