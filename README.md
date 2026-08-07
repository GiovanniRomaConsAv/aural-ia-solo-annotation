# Aural-ia — Solo Nr. 19 Annotation

Supplementary materials for the paper:

**"From Object to Relation: Annotating Semantic Instability 
in Stockhausen's Solo (Nr. 19)"**  
Giovanni Roma, Alba Francesca Battista  
CIM 2026 — XXV Colloquio di Informatica Musicale, L'Aquila

---

## Contents

### `formschema_trascrizione.html`
Browser-based transcription tool for the Formschema domain 
of Stockhausen's Solo. Open in any modern browser — no 
installation required. Enforces controlled vocabularies, 
validates in real time, and exports typed JSON with 
`riferimento_istruzione` field linking every annotation to 
its source paragraph in Stockhausen's performance instructions.

### `formschema_version_IV.json` *(coming soon)*
Complete Formschema annotation export for Version IV, 
produced by the transcription tool. Version IV is provided 
as the sample because its cycle A activates the OMISSION 
semantic resolution, directly demonstrating the semantic 
instability mechanism described in the paper.

### `Manuale_Etichette_Solo.pdf`
Annotation label manual (in Italian). Defines all label 
categories, controlled vocabularies, attribute types, and 
decision criteria for the four annotation domains: 
Editorial, Formschema, Score, and Manual. Designed to 
ensure consistency across independent annotators and to 
serve as the primary methodological reference for dataset 
construction.


---

## How to use the transcription tool

1. Open `formschema_trascrizione.html` in a browser
2. Select a version (I–VI) from the dropdown
3. Fill in the 51-period grid for each operator channel
4. Use **Esporta JSON** to download the typed export
5. Use **Salva lavoro** / **Riprendi lavoro** to save and reload sessions
6. Consult `annotation_agreement_manual.pdf` for label 
   definitions and decision criteria before annotating

---

## Citation

*(to be updated after publication)*

---

## License

CC BY 4.0
