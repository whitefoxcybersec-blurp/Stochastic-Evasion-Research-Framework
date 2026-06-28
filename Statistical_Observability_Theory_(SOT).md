# Statistical Observability Theory (SOT)

## Towards a Mathematical Foundation for Statistical Detection in Computational Systems

**Author:** Gabriel Ghostwire

---

# Abstract

Modern anomaly detection systems are fundamentally inference engines operating under incomplete information. Existing approaches largely focus on improving classification algorithms while treating observability as an implicit assumption. This work proposes the **Statistical Observability Theory (SOT)**, a mathematical framework describing the relationship between observable information, uncertainty, and the theoretical limits of statistical detection.

The central hypothesis is that the detectability of any computational system is not an intrinsic property of the detector itself, but rather a consequence of the quantity, quality, and temporal stability of the information available through observation.

---

# 1. Introduction

Every detection system solves the same mathematical problem.

Given a partially observable system, infer its hidden internal state.

Whether the detector is an EDR, IDS, antivirus, machine learning classifier or Bayesian decision model is secondary.

All are attempting to estimate an unknown state from incomplete observations.

This shifts the problem of cybersecurity from software engineering toward statistical inference.

---

# 2. State Space

Let

\[
\mathcal{S}
\]

denote the complete state space of a computational system.

Each element

\[
s \in \mathcal{S}
\]

represents the complete internal configuration of the environment, including

- memory
- process hierarchy
- execution context
- kernel state
- file system
- network activity
- temporal dependencies

The true state is never directly observable.

---

# 3. Observation Operator

Define the observation operator

\[
\mathcal{O} :
\mathcal{S}
\rightarrow
\mathcal{Y}
\]

where

\[
\mathcal{Y}
\]

is the observable telemetry space.

Examples include

- ETW events
- Syscalls
- API calls
- PE metadata
- Network flows
- File entropy
- Memory snapshots

The observation operator is generally non-invertible.

Therefore,

\[
\exists
s_i \neq s_j
\]

such that

\[
\mathcal{O}(s_i)
=
\mathcal{O}(s_j)
\]

meaning multiple internal states may generate identical observations.

---

# Definition 1 — Information Loss

The unavoidable information loss introduced by the observation process is defined as

\[
\mathcal{L}
=
H(S|Y)
\]

where

\[
H(S|Y)
\]

denotes the conditional entropy of the system state given the observed telemetry.

This quantity measures the residual uncertainty after observation.

---

# Definition 2 — Statistical Observability

We define the Statistical Observability Index

\[
\boxed{
\Omega
=
\frac{I(S;Y)}
{H(S)}
}
\]

where

- \(I(S;Y)\) is the Mutual Information;
- \(H(S)\) is the entropy of the complete system state.

Properties:

\[
0
\le
\Omega
\le
1
\]

Interpretation

- \(\Omega = 1\): Complete observability.
- \(\Omega = 0\): No useful information is available.
- \(0<\Omega<1\): Partial observability.

---

# Axiom I — Limited Observability

No real-world detection system operating through indirect telemetry can achieve

\[
\Omega = 1
\]

under non-stationary environments.

Information loss is an intrinsic consequence of partial observation.

---

# Axiom II — Residual Uncertainty

For every incomplete observation operator,

\[
H(S|Y)>0
\]

holds even after an arbitrarily large number of observations.

Additional telemetry reduces uncertainty but cannot eliminate it entirely.

---

# Axiom III — Conservation of Statistical Evidence

Observable statistical evidence cannot be destroyed.

It can only migrate across observational domains.

Formally,

\[
\sum_{k=1}^{n}
I_k
=
C-\varepsilon
\]

where

\[
I_k
\]

represents the mutual information available in observational domain

\[
k
\]

Examples include

- static analysis
- runtime behavior
- memory
- network
- distributed topology

Reducing observability in one domain necessarily increases dependence on others.

---

# Axiom IV — Non-Stationary Degradation

Let

\[
P_t
\]

denote the operational distribution at time

\[
t.
\]

Whenever

\[
P_t
\neq
P_{t+\Delta t}
\]

the observation operator becomes progressively misaligned with reality.

Consequently,

\[
\Omega(t+\Delta t)
<
\Omega(t)
\]

unless recalibration occurs.

---

# Definition 3 — Epistemic Energy

We define the Epistemic Energy of a detection system as

\[
\mathcal{E}
=
D_{KL}
+
W_1
+
ECE
\]

where

- \(D_{KL}\) measures probabilistic divergence;
- \(W_1\) measures optimal transport cost;
- \(ECE\) measures probability calibration error.

The larger

\[
\mathcal{E},
\]

the more difficult accurate inference becomes.

---

# Definition 4 — Observability Field

Statistical observability varies throughout the state space.

Define

\[
\Omega(s)
:
\mathcal{S}
\rightarrow
[0,1]
\]

as a scalar field assigning each state its degree of observability.

Its gradient

\[
\nabla\Omega
\]

represents the direction of maximal increase or decrease in inferability.

---

# Theorem 1 — Observation Saturation

Assume

\[
I(S;Y_n)
\]

converges.

Then there exists

\[
\Omega^*
<
1
\]

such that

\[
\lim_{n\rightarrow\infty}
\Omega_n
=
\Omega^*.
\]

Therefore,

perfect observability cannot be achieved solely through increasing telemetry volume.

---

# Theorem 2 — Detectability Upper Bound

For any statistical detector

\[
D,
\]

the probability of correct inference satisfies

\[
P_D
\le
\Omega.
\]

Thus,

the theoretical detection capability is bounded above by the information effectively preserved during observation.

---

# Central Hypothesis

The detectability of computational systems is fundamentally limited by statistical observability rather than algorithmic sophistication.

Consequently,

future advances in detection should prioritize increasing the information content of observations instead of exclusively improving classifiers.

---

# Research Implications

The Statistical Observability Theory suggests a shift in research focus from classifier optimization toward the mathematical characterization of observable information.

Under this perspective,

concept drift,

Bayesian inference,

information theory,

optimal transport,

and statistical calibration become different manifestations of a single underlying principle:

> **Detection is fundamentally constrained by the information preserved through observation.**
