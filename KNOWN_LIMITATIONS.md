# Status and known limitations

This tool is a research prototype under active development. It is the
working instrument with which the Formschema domain of the dataset is
being transcribed, and it was released at this stage to accompany the
CIM 2026 paper *From Object to Relation: Annotating Semantic Instability
in Stockhausen's Solo (Nr. 19)*. It is not a finished product: the schema
and the interface are being refined iteratively as transcription surfaces
notational cases not covered by the initial design.

## Known limitations of this release (v0.3-alpha)

- **Perforation timing (Formschema IV and V).** The schema does not yet
  cover the timing indications that Formschema versions IV and V associate
  with perforation events. A dedicated field will be added in a later
  release. Exports of Version I are unaffected.

- **Third-operator event sequence.** Third-operator events (e.g. channel
  swap) are recorded per period as an *unordered set*: the export documents
  *which* events occur within a period, but not yet their chronological
  sequence within it. Where a period contains more than one third-operator
  event, their order must currently be read from the Formschema page. In
  the exported array the order of elements is **not** significant. A
  tile-based, sequenced representation aligned with the other operators is
  planned for a later release. <!-- opzionale: "In Version I this affects N of the 51 periods." -->

- **Single annotator.** Transcription is currently performed by a single
  annotator; inter-annotator agreement has not yet been measured (see
  paper, Section 4). The triple-level verification structure guarantees
  internal consistency, not inter-subjective reliability.

## Roadmap

Later versions of the tool and additional Formschema exports (Versions
II–VI) will be released under the same concept DOI, so that the citation
in the paper always resolves to the latest version:

<https://doi.org/10.5281/zenodo.21837959>
