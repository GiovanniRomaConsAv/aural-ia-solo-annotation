# Dominio del Manuale — 3000–3099

---

## Strategia di trattamento

Le 22 pagine del manuale di *Solo* non vengono annotate in CVAT ma trattate come **corpus multimodale strutturato** destinato alla segmentazione diretta per il sistema RAG.

Le illustrazioni inline — diagrammi tecnici, esempi di sovrapposizione, figure delle perforazioni — sono parte integrante del contenuto semantico di molti paragrafi e non separabili dal testo che le accompagna.

---

## Segmentazione

La segmentazione avviene per **unità di paragrafo numerato**, seguendo la gerarchia della numerazione originale di Stockhausen:

| Tipo | Esempi |
|------|--------|
| Paragrafi con cerchio latino | `a`, `b`, `c` |
| Paragrafi con numero circolare | `1`, `2`, `3`, `5.1`, `5.2`, `5.3`, `5.4`, `5.5` |
| Paragrafi tecnici alfanumerici | `x_1`, `x_2`, `y`, `z` |

Il processing avviene tramite strumenti multimodali (LlamaIndex, LlamaParse o equivalenti) che estraggono simultaneamente testo e immagini inline per ogni pagina, associandoli per prossimità spaziale.

---

## Struttura del chunk

```json
{
  "id": "x_2",
  "testo": "In every FORM SCHEME there is a FEEDBACK SCHEME...",
  "immagini": ["schematic_x2.png"],
  "descrizione_immagine": "Diagramma schematico del sistema di feedback...",
  "pagina": 15
}
```

La descrizione visiva viene prodotta da un modello multimodale durante la fase di indicizzazione (**vision-augmented indexing**): il chunk è recuperabile tramite ricerca testuale sulla descrizione, non solo sul testo originale.

---

## Meccanismo di correlazione

La chiave numerica del paragrafo (es. `"x_2"`, `"5.1"`) è la stessa che compare nell'attributo `riferimento_istruzione` delle etichette CVAT del Formschema e della partitura. Questa corrispondenza è il meccanismo di correlazione tra annotazioni visive e corpus del manuale nel RAG.

---

## 3000 — Manual_Schematic_Diagram

Diagramma tecnico del manuale che per dimensioni o complessità richiede annotazione CVAT separata oltre alla descrizione automatica.

- **Tipo geometrico:** rettangolo (intero diagramma)

| Attributo | Tipo | Valori |
|-----------|------|--------|
| `tipo` | enum | `feedback_schema` \| `staging_schema` \| `superimposition_example` \| `perforation_example` |
| `pagina_manuale` | intero | |
| `riferimento_istruzione` | stringa | |

---

## 3001 — Manual_Diagram_Element

Elemento singolo all'interno di un diagramma tecnico — componente identificabile come unità semantica autonoma.

- **Tipo geometrico:** rettangolo sul componente

| Attributo | Tipo | Valori |
|-----------|------|--------|
| `tipo_componente` | enum | `microphone` \| `recorder` \| `playback_head` \| `feedback_channel` \| `loudspeaker` \| `potentiometer` \| `switch` |
| `canale` | enum | `I` \| `II` \| `none` |
| `riferimento_istruzione` | stringa | |
