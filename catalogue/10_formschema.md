# Dominio Formschema — 1000–1999

Il Formschema governa l'intera esecuzione di *Solo*: 51 periodi fissi suddivisi in sei sezioni (A–F), le azioni dei tre operatori su ciascun canale, gli eventi speciali e lo schema interpretativo. La struttura di 51 periodi è invariante attraverso tutte e sei le versioni.

---

## 1000 — Formschema_Version

- **Tipo geometrico:** rettangolo (intera pagina del Formschema)
- **Attributi:**
  - `versione` — enum: `I` | `II` | `III` | `IV` | `V` | `VI`
  - `durata_totale_secondi` — decimale
  - `numero_periodi_totali` — intero fisso: `51`
  - `riferimento_istruzione` — stringa: `"2"`, `"x_1"`

---

## 1001 — Formschema_Section

- **Tipo geometrico:** rettangolo (colonna verticale della sezione)
- **Attributi:**
  - `versione` — enum: `I`–`VI`
  - `lettera_sezione` — enum: `A` | `B` | `C` | `D` | `E` | `F`
  - `durata_totale_secondi` — decimale
  - `numero_periodi` — intero
  - `durata_singolo_periodo_secondi` — decimale
  - `riferimento_istruzione` — stringa: `"3"`, `"4"`, `"5"`

---

## 1002 — Period

Etichetta verticale che fotografa lo stato di tutti gli operatori su entrambi i canali in un singolo periodo.

- **Tipo geometrico:** rettangolo (colonna verticale del periodo)

### Attributi strutturali

| Attributo | Tipo | Note |
|-----------|------|------|
| `versione` | enum I–VI | |
| `sezione` | enum A–F | |
| `numero_progressivo_assoluto` | intero 1–51 | |
| `numero_progressivo_nella_sezione` | intero | |
| `durata_secondi` | decimale | |
| `is_electronic_rest` | booleano | `true` obbligatorio per A_1 |
| `riferimento_istruzione` | stringa | `"4"`, `"x_2"` |

### Attributi per operatore 1 e 2 (per ogni canale left/right)

Prefissi: `op_1_left_`, `op_1_right_`, `op_2_left_`, `op_2_right_`

| Attributo | Tipo | Note |
|-----------|------|------|
| `on` | booleano | fader aperto |
| `perforazioni` | intero | numero di chiusure nel periodo |
| `number_semantics` | enum | `PERFORATION` \| `OMISSION` |
| `distribution` | enum | `AD_LIB` \| `ACCEL` \| `RIT` \| `ACCEL_RIT` |
| `duration_s_stated` | decimale | durata dell'apertura in secondi; null se non specificata |
| `open_offset_s_stated` | decimale | ritardo dall'inizio del periodo; null se assente |
| `approx` | booleano | durata approssimata |

### Attributi per operatore 3 (per ogni canale left/right)

Prefissi: `op_3_left_`, `op_3_right_`

| Attributo | Tipo | Note |
|-----------|------|------|
| `on` | booleano | interruttore aperto |
| `sovrapposizioni` | intero | numero linee parallele sull'interruttore; 0 se chiuso |
| `envelope` | stringa line~ | coppie `ampiezza tempo_ms`; primo tempo = 0; ampiezza 0–1 |
| `forma_derivata` | enum | derivato automaticamente dall'envelope (vedi sotto) |

**Formato envelope (line~):** coppie spazio-separate di `ampiezza tempo_ms`, es. `0 0, 1 500, 0.5 1000, 0 2000`. Il sistema deriva automaticamente la forma:

| forma_derivata | Condizione |
|----------------|------------|
| `piatto` | tutti i valori di ampiezza uguali e > 0 |
| `fade_in` | solo incrementi |
| `fade_out` | solo decrementi |
| `fade_in_out` | picco interno |
| `fade_out_in` | valle interna |
| `composito` | nessuno dei precedenti |
| `none` | envelope vuoto |

---

## 1010–1015 — Etichette orizzontali degli operatori

Descrivono la sequenza completa dei 51 stati di un singolo operatore su un singolo canale. Fungono sia da rappresentazione del gesto prolungato nel tempo sia da strumento di validazione rispetto alle etichette Period (1002).

**Compilazione:** sempre in ordine progressivo da periodo 1 a periodo 51.  
**Riferimento istruzione condiviso:** `"x_1"`, `"x_2"`

| Etichetta | Operatore | Canale | Riga Formschema |
|-----------|-----------|--------|-----------------|
| 1010 — Operator_1_Left | 1° Assistent Mikrophonaufnahme | sinistro | Kanal I |
| 1011 — Operator_1_Right | 1° Assistent Mikrophonaufnahme | destro | Kanal II |
| 1012 — Operator_2_Left | 2° Assistent Rückkopplung | sinistro | Kanal I |
| 1013 — Operator_2_Right | 2° Assistent Rückkopplung | destro | Kanal II |
| 1014 — Operator_3_Left | 3° Assistent Wiedergabe | sinistro | Lautsprecher I |
| 1015 — Operator_3_Right | 3° Assistent Wiedergabe | destro | Lautsprecher II |

### Struttura per periodo (1010–1013)

Per ciascuno dei 51 periodi:

