# Aural-ia — Solo Nr. 19 Annotation

Supplementary materials for the paper:

**"From Object to Relation: Annotating Semantic Instability 
in Stockhausen's Solo (Nr. 19)"**  
Giovanni Roma, Alba Francesca Battista  
CIM 2026 — XXV Colloquio di Informatica Musicale, L'Aquila

---

## Repository Structure

### `/catalogue/`
Label taxonomy for the four annotation domains.

- `00_editorial.md` — Editorial domain labels and attributes
- `10_formschema.md` — Formschema domain labels, controlled vocabularies, and verification rules
- `20_score.md` — Score domain labels and module-level annotation criteria
- `30_manual.md` — Manual domain labels for performance instruction segmentation

### `/docs/`
Methodological documentation.

- `PRINCIPLES.md` — Foundational epistemological choices and annotation protocol
- `PIPELINE.md` — Technical workflow: CVAT, Docker, Python scripting, JSON export
- `README.md` — This file

### Root
- `formschema_trascrizione.html` — Browser-based transcription tool for the Formschema domain. Open in any modern browser, no installation required. Enforces controlled vocabularies, validates in real time, exports typed JSON with `riferimento_istruzione` field.
- `Manuale_Etichette_Solo.pdf` — Complete annotation label manual (in Italian). Defines all label categories, controlled vocabularies, attribute types, and decision criteria for all four domains.
- `formschema_version_I.json` — Complete Formschema annotation export for Version I, produced by the transcription tool. See KNOWN_LIMITATIONS.md for schema limitations affecting this export.
- `KNOWN_LIMITATIONS.md` — Status of the tool and declared limitations of this release: schema gaps (perforation timing in Formschema IV–V, third-operator event sequence), single-annotator status, and release roadmap. Read before using the exported data.

---

## How to use the transcription tool

1. Open `formschema_trascrizione.html` in a browser
2. Select a version (I–VI) from the dropdown
3. Fill in the 51-period grid for each operator channel
4. Use **Esporta JSON** to download the typed export
5. Use **Salva lavoro** / **Riprendi lavoro** to save and reload sessions
6. Consult `/catalogue/10_formschema.md` for label definitions and decision criteria

---

## Citation

Roma, G., Battista, A.F. (2026). "From Object to Relation: 
Annotating Semantic Instability in Stockhausen's Solo (Nr. 19)." 
In *Proceedings of the XXV Colloquio di Informatica Musicale 
(CIM 2026)*, L'Aquila, October 2026.

**Abstract:** Electroacoustic scores present a specific 
preservation challenge that standard archival approaches do 
not address. If a work is updated to accommodate new technology, 
the revised edition may silently discard the relational layer 
that made it executable, delegating procedural knowledge to an 
external system that subsequently becomes obsolete. The notational 
object survives; the relations that governed it do not, unless 
they were mapped independently of the technology that carried them.

This paper presents a supervised annotation methodology designed 
to capture that relational layer in structured, computationally 
accessible form, applied to two case studies of contrasting 
complexity. The annotation of Jonathan Harvey's *Ricercare una 
melodia* demonstrated that annotation choices already constitute 
a model of the work's operative structure. The extension to 
Stockhausen's *Solo für Melodieinstrument mit Rückkopplung* 
(Nr. 19) introduces *semantic instability* as a core analytical 
concept and identifies the *Spezzabattuta*-delimited parts as 
*projective entities* whose musical identity is activated by the 
governing Formschema rather than fixed in the notation.

The dataset under development is strictly typed and traceable 
to primary analytical sources: a verification record, not an 
interpretation. Conversational, source-grounded access to this 
knowledge through RAG-based inference is a direction for future 
validation; the contribution of the present work is the 
annotation methodology itself.

---

## License

CC BY 4.0
```
