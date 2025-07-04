# Forensic Kinship Project

This repository presents a reproducible, scalable pipeline for SNP-based kinship analysis using the MERLIN simulation engine. It was developed as part of an MSc research project to support forensic applications such as disaster victim identification (DVI), missing person investigations, and familial relationship testing.

The pipeline implements simulations for full siblings (FS), half siblings (HS), and first cousins (FC) using both linked and unlinked marker models. It supports genome-wide simulation (~10,000 SNPs), blind testing on real genotype data, and comparison with existing tools like FamLink.

---

## Directory Structure

```
Forensic_Kinship_Project/
├── 94_SNP_Simulation/                     # Phase 1: Benchmarking (94 SNPs)
│   ├── FS_Simulation/                     # FS scenarios (linked/unlinked) - MERLIN logs, LRs
│   ├── HS_Simulation/                     # HS scenarios (linked/unlinked) - MERLIN logs, LRs
│   ├── FC_Simulation/                     # FC scenarios (linked/unlinked) - MERLIN logs, LRs
│   ├── Original_Input_Files/              # Initial FamLink input files
│   ├── 94_SNP_Comparison/                 # Comparison of MERLIN and FamLink
│   ├── Outputs/                           # All LR outputs, summary stats, plots
│   └── Scripts/                           # Simulations, manipulations, LR and stat calculations, plots
├── 10,000_SNP_Simulation/                 # Phase 2: Genome-wide simulation
│   ├── FS_Simulation/                     # FS scenarios (linked/unlinked) - some MERLIN logs, LRs
│   ├── HS_Simulation/                     # HS scenarios (linked/unlinked) - some MERLIN logs, LRs
│   ├── FC_Simulation/                     # FC scenarios (linked/unlinked) - some MERLIN logs, LRs
│   ├── 10,000SNP_Comparison/              # Comparison with independent replication
│   ├── Outputs/                           # All LR outputs, summary stats, plots
│   ├── Scripts/                           # Simulations, manipulations, LR and stat calculations, plots
│   └── 10,000_SNPs_Input_Files/
│       ├── .ped/.map/.freq/.dat           # Input files
│       └── Scripts/                       # Input file generation
├── Cases/                                 # Phase 3: Blind testing on real genotype data
│   ├── Input_Files/                       # PEDs for hypotheses per case
│   ├── Outputs/                           # MERLIN logs, LRs, final predictions
│   ├── Scripts/                           # Case.Rmd for summary/reporting
│   ├── ped_files_template.xlsx
│   └── White British Case Genotypes.xlsx
```

## Project Overview

The main goal is to produce a fully automated simulation workflow that:

- Scales to tens of thousands of SNPs
- Enables robust relationship testing using likelihood ratios
- Avoids the limitations of GUI-based tools (e.g., Familias, FamLink)
- Supports both synthetic and real case data

It was developed in R and Bash and validated across three phases:
1. Replicating 94-SNP benchmark data
2. Scaling to 10,000 SNPs across FS, HS, FC
3. Blind testing of real genotype profiles

---

## Libraries/Packages 

- Unix/Linux terminal or HPC
- [`MERLIN`](http://csg.sph.umich.edu/abecasis/Merlin/) (v1.1.2)
- `R` (≥ 4.4.1) with:
  - ‘dplyr’
  - ‘tidyr’
  - ‘readr’
  - ‘readxl’
  - ‘ggplot2’
  - ‘writexl’
  - ‘scales’
  - etc...

---

## Pipeline Workflow

### 1. Preprocessing
- Input `.ped`, `.map`, `.freq`, `.dat` files created in [`Original_Input_Files/`](94_SNP_Simulation/Original_Input_Files) or [`10,000_SNPs_Input_Files/`](10,000_SNP_Simulation/10,000_SNPs_Input_Files/) 
- Marker linkage models: both linked and unlinked versions prepared

### 2. Simulation
- MERLIN is executed in batch mode via Bash scripts
- Simulations run for FS, HS, FC and unrelated classes
- 50,000 iterations per scenario in genome-scale simulation

### 3. Postprocessing
- Output files parsed using RMarkdown scripts
- LR distributions analysed and visualised (density plots)
- FamLink vs MERLIN comparisons in 94-SNP validation phase
- MERLIN comparison with independent replication for ~10,000-SNP

---

## Outputs

You’ll find the following in `Outputs/` folders throughout the repo:
- Raw likelihood values and logs
- Summarised LR statistics (CSV, Excel)
- Visualisations for discriminatory power (e.g. FS vs HS vs FC) with comparisons

---

## Blind Case Testing

The [`Cases/`](Cases) folder contains a real-world proof-of-concept analysis.

### Data:
- Genotype data from White British individuals ([`White British Case Genotypes.xlsx`](Cases/White%20British%20Case%20Genotypes.xlsx))
- PEDs generated for each possible relationship class ([`ped_files_template.xlsx`](Cases/ped_files_template.xlsx))

### Script:
- `Case.Rmd`: Processes MERLIN logs, calculates LRs, and classifies most likely relationship

### Outputs:
- `.merlin.log` and `.likelihood.txt` files for each test
-  [`Case_LR_summary.csv`](Cases/Outputs/Case_LR_summary.csv) and [`Case_LR_summary_classified.csv`](Cases/Outputs/Case_LR_summary_classified.csv): Final results

---

## Citation & Contact

Please cite this work if used in academic contexts:

> Hamza, M. (2025). *Framework Development for Assessment of Forensic Victim Identification Workflows*. King’s College London, MSc in Applied Bioinformatics.

**Author**: Maahi Hamza  
**Supervisor**: Dr. Lucinda Davenport and Dr David Ballard  
**Department**: Analytical, Environmental and Forensic Sciences (FoLSM)  
**Email**: m.maahihamza1@gmail.com

---

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---
 
