**Computational Pipeline for B-Cell–Targeted Drug Repurposing in Multiple Sclerosi**

**Overview**
_This repository presents a comprehensive computational pipeline for B-cell–targeted drug repurposing in Multiple Sclerosis (MS), integrating transcriptomic analysis, network pharmacology, molecular docking, molecular dynamics (MD), virtual screening, and ADME/Tox profiling. The workflow begins with GEO-based data acquisition and preprocessing using R (v4.3.0) and Bioconductor (v3.18), followed by differential expression analysis (limma/GEO2R) to identify significant DEGs. High-confidence hub genes are then mapped via STRING and visualized with Cytoscape, with modules detected using MCODE. Potential therapeutic compounds are screened and docked using AutoDock Vina and Glide, and the top hits are further validated through 100 ns MD simulations in Desmond with OPLS_2005 force field. Finally, ADME/Tox profiling (SwissADME, pkCSM) evaluates pharmacokinetic and toxicity properties. All scripts, software versions, parameters, and processing steps are fully documented to ensure reproducibility and transparency, making this repository a robust resource for researchers exploring B-cell–centric therapeutics in MS._
_
**Repository Contents**

****Data_Preprocessing/** **– R scripts for GEO data preprocessing and differential expression analysis.

**PPI_Network/** – Cytoscape session files, STRING network data, and module detection results.

**Docking/** – AutoDock Vina and Glide docking input/output files.

**MD_Simulation/** – Desmond MD input files and trajectory outputs.

**Virtual_Screening**/ – LigPrep-prepared ligands, Glide docking results, and top compound lists.

**ADMET_Analysis/** – SwissADME and pkCSM results with drug-likeness and toxicity predictions.

**README.md** – This file, describing the project, workflow, and methodology.

**Computational Workflow**
**1. Data Acquisition & Preprocessing**

Source: GEO (NCBI), Accession GSE21942, Platform GPL570 (Affymetrix Human Genome U133 Plus 2.0 Array)

Software: R v4.3.0, Bioconductor v3.18 (affy, limma)

_Steps:_

RMA normalization to correct background noise

Log₂ transformation of expression values

Probe filtering to remove low-intensity/non-informative probes

Scripts fully documented for reproducibility

**2. Differential Expression Analysis**

Tool: limma / GEO2R

Parameters: Adjusted p-value < 0.05 (Benjamini-Hochberg), |log₂FC| ≥ 1.5

Outputs: Volcano plots, heatmaps, and DEG tables

Notes: All steps scripted in R for reproducibility

**3. PPI Network Construction**

Tools: STRING v12.0, Cytoscape v3.10.1 with NetworkAnalyzer & CytoHubba (MNC algorithm)

Parameters: STRING combined score ≥ 0.4 (medium-confidence), ≥0.7 recommended for hub gene prioritization

Outputs: PPI network diagrams, hub genes, topological metrics

Reproducibility: OS, Java version, and plugin details specified

**4. Module Detection**

Tool: MCODE

Parameters: Degree cutoff = 2; Node score cutoff = 0.2; K-core = 2; Max depth = 100

Outputs: Identified modules functionally annotated for B-cell activation, erythrocyte differentiation, etc.

**5. Molecular Docking**

Tools: AutoDock Vina v1.2.3, Glide (Schrödinger)

_Docking Parameters:_

Vina: Exhaustiveness = 32, top 100 compounds selected, grid 20×20×20 Å with target-specific center coordinates

Glide: SP/XP modes, RMSD ≤ 2.0 Å, protein force field OPLS4

Outputs: Docked poses, binding affinities, interaction diagrams

Best Practices: Protein/ligand preparation, grid definitions, and docking scripts documented

**6. Molecular Dynamics (MD) Simulation**

Tool: Desmond (Schrödinger)

_Parameters:_

Force field: OPLS_2005

Solvent: TIP3P water, 10 Å buffer, 0.15 M NaCl

Production run: 100 ns, NPT ensemble, Berendsen thermostat, Parrinello-Rahman barostat

_Time step:_ 2 fs, snapshot interval: 10 ps

Outputs: RMSD, RMSF, hydrogen bond analysis, radius of gyration

Notes: Equilibration and production steps documented for reproducibility

**7. Virtual Screening**

Tools: LigPrep (Schrödinger), Glide SP/XP

_Database:_ ~2,500 FDA-approved compounds from ZINC15 and PubChem

_Workflow:_ HTVS → SP → XP docking

Selection Criteria: Binding energy, interaction profiles, drug-likeness

Outputs: Ranked top compounds exported for MD simulations

**8. ADME/Tox Profiling**

Tools: SwissADME, pkCSM

_Parameters:_ Drug-likeness, BBB permeability, solubility, CYP interactions, toxicity

Notes: Input formats (SMILES/Mol2) documented; cross-validation with multiple tools recommended
