# In Silico PCR Primer Design and Validation Workflow

## Project Overview
This project demonstrates a complete dry-lab workflow for designing and validating PCR primers using bioinformatics tools.

## Step 1 – Primer Design (Primer3)

### Objective
Design PCR primers targeting the human GAPDH transcript variant 1 (NM_002046.7) using Primer3.

### Target Region
Specified target positions: 340, 500  
Product size range allowed: 100–1000 bp  

### Primer3 Settings

- Primer Length: Min 18 | Opt 20 | Max 24
- Primer Tm: Min 58°C | Opt 60°C | Max 62°C
- Max Tm difference between primer pairs: 5°C
- GC Content: Min 40% | Opt 50% | Max 60%
- Thermodynamic model: SantaLucia 1998
- Max 3’ stability: 9.0
- Max library mispriming: 12.00
- Pair max library mispriming: 20.00
- Number of primer pairs returned: 5

### Selected Primer Pair

Forward Primer  
Sequence: GATTTGGTCGTATTGGGCGC  
Length: 20 bp  
GC%: 55%  
Tm (Primer3): 59.97°C  
Start position: 105  

Reverse Primer  
Sequence: GTCAAAGGTGGAGGAGTGGG  
Length: 20 bp  
GC%: 60%  
Tm (Primer3): 59.96°C  
Start position: 964  

Expected Product Size: 860 bp  

### Pair Quality Metrics

- Pair Any_TH complementarity: 0.00  
- Pair 3’_TH complementarity: 0.00  
- No significant hairpin structures detected  
- No problematic self- or cross-dimer formation  

### Rationale for Selection

The selected primer pair was chosen based on:
- Nearly identical melting temperatures (~60°C)
- Acceptable GC content within defined constraints
- Absence of significant secondary structure
- Zero 3’ complementarity risk
- Acceptable mispriming scores

Additional primer pairs were generated; however, the selected pair showed optimal thermodynamic balance and clean complementarity metrics.

---

## Step 2 – Thermodynamic Validation (NEB Tm Calculator)

### Objective
Validate primer melting temperatures under realistic PCR buffer conditions using NEB Tm Calculator.

### Tool Used
NEB Tm Calculator (Q5 High-Fidelity DNA Polymerase)

### Reaction Conditions
- Polymerase: Q5 High-Fidelity DNA Polymerase
- Primer concentration: 500 nM
- Default NEB salt conditions (Q5 buffer system)

### Results

| Primer | Length | GC% | Tm (NEB) |
|--------|--------|------|----------|
| Forward | 20 nt | 55% | 67°C |
| Reverse | 20 nt | 60% | 68°C |

Recommended Annealing Temperature: **68°C**

### Interpretation

Compared to Primer3 (~60°C), NEB-calculated Tm values are higher because:

- Primer3 uses generalized thermodynamic assumptions
- NEB uses polymerase-specific buffer conditions
- Salt concentration and primer concentration significantly influence Tm

The 1°C difference between primers indicates excellent thermodynamic balance, ensuring synchronized annealing during PCR.

![NEB Tm Result](results/step2_tm_validation/neb_tm_q5_result.png.png)

## Step 3A – Specificity Assessment (Primer-BLAST)

The primer pair designed using Primer3 was evaluated using NCBI Primer-BLAST 
against the human reference genome (GRCh38.p14).

### On-target amplification

- Chromosome: 12
- Gene: GAPDH (glyceraldehyde-3-phosphate dehydrogenase)
- Expected product size: 1454 bp

### Off-target amplification

Multiple additional amplification products were predicted across several chromosomes, including:

- Chromosome 5 (alpha-1b adrenergic receptor)
- Chromosome 6 (uncharacterized region)
- Chromosome X (multiple loci)
- Chromosome 20 (protein phosphatase EYA2)
- Chromosome 11 (olfactory receptors)
- Chromosome 15 (zinc finger protein 609)
- Chromosome 7
- Chromosome 1
- Chromosome 18

Predicted off-target product sizes ranged from 292 bp to 1837 bp.

### Conclusion

Although the primer pair showed balanced Tm values and acceptable GC content, the presence of extensive off-target amplification indicates poor genome-wide specificity.

Therefore, primer redesign was required.

➡️ See redesigned primers in [Step 3B](step3b_primer_redesign.md)

