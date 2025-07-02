# RNA Structural Bioinformatics

This collection of Jupyter notebooks provides end-to-end pipelines for parsing, analyzing and comparing RNA structures. Each notebook guides you through raw data ingestion, manual quality checks, automated processing and final result summaries.

---

## Notebook 1: Dot-Bracket ↔ BPSEQ Conversion & Structural Element Extraction  
Transform secondary-structure strings between dot-bracket and BPSEQ formats, with built-in detection of key motifs.  
- **Data I/O & manual inspection**  
  - Scan a folder of dot-bracket files, visually verify sequence–structure correspondence and flag any misformatted entries by hand.  
  - After conversion, spot-check a handful of BPSEQ outputs to ensure pairing conventions were preserved.  
- **Bidirectional conversion pipeline**  
  - Convert dot-bracket to BPSEQ by mapping each bracket pair to index–base lines.  
  - Reconstruct dot-bracket from BPSEQ via a nesting-aware bracket-assignment routine, resolving conflicts with a first-come-first-served strategy.  
- **Secondary-structure feature finding**  
  - Automatically identify hairpin loops, contiguous stems and unpaired single-strand regions, then manually curate borderline cases.  
- **Batch processing & summary**  
  - Process entire directories in one run, generate per-file reports listing counts of loops, stems and singles, and compile a master summary table.

---

## Notebook 2: Dot-Bracket Pair Extraction & Structure Comparison Metrics  
Extract base-pair lists from dot-bracket notation and quantify structural similarity.  
- **Pair parsing & conflict resolution**  
  - Read dot-bracket strings line by line, build zero-based pairing lists, and manually inspect any ambiguous or overlapping assignments.  
- **Similarity metric computation**  
  - Compute Interaction Network Fidelity between two pairing sets and calculate edit distances on the dot-bracket strings.  
  - Hand-verify a few example pairs to confirm the INF denominator and distance algorithm behave as expected.  
- **Demonstration on example structures**  
  - Run the metrics on reference vs. predicted structures, print tabulated INF scores and Levenshtein distances, and highlight cases where manual realignment was needed.

---

## Notebook 3: RNA Motif Search in Dot-Bracket Structures  
Scan sequence-structure files for common tetraloops and T-loops using pattern matching.  
- **Pattern setup & tuning**  
  - Define motif descriptors (e.g. GNRA, UNCG, T-loop) via IUPAC‐style patterns, tweak regex heuristics by hand to avoid false positives.  
- **Data loading & JSON I/O**  
  - Read combined sequence + structure inputs, output motif→match positions in JSON, and manually inspect a subset of matches to refine patterns.  
- **Loop-region scanning logic**  
  - Restrict searches to predicted loop segments, then apply each pattern sequentially and record start/end indices.  
- **Results aggregation**  
  - Merge per-file JSON outputs into a summary report of motif frequencies across the dataset.

---

## Notebook 4: PDB-Based G–C Base-Pair Detection  
Use Biopython to parse PDB files and find G–C pairs by geometric criteria.  
- **Structure parsing & distance thresholding**  
  - Load PDBs, iterate nucleotide residues, compute N1(G)–N3(C) distances, and manually adjust the cutoff to capture canonical pairs without spurious hits.  
- **Optional scoring normalization**  
  - Offer a cosine-based distance norm for advanced filtering, with hand-tuned weight factors to downplay borderline cases.  
- **Batch execution & output files**  
  - Walk through a folder of PDBs, write `<basename>_pairs.txt` with residue index pairs, and compile a summary of total G–C counts per structure.

---

## Notebook 5: RMSD, Superposition & Torsion-Angle Comparison for RNA PDBs  
Align two RNA structures and quantify both spatial and angular deviations.  
- **Coordinate extraction & manual atom selection**  
  - Extract phosphorus (P) atom coordinates from each PDB, inspect a few alignments by eye to confirm matching residue ordering.  
- **Structural superposition & RMSD calculation**  
  - Perform optimal superposition using the Kabsch algorithm to align P atom sets, compute root-mean-square deviation (Å), and validate results on test pairs.  
- **Torsion-angle (MCQ) computation**  
  - Compute backbone β, γ and δ angles for each residue, calculate circular differences, and average them to yield the MCQ metric (degrees).  
- **Validation & summary reporting**  
  - Confirm equal residue counts, print out RMSD, superposition transformations and MCQ values.
