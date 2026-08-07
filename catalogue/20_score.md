# Dominio della Partitura — 2000–2999

---

## La cellula semiotica indivisibile

L'unità di annotazione è il **modulo** — il segmento di notazione delimitato dagli spezzabattuta. Il termine adottato in questo sistema è **cellula semiotica indivisibile**.

Lo spezzabattuta in *Solo* non è una stanghetta convenzionale ma un confine procedurale dichiarato da Stockhausen nel regolamento: il modulo è l'elemento minimo che l'esecutore seleziona, taglia, incolla, ripete e combina nella costruzione di una versione.

La granularità della nota singola è deliberatamente esclusa per due ragioni:

1. **Musicologica** — i gesti musicali di *Solo* hanno senso come unità globali. Un glissando non è una successione di altezze: scomporlo in note singole distrugge l'informazione.
2. **Computazionale** — i modelli preaddestrati possiedono già il vocabolario musicale. L'annotazione deve ancorarli alla struttura specifica di *Solo*, non ridefinire il vocabolario.

---

## Struttura gerarchica

```
pagina (P_1–P_6)
  └── sistema
        └── rigo (timbro: N, I, II, III)
              └── modulo (cellula semiotica indivisibile)
```

Le sei pagine di notazione sono identificate con **P_1–P_6** in base all'ordine fisico dei fogli nella partitura pubblicata da Universal Edition (UE 14789).

> ⚠️ L'ordine P_1–P_6 sarà confermato definitivamente con la scansione HD della partitura originale.

---

## 2000 — Score_Page

- **Tipo geometrico:** rettangolo (intera pagina)

| Attributo | Tipo | Valori |
|-----------|------|--------|
| `id_pagina` | enum | `P_1` \| `P_2` \| `P_3` \| `P_4` \| `P_5` \| `P_6` |
| `numero_sistemi` | intero | |

---

## 2001 — System

- **Tipo geometrico:** rettangolo (intero sistema)

| Attributo | Tipo |
|-----------|------|
| `id_pagina` | enum P_1–P_6 |
| `numero_sistema_nella_pagina` | intero |
| `numero_righi` | intero |

---

## 2002 — Staff

- **Tipo geometrico:** rettangolo (singolo rigo)

| Attributo | Tipo | Valori |
|-----------|------|--------|
| `id_pagina` | enum | P_1–P_6 |
| `numero_sistema` | intero | |
| `timbro` | enum | `N` \| `I` \| `II` \| `III` |
| `posizione_nel_sistema` | intero | ordine dall'alto |

---

## 2003 — Module

La cellula semiotica indivisibile — il segmento di notazione delimitato dagli spezzabattuta.

- **Tipo geometrico:** rettangolo sul modulo nel rigo

| Attributo | Tipo | Valori / Note |
|-----------|------|---------------|
| `id_pagina` | enum | P_1–P_6 |
| `numero_sistema` | intero | |
| `timbro_iniziale` | enum | `N` \| `I` \| `II` \| `III` |
| `cambio_timbro` | booleano | |
| `timbro_finale` | enum | `N` \| `I` \| `II` \| `III` \| `none` — compilato solo se `cambio_timbro` è true |
| `posizione_cambio_timbro` | enum | `inizio` \| `meta` \| `fine` \| `none` |
| `indicazione_testuale` | stringa | trascrizione letterale; campo vuoto se assente |
| `dinamica_iniziale` | enum | `ppp` \| `pp` \| `p` \| `mp` \| `mf` \| `f` \| `ff` \| `none` |
| `dinamica_finale` | enum | `ppp` \| `pp` \| `p` \| `mp` \| `mf` \| `f` \| `ff` \| `none` |
| `tipo_notazione` | enum | `misurata` \| `proporzionale` \| `mista` |
| `riferimento_istruzione` | stringa | paragrafo del manuale pertinente |

### Nota sul campo `indicazione_testuale`

Il vocabolario delle indicazioni testuali nelle sei pagine di *Solo* è ampio, variabile e include combinazioni non riducibili a un menu chiuso (VIBR. LANGSAM, VIBR. SCHNELL, VIBR. MASSIG, ACCEL., RIT., ETWAS GERÄUSCHHAFT, SEHR GERÄUSCHHAFT, GLISS., ecc.). 

La scelta del campo testuale aperto con trascrizione fedele è metodologicamente preferibile a un enum incompleto. La consistenza tra annotatori è garantita dalla norma della **trascrizione letterale**: ogni annotatore trascrive esattamente ciò che legge in partitura, comprese abbreviazioni e punteggiatura originali, senza normalizzazioni.
