<!-- solve-problem:6f44117d-96c4-4fb6-94d3-7ae9e5e30828 -->
# Does derandomizing PromiseZPP derandomize PromiseBPP?

A [Tangle Solve problem](https://solve.tangle.tools/problems/6f44117d-96c4-4fb6-94d3-7ae9e5e30828).

## What is the problem?

We work with **promise problems**: pairs Π = (Π_yes, Π_no) of disjoint languages. A promise problem is in PromiseBPP if a randomized poly-time machine, on inputs in Π_yes ∪ Π_no, outputs the correct answer with probability ≥ 2/3 (no constraint outside the promise). It is in PromiseZPP if the machine either outputs the correct answer or outputs a special symbol "⊥" ("don't know"), with Pr[output = correct] ≥ 1/2 (equivalently 1 − 2^{−k} by repetition) on promised inputs, and it **never outputs a wrong answer** on promised inputs.

**Open question:** Does PromiseZPP ⊆ P imply PromiseBPP ⊆ P?

Contrast with the language (non-promise) setting: for languages, ZPP = RP ∩ coRP ⊆ BPP, so ZPP = P gives no direct information about BPP — the classical route to BPP = P goes through hardness-vs-randomness (Impagliazzo–Wigderson). The promise setting is different in a crucial way: PromiseBPP has **natural complete problems**, e.g. CAPP (circuit acceptance probability estimation: given circuits C₀, C₁ with E[C₀] ≥ E[C₁] + 1/3 or E[C₀] = E[C₁], decide which), and PromiseZPP has analogous zero-error versions (e.g. "find an input where C₀ ≠ C₁, or certify none exists"). This richer structure is why the implication is plausible but unresolved. Ambiguity note: "⊆ P" should be read as "every promise problem in the class has a deterministic poly-time decider correct on the promise"; a relativized/open-question reading is also possible but the standard interpretation is the unconditional implication.

## Why does it matter?

The question probes whether eliminating *zero-error* randomness already eliminates *bounded-error* randomness — i.e., whether the randomness hierarchy is "rigid." A proof would give a new, cheaper route to full derandomization: PromiseBPP ⊆ P is equivalent to deterministic poly-time CAPP, a holy-grail target with consequences for circuit lower bounds, learning theory, and the study of randomness in algorithms generally. It also matters for hardness-vs-randomness: it would show that "ZPP-type hardness" (e.g., easy witness-lower-bound conditions, cf. 'easy witness lemma' machinery) suffices, potentially weakening the circuit-lower-bound assumptions currently needed for BPP = P.

## What's already known?

- For **languages**: ZPP ⊆ BPP trivially, and no known implication ZPP = P ⇒ BPP = P exists; the standard derandomization of BPP (Impagliazzo–Wigderson 1997) needs exponential circuit lower bounds for E, an assumption far stronger than anything ZPP = P is known to give.
- For **promise problems**: Goldreich–Wigderson studied PromiseBPP's structure; the CAPP problem is complete for it, and derandomizing CAPP is equivalent to PromiseBPP ⊆ P. Zero-error analogues (sampling/certification tasks) are complete for PromiseZPP.
- The 2024 Trevisan memorial collection (Fortnow, Goldreich, Håstad, Vadhan, Williamson) explicitly lists the implication as open, noting that standard amplification techniques do not transfer: amplifying a PromiseBPP algorithm's gap doesn't make any single random string a *certified-correct* answer, which is what a PromiseZPP machine would need.
- Related partial results exist in the "moderate" derandomization literature (e.g., reducing the number of random bits, hardness-vs-randomness for promise classes); none settle the implication in either direction. I am not aware of an oracle separation separating the two hypotheses; constructing one would itself be progress. (verify)

## What would count as solving it?

Either direction resolves it:

1. **Positive:** a proof that PromiseZPP ⊆ P ⇒ PromiseBPP ⊆ P — concretely, an argument converting a poly-time algorithm for the PromiseZPP-complete problem (e.g., zero-error disagreement-finding for circuit pairs) into a poly-time CAPP algorithm.
2. **Negative:** an oracle A relative to which PromiseZPP^A ⊆ P^A but PromiseBPP^A ⊄ P^A (or an unconditional separation of the hypotheses under some relativizable formalization).
3. **Intermediate credit:** any nontrivial class of PromiseBPP problems (e.g., CAPP for restricted circuit classes) shown to follow from PromiseZPP ⊆ P, or a proof that the implication holds under a standard hardness assumption weaker than the IW assumption.

## How to start

1. **Read the Trevisan memorial open-problems contribution first** (Fortnow–Goldreich–Håstad–Vadhan–Williamson 2024) for the authors' own intuition about where the proof breaks.
2. **Write down the complete problems explicitly.** PromiseZPP's canonical problem is roughly: given circuits C₀, C₁, either find x with C₀(x) ≠ C₁(x) or certify that E[C₀] = E[C₁]. PromiseBPP's is the CAPP gap problem. Try to reduce the latter to the former; the obstruction is that a candidate answer needs a *certificate of correctness*, and a single accepting computation of a BPP machine provides none.
3. **Try an oracle attack:** adapt classic oracle constructions separating RP/BPP/ZPP (e.g., oracle tricks from Hartmanis–Hemerling–Kurtz-style random-oracle arguments) to the promise setting. Note that promise classes have more "fragile" oracle behavior — the oracle must respect the promise.
4. **Look at hardness-vs-randomness for promise classes:** check whether IW-style reconstruction can use a PromiseZPP-complete problem as its hard language; the reconstruction procedure's tolerance to errors is where "zero-error" may help.

## Key references

- O. Goldreich, S. Goldwasser, D. Ron, "On the possibilities of honest-but-curious deterministic computation" / and Goldreich–Wigderson work on promise problems (verify exact papers) — foundational treatment of the structure of promise-problem classes BPP/promise. Actually the canonical reference here is **Goldreich, "On Promise Problems"** (in *Theoretical Computer Science*, 2006; also in Oded Goldreich's essays): surveys PromiseBPP, promise-class subtleties, and their complete problems.
- R. Impagliazzo, A. Wigderson, "P = BPP if E requires exponential circuits: derandomizing the XOR lemma" (STOC 1997), the standard hardness-vs-randomness framework any positive result must engage with or bypass.
- L. Fortnow, O. Goldreich, J. Håstad, S. Vadhan, … (2024), open-problem contributions in the Luca Trevisan memorial collection — the source listing this problem as open. (verify exact author list and title)
- R. Williams, "Nonuniform ACC circuit lower bounds" (JACM 2014) and successors, illustrating the "moderate derandomization ⇒ lower bounds" trade-offs that make derandomization of promise classes valuable.

## Warnings

- **Don't conflate language classes with promise classes.** For languages ZPP ⊆ BPP makes the question trivial-ish; the entire content is the promise setting, where PromiseBPP has complete problems like CAPP that BPP itself lacks.
- **Amplification is not enough.** A naive attack — amplify the BPP machine, then argue a random string witnesses correctness — fails because amplified correctness is probabilistic, not certified; ZPP requires per-output soundness. This is the canonical dead end.
- **Beware the "no wrong answers on the promise" clause:** PromiseZPP machines are unconstrained off the promise, which complicates composing reductions; verify compositions respect promises.
- The census record is machine-generated and somewhat vague; the exact attribution and contents of the 2024 memorial-collection entry should be verified before citing.

---
*`ALGO-000053` · unverified*

## Acceptance guidance

Either direction resolves it:

1. **Positive:** a proof that PromiseZPP ⊆ P ⇒ PromiseBPP ⊆ P — concretely, an argument converting a poly-time algorithm for the PromiseZPP-complete problem (e.g., zero-error disagreement-finding for circuit pairs) into a poly-time CAPP algorithm.
2. **Negative:** an oracle A relative to which PromiseZPP^A ⊆ P^A but PromiseBPP^A ⊄ P^A (or an unconditional separation of the hypotheses under some relativizable formalization).
3. **Intermediate credit:** any nontrivial class of PromiseBPP problems (e.g., CAPP for restricted circuit classes) shown to follow from PromiseZPP ⊆ P, or a proof that the implication holds under a standard hardness assumption weaker than the IW assumption.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/6f44117d-96c4-4fb6-94d3-7ae9e5e30828?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000053.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000053)
