# Dominio Editoriale — 0000–0019

La numerazione è mutuata dal sistema Harvey, garantendo interoperabilità tra i due dataset. A differenza di Harvey — in cui i campi testuali erano aperti — in *Solo* i valori sono fissi e predeterminati. Tutti i campi di questo dominio sono implementati come **selezione chiusa con valore di default preimpostato**: l'annotatore conferma, non scrive. Questa scelta ottimizza i tempi di etichettatura ed elimina errori di trascrizione.

L'unica eccezione è la durata, dichiarata come `variable` e rimandando alle etichette del Formschema per i dati precisi per versione.

---

## 0000 — ImageDecorative

- **Tipo geometrico:** rettangolo
- **Attributi:**
  - `presente` — booleano

Elementi grafici decorativi presenti in copertina o nelle pagine introduttive, privi di contenuto informativo.

---

## 0001 — Page

- **Tipo geometrico:** rettangolo (intera pagina)
- **Attributi:**
  - `numero_pagina` — intero
  - `tipologia` — enum: `copertina` | `istruzioni` | `partitura` | `formschema`

---

## 0010 — ComposerName

- **Tipo geometrico:** rettangolo sul testo
- **Valore fisso:** `Karlheinz Stockhausen`

---

## 0011 — Title

- **Tipo geometrico:** rettangolo sul testo
- **Valore fisso:** `Solo`

---

## 0012 — Subtitle

- **Tipo geometrico:** rettangolo sul testo
- **Valore fisso:** `für Melodieinstrument mit Rückkopplung`

---

## 0013 — CatalogueNumber

- **Tipo geometrico:** rettangolo sul testo
- **Valore fisso:** `Nr. 19`

---

## 0014 — Year

- **Tipo geometrico:** rettangolo sul testo
- **Valore fisso:** `1965–66`

---

## 0015 — PublisherName

- **Tipo geometrico:** rettangolo sul testo o logo
- **Valore fisso:** `Universal Edition`

---

## 0016 — PublisherCode

- **Tipo geometrico:** rettangolo sul testo
- **Valore fisso:** `UE 14789`

---

## 0017 — Duration

- **Tipo geometrico:** rettangolo sul testo
- **Valore fisso:** `variable`

La durata precisa per ciascuna versione è codificata nelle etichette `1000 — Formschema_Version`.

---

## 0018 — PerformanceInstructions

- **Tipo geometrico:** rettangolo sul blocco testuale
- **Attributi:**
  - `lingua` — enum: `deutsch` | `english` | `français`

Il contenuto delle istruzioni non viene trascritto in questo dominio — la sua codifica strutturata appartiene al dominio del Formschema.