| Attributo | Tipo |
|-----------|------|
| `on` | booleano |
| `perforazioni` | intero |
| `number_semantics` | enum: `PERFORATION` \| `OMISSION` |
| `distribution` | enum: `AD_LIB` \| `ACCEL` \| `RIT` \| `ACCEL_RIT` |
| `duration_s_stated` | decimale |
| `open_offset_s_stated` | decimale |
| `approx` | booleano |

### Struttura per periodo (1014–1015)

Per ciascuno dei 51 periodi:

| Attributo | Tipo |
|-----------|------|
| `on` | booleano |
| `sovrapposizioni` | intero |
| `envelope` | stringa line~ |
| `forma_derivata` | enum derivato |

---

## 1016 — Operator_Card

Scheda statistica aggregata dell'attività di un singolo operatore su un singolo canale nell'intera versione.

- **Tipo geometrico:** rettangolo (intera riga dell'operatore)
- **Attributi:**

| Attributo | Tipo | Note |
|-----------|------|------|
| `versione` | enum I–VI | |
| `operatore` | enum 1 \| 2 \| 3 | |
| `canale` | enum `left` \| `right` | |
| `funzione` | enum | `mikrophonaufnahme` \| `rückkopplung` \| `wiedergabe` |
| `periodi_attivi_totali` | intero | |
| `periodi_inattivi_totali` | intero | |
| `perforazioni_totali` | intero | null per operatore 3 |
| `perforazioni_media_per_periodo` | decimale | null per operatore 3 |
| `perforazioni_massimo` | intero | null per operatore 3 |
| `perforazioni_minimo` | intero | null per operatore 3 |
| `sezione_piu_attiva` | enum A–F | |
| `sezione_meno_attiva` | enum A–F | |
| `periodi_consecutivi_attivi_max` | intero | |
| `periodi_consecutivi_inattivi_max` | intero | |

---

## Evento derivato: cambio_testina

Ad ogni confine tra sezioni il sistema di registrazione richiede un cambio di testina di playback. Esportato come evento derivato nel JSON.

| Attributo | Tipo | Note |
|-----------|------|------|
| `separatore` | stringa | es. `"A\|B"` |
| `sezione_successiva` | enum B–F | |
| `presente` | booleano | |
| `ritardo_secondi` | decimale | null se non presente |
| `coincide_con_separatore` | booleano | true se ritardo = 0 |
| `periodo_derivato` | intero | periodo in cui cade il cambio |
| `frazione_nel_periodo` | decimale 0–1 | |
| `tempo_assoluto_secondi` | decimale | |

---

## 1017 — Speaker_Operator_3_Actions

> ⚠️ **In fase di sviluppo attivo.** I vocabolari di `action_class`, `speed_profile` e `notation_carrier` sono stati censiti sistematicamente su tutte e sei le versioni ma potrebbero richiedere revisione durante la fase di annotazione.

Istruzioni una tantum del 3° Assistent (Wiedergabe) che non rientrano nella struttura periodica regolare.

- **Tipo geometrico:** punto sull'istruzione nel Formschema

| Attributo | Tipo | Valori |
|-----------|------|--------|
| `versione` | enum | I–VI |
| `sezione` | enum | A–F |
| `period_span` | stringa | periodo o intervallo di riferimento |
| `channel` | enum | `LS_I` \| `LS_II` \| `BOTH` |
| `action_class` | enum | `SPAT_ALT` \| `DYN` \| `ECHO` \| `INS` \| `ACC` \| `DUR` \| `MODE` |
| `speed_profile` | enum | `VIELE` \| `SCHNELL` \| `LANGSAM` \| `RIT` \| `SYNC` \| `FREE` \| `NA` |
| `count` | intero | null se `indeterminate` è true |
| `indeterminate` | booleano | true quando il numero di occorrenze non è specificato |
| `group_id` | intero | raggruppa eventi correlati; null se non applicabile |
| `duration_s` | decimale | null se non specificata |
| `dynamics` | enum | `F` \| `P` \| `PPP` \| `AD_LIB` \| `NA` |
| `notation_carrier` | array di enum | `TEXT` \| `ARROW` \| `DYN_SIGN` \| `HATCH_DENSE` \| `DASHED_BOX` \| `BAR_PATTERN` \| `DIAMOND` \| `MULTIPLIER` \| `DURATION_TEXT` \| `FOOTNOTE_REF` \| `TN_REF` \| `CIRCLED_MARK` |
| `tn_ref` | stringa | riferimento al t-numero dell'Interpretation Schema: `NONE` \| `NOTE_1` \| `t2`–`t12` |
| `source_text` | stringa | trascrizione letterale del testo originale tedesco |
| `verify_flag` | booleano | segnala annotazioni da verificare |

---

## 1018 — Interpretation_Icon

Icona dell'Interpretations-Schema, posizionata esattamente sull'elemento grafico nell'immagine.

- **Tipo geometrico:** punto

| Attributo | Tipo | Valori |
|-----------|------|--------|
| `versione` | enum | I–VI |
| `sezione` | enum | A–F |
| `icona_tipo` | enum | `freccia_giu` \| `freccia_loop_avanti` \| `freccia_loop_indietro` \| `freccia_bidirezionale` \| `freccia_su` \| `punto` \| `tilde` \| `croce` \| `croce_doppia` \| `L` \| `F` \| `gamma` \| `L_gamma` |
| `riferimento_istruzione` | stringa | paragrafo del manuale: `"5.1"`, `"5.2"`, ecc. |
