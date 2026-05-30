# Oosawa Model — Stochastic Simulation of Protein Aggregation

**Topic:** Protein Aggregation & Protein Misfolding Disorders  
**Question:** When and what can physics/models tell you from data on protein aggregates?
 
---
 
## Overview
 
This project implements the **Oosawa model** for protein aggregation using the **Gillespie stochastic algorithm**, and compares simulation results against the analytical/ODE solution. It addresses the two-step kinetics observed across protein misfolding diseases (Alzheimer's, Parkinson's, Type 2 Diabetes): a slow nucleation phase followed by fast growth.
 
---
 
## The Model
 
### Oosawa model reactions
 
| Reaction | Description | Rate |
|----------|-------------|------|
| Nucleation | $n_c$ monomers → polymer of size $n_c$ | $k_n \cdot m(t)^{n_c}$ |
| Association | polymer$(j)$ + monomer → polymer$(j+1)$ | $k_a \cdot m(t)$ per polymer |
 
### State variables
 
- $m(t) = m_0 - M(t)$ — free monomers  
- $P(t)$ — number of polymers (changes only via nucleation)  
- $M(t)$ — total polymer mass (changes via nucleation and association)  
- $f(j, t)$ — number of polymers of length $j$ at time $t$
### Moment equations (ODE theory)
 
$$\frac{dP}{dt} = k_n \cdot m(t)^{n_c}$$
 
$$\frac{dM}{dt} = n_c k_n m(t)^{n_c} + k_a m(t) P(t)$$
 
---
 
## The Gillespie Algorithm
 
The Gillespie algorithm simulates exact stochastic dynamics — essential when molecule numbers are small (P ~ 10–100), where ODE approaches break down.
 
**At each step:**
 
1. Calculate reaction rates: `r_nucl = kn * m^nc`, `r_assoc = ka * m * P`
2. Sample time to next event: $\tau = -\frac{1}{r_{total}} \ln(\text{rand})$
3. Choose which reaction fires (proportional to rates)
4. Update state: $m$, $M$, $P$, polymer list
5. Repeat until $m = 0$ or `max_events` reached
---
 
## Results Summary
 
### Simulation vs Theory (Figure 1)
 
The Gillespie simulation agrees well with the ODE solution for $M(t)$ and $P(t)$. Small deviations are expected — stochasticity matters most early in the simulation when $P$ is small, which is precisely the biologically relevant nucleation regime.
 
### Effect of parameters (Figure 2)
 
| Parameter change | $M(t)$ | $P(t)$ | $f(j, t)$ |
|-----------------|--------|--------|-----------|
| ↑ $k_n$ | Shorter lag phase | More polymers | Many small polymers |
| ↑ $k_a$ | Faster growth | $P(\infty)$ unchanged | Fewer, larger polymers |
| ↑ $n_c$ | Much longer lag (exponential dependence on $n_c$) | Far fewer polymers | Fewer, larger polymers |
 
The exponential dependence on $n_c$ in the nucleation rate ($k_n \cdot m^{n_c}$) explains why nucleation is so sensitive to concentration — and why the lag phase is a hallmark of PMDs.
 
### Size distribution f(j,t) (Figure 3)
 
With Nucleation + Association only (no fragmentation), $f(j, t)$ is always monotonically decreasing — a sin-like distribution dominated by the smallest polymers. This matches the theoretical prediction. A bell-shaped (peaked) distribution requires fragmentation, as shown in the lecture notes.
 
---
 
## Background
 
Protein misfolding diseases (PMDs) involve proteins that misfold, aggregate, and accumulate in tissues. Around 30 different PMDs are known, including Alzheimer's (Aβ, tau), Parkinson's (α-synuclein), Huntington's, and Type 2 Diabetes (IAPP). Despite different proteins and tissues, they share a universal two-step aggregation kinetics: slow nucleation followed by fast growth — captured naturally by the Oosawa model.
 
**Key references:**  
- Prof. Ala Trusina, Lecture notes from the course "Physics of Molecular Diseases", Niels Bohr Institute, 2020
- Oosawa & Asakura (1975) — original polymer model  
- Knowles et al., *Science* (2009) — nucleated polymerisation framework  
- Buell et al., *Essays in Biochemistry* (2014) — experimental techniques  
 
