# Finke–Watzky Model for Protein Aggregation

This repository implements and analyzes the deterministic Finke–Watzky two-step model for protein aggregation kinetics.

Developed as part of the MSc course:

**Physics of Molecular Diseases**  
Niels Bohr Institute — University of Copenhagen (Prof. Ala Trusina)


# Overview
The Finke–Watzky model describes aggregation as a two-step process:

1. **Nucleation:**
   A → B with rate constant k₁

2. **Autocatalytic growth:**
   A + B → 2B with rate constant k₂

The model captures the characteristic sigmoidal behavior observed in protein aggregation experiments.

---

## 🧪 Tasks Implemented

### 1. Implementation of the Model

The analytical solution of the Finke–Watzky model is implemented and validated against numerical expectations.

### 2. Data Extraction and Fitting

Experimental data are extracted from published figures using WebPlotDigitizer and fitted using nonlinear least squares.

### 3. Interpretation of Results

The model successfully reproduces sigmoidal aggregation kinetics. The fitted parameters provide insight into:

* **k₁:** nucleation rate (controls lag phase)
* **k₂:** autocatalytic growth rate (controls slope)
* **A₀:** total concentration (plateau level)

Deviations at early times suggest experimental offsets or pre-existing aggregates.

### 4. Comparison with Oosawa Model

| Feature            | Finke–Watzky  | Oosawa     |
| ------------------ | ------------- | ---------- |
| Type               | Deterministic | Stochastic |
| Complexity         | Low           | High       |
| Data fitting       | Easy          | Difficult  |
| Mechanistic detail | Limited       | High       |
| Size distribution  | No            | Yes        |

The two models are complementary:

* Finke–Watzky is ideal for fitting experimental data
* Oosawa provides deeper mechanistic insight

---

## 📊 Example Output

The model reproduces sigmoidal aggregation curves and provides good agreement with experimental data, especially in the growth regime.

---

## ⚠️ Limitations

* Does not account for fragmentation or heterogeneity
* Sensitive to data quality and baseline offsets
* Cannot uniquely determine mechanism from fitting alone

---

# Review
## Comparison Between the Oosawa Model and the Finke–Watzky Model

The Oosawa model and the Finke–Watzky model provide two fundamentally different approaches to describing protein aggregation kinetics.
The Oosawa model is a stochastic, mechanistic framework that explicitly tracks the formation and evolution of aggregates of different 
sizes. It allows for detailed modeling of processes such as nucleation, elongation, fragmentation, and dissociation, and provides access
to the full size distribution of aggregates. This makes it highly informative for understanding the microscopic mechanisms of aggregation.
However, the model is computationally demanding and involves many parameters, making it difficult to fit directly to experimental data.
In contrast, the Finke–Watzky model is a simplified deterministic model based on two steps: nucleation and autocatalytic growth. It 
describes the time evolution of aggregate mass using a small number of parameters and has an analytical solution. This makes it 
particularly suitable for fitting experimental data and extracting kinetic parameters. However, it lacks mechanistic detail and does 
not provide information about aggregate size distributions or more complex processes such as fragmentation.
The choice between the two models depends on the goal of the analysis. The Finke–Watzky model is preferred when analyzing experimental 
data and extracting effective kinetic parameters, while the Oosawa model is more appropriate for investigating the underlying physical
mechanisms and detailed aggregation dynamics.
Overall, the two models are complementary: the Finke–Watzky model offers simplicity and direct applicability to data, whereas the Oosawa
model provides deeper mechanistic insight at the cost of increased complexity.

---

## 📚 References

* Finke, R. G., & Watzky, M. A. (2007)
* Morris et al., Biochemistry (2008)
* Prof. Ala Trusina, MSc Course: Biophysics of Molecular Diseases, University of Copenhagen, Niels Bohr Institute

---
