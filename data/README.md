# Data

`corpus.csv` contains the 2,240 Chinese Essen pieces with usable musical features.
`heptatonic.csv` contains the 219 manually annotated pieces used for mode analysis.
Join the tables on `name`. Both files are UTF-8 CSVs with one piece per row.
Blank metadata cells indicate missing information.

## Sources and preparation

The source scores belong to the [Chinese portion of the Essen Folksong Collection](https://kern.humdrum.org/cgi-bin/ksbrowse?l=/essen/asia/china).
Each `source_url` identifies a collection folder; `name` identifies the score within it.
The source records credit Helmut Schaffrath and carry the copyright notice of his estate.

The musical features come from the project's `processed_fulldata.csv`.
Duration-weighted pitch profiles summarize measured note events in the first
part, using quarter-note duration units and omitting rests and chords.
Pitch durations were summed without octave distinctions and divided by the
piece's total note duration. The unusable zero-note record `han0953.krn` is omitted.

The 219 manual *diao* and *diao-tou* assignments and their model profiles come from
`heptatonic_annotation.csv`. Province assignments incorporate the geographical
corrections in `shanxi_patch.csv`. Four annotated pieces have an ambiguous province
label.

Title, genre, meter and ethnic-group text are decoded from the
source metadata using CP437. Source references, source-family classifications
and recording indicators follow the project's metadata audit.

## `corpus.csv`

| Field | Meaning |
|---|---|
| `name` | Stable source filename, including `.krn`. |
| `source_folder`, `source_url` | Original collection folder and its public catalogue URL. |
| `title` | Title from the source `OTL` record. |
| `province` | Corrected province. `Shanxi_` marks an unresolved assignment between Shanxi and Shaanxi. |
| `province_status` | `resolved`, `ambiguous`, or `missing`. |
| `genre` | Complete source `AGN` text, including multiple descriptors. Commas, periods and semicolons separate the recorded tags. |
| `genre_broad` | Broad classification of the leading genre label with spelling aliases normalized. |
| `ethnic_group` | Complete ethnic-group label from an ordinary source comment, including multiple labels where present. |
| `meter` | Source `AMT` metric classification, such as `simple duple`. |
| `source_reference` | Source citation text recovered between the geographical-origin and catalogue records. |
| `source_family` | Source siglum or named source family from the citation text. |
| `own_recording` | Whether an ordinary source comment contains `Eigene Aufnahme` (“own recording”). |
| `note_count` | Number of extracted note events. |
| `unique_pitch_class_count` | Number of distinct pitch classes represented in the profile. |
| `source_tonic_pitch_class` | Tonic pitch class from the source’s first explicit Humdrum key declaration, with C = 0 through B = 11. This is the reference used to transpose the corpus profile to C. |
| `pc_0` … `pc_11` | Duration proportions after transposing the declared tonic to C. The 12 values sum to 1. |

For example, a source declaration of F has `source_tonic_pitch_class = 5`.
Corpus pitch classes are expressed as `(source_pitch_class - source_tonic_pitch_class) % 12`,
so F becomes C. The `pc_0` … `pc_11` columns contain the resulting duration proportions.
The key signature records sharps or flats; this field records the declared tonic.
The source tonic and the manual *gong* assignment are separate annotations.
Source-family placeholders `[missing source]` and `[unknown: NN]` distinguish
absent and explicitly unknown source citations.

## `heptatonic.csv`

| Field | Meaning |
|---|---|
| `name` | Source filename linking to `corpus.csv`. |
| `diao` | Manual category: `xiazhi`, `zhengsheng`, or `qingshang`. Counts are 156, 52 and 11, respectively. |
| `gong_pc` | Annotated *gong* in the common diatonic reference: 0 for *xia zhi*, 5 for *zheng sheng*, and 7 for *qing shang*. |
| `diao_tou` | Manual final-tone category: `gong`, `shang`, `jue`, `zhi`, or `yu`. These correspond to annotation codes 1–5. |
| `pc_0` … `pc_11` | Duration proportions in the common diatonic reference, whose pitch-class set is C, D, E, F, G, A, B (0, 2, 4, 5, 7, 9, 11). The 12 values sum to 1. |

The two tables use different reference transpositions. The mode analysis uses
the profiles in `heptatonic.csv`; the notebook applies random transpositions
before inference.
