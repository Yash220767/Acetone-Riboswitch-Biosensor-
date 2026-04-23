# Synthetic Biology-Based Wearable Patch for Non-Invasive Volatile Organic Compound Detection in Diabetes Mellitus

**MIT Media Lab — How to Grow (Almost) Anything 2025**  
**Individual Final Project | Yash Sawant**

---

## Abstract

Diabetic ketoacidosis (DKA) is a life-threatening complication of diabetes mellitus characterised by elevated ketone body concentrations, including acetone, in blood, urine, breath, and sweat. Current monitoring methods are invasive, requiring frequent blood draws, and demand continuous user input. This project proposes a synthetic biology-based approach to overcome these limitations through the design of an acetone-responsive riboswitch circuit embedded in a wearable patch format.

The central hypothesis is that acetone, like conventional small-molecule inducers, can function as a ligand by binding to a rationally designed aptamer sequence, triggering a conformational change in the riboswitch and activating downstream gene expression (GFP reporter). Computational validation was performed using molecular docking (SwissDock/AutoDock Vina), RNA secondary structure prediction (RNAfold), and structural visualisation (PyMOL). Benchling was used for genetic circuit design.

---

## Table of Contents

1. [Background](#background)
2. [Project Aims](#project-aims)
3. [Experimental Design](#experimental-design)
4. [Results](#results)
5. [Discussion](#discussion)
6. [Future Work](#future-work)
7. [Tools and Technologies](#tools-and-technologies)
8. [References](#references)

---

## Background

### Diabetes and Diabetic Ketoacidosis

Diabetes mellitus is a chronic metabolic disorder caused by insufficient insulin production or impaired insulin utilisation. Hyperglycemia, if left untreated, leads to catastrophic damage to neurological and vascular systems. In insulin-deficient states, the body shifts to fatty acid catabolism, producing ketone bodies — including acetone, acetoacetate, and beta-hydroxybutyrate — at elevated concentrations. Diabetic ketoacidosis (DKA) occurs when ketone accumulation leads to systemic acidosis, a potentially fatal condition.

Acetone is a volatile organic compound (VOC) emitted passively through breath and sweat, and its concentration correlates directly with blood beta-hydroxybutyrate levels in diabetic patients (Yamane et al., 2006). This makes it a viable non-invasive biomarker for DKA detection.

### Volatile Organic Compounds as Biomarkers

Humans continuously emit VOCs through breath and skin. Studies including the ICHEAR project have demonstrated that VOC emission profiles vary with physiological state, temperature, humidity, and ozone exposure. Elevated acetone in sweat and breath has been directly linked to hyperketonemia in diabetic patients, making it a clinically relevant target for real-time metabolic monitoring.

### Limitations of Current Monitoring Methods

| Method | Type | Limitations |
|---|---|---|
| Blood glucose meters | Invasive | Painful, infection risk, requires sample collection |
| CGM (Continuous Glucose Monitors) | Minimally invasive | Measures glucose only, not ketones |
| Optical/NIR sensors | Non-invasive | Low sensitivity, affected by skin tone and hydration |
| Breath acetone analysers | Non-invasive | Not wearable, requires active user input |

Current non-invasive approaches suffer from low sensitivity to trace biomarkers, susceptibility to environmental interference, and poor integration into wearable formats. A synthetic biology-based approach offers biological amplification, modularity, and low-cost scalability.

---

## Project Aims

### Aim 1 — Computational Design and Validation
Develop a synthetic biology gene circuit that detects acetone VOCs from sweat using an aptamer-based riboswitch. Validate computationally using docking simulations, RNAfold structural analysis, and PyMOL visualisation.

**Workflow:**
1. Select ligand (acetone) and aptamer scaffold
2. Retrieve and visualise aptamer structure in PyMOL (PDB: 1ehz)
3. Extract aptamer sequence for riboswitch modelling
4. Design acetone-responsive riboswitch in Benchling
5. Run docking simulations (acetone + aptamer) using SwissDock/AutoDock Vina
6. Analyse binding pockets, conformational changes using PyMOL and RNAfold

### Aim 2 — Experimental Validation and Optimisation
Experimentally confirm acetone binding affinity and validate the predicted conformational change in the riboswitch. Overcome limitations related to small molecule affinity and sensitivity.

**Protocol:**
1. Synthesise DNA construct (T7 promoter – riboswitch – RBS – GFP – T7 terminator)
2. Rehydrate in cell-free TX-TL system
3. Add acetone at varying concentrations; include positive (all components) and negative (no acetone) controls
4. Observe and measure GFP fluorescence
5. Analyse signal vs. acetone concentration

**Confirmation techniques:**
| Method | Expected Outcome |
|---|---|
| Native PAGE | Mobility shift indicating ligand-induced folding change |
| NMR Spectroscopy | Atomic-level conformational change upon binding |
| Circular Dichroism (CD) | Base stacking / helicity changes in response to binding |
| EMSA | Structural shifts upon ligand binding |
| SHAPE / In-line probing | Mapping of structural flexibility changes |

### Aim 3 — Wearable Integration and Real-Time Monitoring

**Aim 3.1 — Scalability**
Optimise for mass production, standardisation, safety, and cost-effectiveness to maximise societal impact across socioeconomic demographics.

**Aim 3.2 — Smartphone Interface**
Integrate the biosensor into a textile patch coupled to a smartphone interface for real-time VOC monitoring.

Hardware components required:
- BLE (Bluetooth Low Energy) microcontroller
- Silicone elastomer sensor wells
- CMOS optical detector
- Polymer optical fiber (POF)
- Smartphone app for real-time acetone level display and threshold alerts

---

## Experimental Design

### Step 1 — Ligand and Aptamer Selection

- **Target ligand:** Acetone (SMILES: `CC(=O)C`)
- **Aptamer scaffold:** Yeast tRNA phenylalanine (*Saccharomyces cerevisiae*, PDB: 1ehz) — selected for structural stability as an RNA scaffold

Acetone molecular structure (MOL2 format):
```
Atoms: C1, C2 (carbonyl), C3, O1 (carbonyl oxygen)
Bond: C2=O1 (double bond, carbonyl)
Partial charges: C2 (+0.1284), O1 (-0.3021)
```

### Step 2 — Structural Visualisation in PyMOL

Structures visualised:
- Yeast tRNA phenylalanine (PDB: 1ehz) — showing anticodon stem, D-stem, T-stem, and four-way junction
- Acetone molecule in PDB format for docking
- Potential binding pockets on tRNA surface identified using PyMOL cavity detection

### Step 3 — Aptamer Sequence Extraction

Observed residues at potential binding region (extracted via PyMOL):

```
7U, 8U, 9A, 10G, 11C, 21A, 26G, 45G, 46G, 47U, 48C, 49C, 50U, 66A, 67A
```

Derived aptamer sequence for Benchling riboswitch design:
```
5'-TTTGTAGAGTCTTAA-3'
```

### Step 4 — Riboswitch Design in Benchling

Full Benchling construct sequence (788 bp):
```
TTGACAGCTAGCTCAGTCCTAGGTATAATGCTAGCTTTGTAGAGTCTTAAAGGAGGATGGTGAGCAAGGGCGAGGAGCT
```

Circuit logic:
- **Without acetone:** Aptamer folds → RBS sequestered → Translation **OFF**
- **With acetone:** Acetone binds aptamer → Conformational change → RBS exposed → Translation **ON** → GFP expressed → Fluorescence detected

Benchling sequence: [View circuit design](https://benchling.com/s/seq-7bCvdBNVNhtjbsfa8DGx?m=slm-jmkLTfTcrH412Xh4kimf)

### Step 5 — Molecular Docking (SwissDock / AutoDock Vina)

**Receptor:** Yeast tRNA phenylalanine (PDB: 1ehz)  
**Ligand:** Acetone (converted to PDB format from SMILES)  
**Software:** SwissDock (AutoDock Vina backend)

### Step 6 — RNAfold Structural Analysis

Used RNAfold (Vienna RNA package) to:
- Predict minimum free energy (MFE) secondary structures with and without acetone
- Assess positional entropy across the riboswitch sequence
- Compare centroid secondary structures to identify conformational changes at the RBS region

---

## Results

### 1. Molecular Docking Results

| Model | Calculated Affinity (kcal/mol) |
|---|---|
| 1 | -2.428 |
| 2 | -2.109 |
| 3 | -2.086 |
| 4 | -2.005 |
| 5 | -1.756 |
| 6 | -1.721 |
| 7 | -1.397 |
| 8 | -1.379 |
| 9 | -1.375 |
| 10 | -1.330 |
| 11 | -1.066 |

**Best docking affinity: -2.428 kcal/mol**

While modest, this binding energy is consistent with expected affinities for small volatile organic compounds interacting with RNA aptamer scaffolds. Acetone docked into a defined pocket near the four-way junction of the tRNA structure.

### 2. RNAfold Secondary Structure Prediction

| Condition | MFE (kcal/mol) | Structural Observation |
|---|---|---|
| Without Acetone | -276.40 | Stable, well-folded conformation; RBS sequestered; low positional entropy |
| With Acetone | -253.61 | Partial unfolding of aptamer domain; RBS exposed; increased positional entropy |

**MFE shift: +22.79 kcal/mol** upon acetone binding — reflects destabilisation of the aptamer fold consistent with RBS exposure and translational activation.

**Key observations:**
- Positional entropy increased significantly around the aptamer domain upon acetone binding
- RBS region showed greater structural variability with acetone present
- Centroid secondary structures showed clear topological differences between bound and unbound states
- All findings are consistent with the riboswitch activation hypothesis

---

## Discussion

### Interpretation

Docking simulations confirm acetone interaction with the aptamer scaffold at a defined binding pocket. The best binding energy of -2.428 kcal/mol, while lower than typical protein-small molecule interactions, is appropriate for a small VOC (MW = 58.08 g/mol) interacting with an RNA structure.

RNAfold analysis strongly supports the riboswitch design logic. The MFE shift from -276.40 to -253.61 kcal/mol upon acetone binding reflects structural loosening of the aptamer, with increased entropy at the RBS site — consistent with translational derepression.

### Limitations

1. **Acetone binding affinity** — Small molecular size and low polarity make high-affinity aptamer binding inherently challenging. Modified binding pockets or signal amplification strategies may be required.
2. **In silico vs in vitro discrepancy** — Environmental factors (hydration, molecular crowding, ionic strength) not captured in computational models may alter real binding behaviour.
3. **Aptamer specificity** — Selectivity for acetone over structurally similar VOCs (e.g., ethanol, isopropanol) requires experimental validation.
4. **tRNA scaffold** — Using tRNA phenylalanine as an aptamer scaffold is a simplification; a SELEX-derived aptamer specific to acetone would be more appropriate for experimental follow-up.

### Significance

If the computational predictions hold experimentally, this system would represent the first riboswitch-based wearable biosensor for acetone VOC detection — advancing both synthetic biology applications in diagnostics and non-invasive diabetes monitoring.

---

## Future Work

1. **Aptamer optimisation** — SELEX rounds in sweat-like conditions to identify higher-affinity acetone-binding sequences
2. **Experimental validation** — Cell-free TX-TL system with GFP reporter to confirm riboswitch functionality
3. **Aptamer engineering** — Systematic mutagenesis around the binding region with functional screening
4. **Wearable integration** — Embedding sensor in textile patch with BLE microcontroller and smartphone interface
5. **Clinical validation** — Mock trials with lab models and human volunteers for standardisation

---

## Tools and Technologies

| Tool | Purpose |
|---|---|
| PyMOL | Structural visualisation of tRNA and acetone; binding site identification |
| SwissDock / AutoDock Vina | Molecular docking simulations |
| RNAfold (Vienna RNA) | RNA secondary structure prediction and entropy analysis |
| Benchling | Genetic circuit design (riboswitch construct) |
| RCSB PDB | Structural data retrieval (PDB: 1ehz) |
| UniProt | Protein/RNA sequence databases |
| BioRender | Scientific figure creation |

---

## References

1. Yamane, N., Tsuda, T., Nose, K., Yamamoto, A., Ishiguro, H., & Kondo, T. (2006). Relationship between skin acetone and blood beta-hydroxybutyrate concentrations in diabetes. *Clinica Chimica Acta*, 365(1-2), 325–329. https://doi.org/10.1016/j.cca.2005.09.016

2. Owen, O. E., Trapp, V. E., Skutches, C. L., Mozzoli, M. A., Hoeldtke, R. D., Boden, G., & Reichard, G. A. (1982). Acetone metabolism during diabetic ketoacidosis. *Diabetes*, 31(3), 242–248. https://doi.org/10.2337/diab.31.3.242

3. Nguyen, P. Q., Soenksen, L. R., Donghia, N. M. et al. (2021). Wearable materials with embedded synthetic biology sensors for biomolecule detection. *Nature Biotechnology*, 39, 1366–1374. https://doi.org/10.1038/s41587-021-00950-3

4. Eberhardt, J., Santos-Martins, D., Tillack, A. F., & Forli, S. (2021). AutoDock Vina 1.2.0: New docking methods, expanded force field, and Python bindings. *Journal of Chemical Information and Modeling*, 61(8), 3891–3898. https://doi.org/10.1021/acs.jcim.1c00203

5. Sharma, A., Badea, M., Tiwari, S., & Marty, J. L. (2021). Wearable Biosensors: An Alternative and Practical Approach in Healthcare and Disease Monitoring. *Molecules*, 26(3), 748. https://doi.org/10.3390/molecules26030748

6. Xu, W., Zou, X., Ding, H. et al. (2023). Rapid and non-invasive diagnosis of type 2 diabetes through sniffing urinary acetone by proton transfer reaction mass spectrometry. *Talanta*, 263, 124265. https://doi.org/10.1016/j.talanta.2023.124265

7. Gaikwad, A., Gauns, S., Borkar, M., Rodrigues, R., & Raykar, S. (2024). Comparative analysis of invasive and non-invasive methods for blood sugar measurement. *International Journal of Creative Research Thoughts (IJCRT)*, 12(4). https://ijcrt.org/papers/IJCRT24A4706.pdf

---

*This project was completed as part of MIT Media Lab's How to Grow (Almost) Anything (HTGAA) 2025 programme.*
