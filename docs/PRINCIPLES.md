# Principi Metodologici

## 1. Quantificabilità sistematica

Ogni attributo di ogni etichetta deve essere esprimibile come valore discreto e verificabile: un intero, un decimale, un booleano, o una selezione da un vocabolario chiuso predefinito. Questo principio si contrappone esplicitamente all'uso di commenti testuali arbitrari, che introducono ambiguità non risolvibili computazionalmente.

Laddove un fenomeno non sia completamente parametrizzabile — come nel caso di certi gesti musicali nella partitura — si adotta un campo testuale semi-controllato con vocabolario dichiarato nel presente manuale.

La scelta di affidarsi a un vocabolario semi-controllato per alcune etichette della partitura è giustificata dalla consapevolezza che i modelli linguistici preaddestrati su cui si basa il sistema RAG possiedono già una comprensione contestuale del vocabolario musicale. Il compito del sistema di annotazione è fornire la conoscenza strutturale specifica e verificabile di *Solo*, non ridefinire da zero il vocabolario musicale.

**Nel dominio del Formschema, ogni attributo è a stabilità computazionale: non esistono campi testuali liberi.**

---

## 2. Ridondanza controllata

Il sistema prevede deliberatamente livelli multipli di annotazione che descrivono la stessa informazione a granularità diverse:

- **Etichetta verticale (Period)** — fotografia dello stato di tutti gli operatori in un singolo periodo
- **Etichette orizzontali (Operator_N_Left/Right)** — sequenza completa dei 51 stati di un singolo operatore su un singolo canale
- **Scheda statistica (Operator_Card)** — aggregati sull'intera versione

Questa ridondanza costituisce uno strumento di validazione interna: se i valori nelle etichette dei singoli periodi non corrispondono ai valori nell'etichetta orizzontale, l'incoerenza è immediatamente rilevabile.

Il principio trova fondamento analitico in Nerenberg (2014), che dimostra come la logica compositiva di *Solo* si articoli simultaneamente su un piano sincronico (periodo per periodo) e diacronico (pattern di sovrapposizione nel tempo).

---

## 3. Distinzione tra stabilità computazionale e trasferibilità cognitiva

| Categoria | Attributi | Funzione |
|-----------|-----------|----------|
| **Stabilità computazionale** | Numerici o a vocabolario chiuso | Ragionamento quantitativo, confronto tra versioni, verifica della coerenza |
| **Trasferibilità cognitiva** | Campi testuali semi-controllati | Sfumature interpretative non parametrizzabili — solo nel dominio della partitura |

---

## 4. La cellula semiotica indivisibile

L'unità di annotazione della partitura è il **modulo** — il segmento di notazione delimitato dagli spezzabattuta. Il termine adottato in questo sistema è **cellula semiotica indivisibile**.

Lo spezzabattuta in *Solo* non è una stanghetta convenzionale ma un confine procedurale dichiarato da Stockhausen nel regolamento: il modulo è l'elemento minimo che l'esecutore seleziona, taglia, incolla, ripete e combina nella costruzione di una versione.

La scelta di non scendere alla granularità della nota singola è supportata da:

1. **Argomento musicologico** — i gesti musicali di *Solo* hanno senso come unità globali. Scomporli in note singole non aggiunge informazione, la distrugge.
2. **Argomento computazionale** — i modelli preaddestrati possiedono già la comprensione del vocabolario musicale. L'annotazione deve ancorare quel vocabolario alla struttura specifica di *Solo*, non ridefinirlo.
