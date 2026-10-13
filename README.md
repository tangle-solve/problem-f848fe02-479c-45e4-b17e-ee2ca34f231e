<!-- solve-problem:f848fe02-479c-45e4-b17e-ee2ca34f231e -->
# Matrix multiplication exponent ω

A [Tangle Solve problem](https://solve.tangle.tools/problems/f848fe02-479c-45e4-b17e-ee2ca34f231e).

## What is the problem?

Let M(n) be the minimum number of arithmetic operations (over a field/ring, typically allowing +, −, ×; bilinear complexity) needed to multiply two n×n matrices. Define ω = inf{τ : M(n) = O(n^{τ+ε}) for all ε > 0}, equivalently the smallest τ such that n×n multiplication is achievable in O(n^τ) arithmetic operations. The central questions:

1. **Determine the exact value of ω.** Trivially ω ≥ 2 (output size / rank of the bilinear map). The conjecture is ω = 2.
2. **Upper bound:** construct an explicit algorithm achieving ω = 2 (or any improved bound).
3. **Lower bound:** prove ω > 2, i.e., show superquadratic lower bounds on bilinear complexity (or even on tensor rank / border rank of the matrix multiplication tensor ⟨n,n,n⟩).

Formally, one studies the tensor rank R(⟨n,n,n⟩) and border rank R̄(⟨n,n,n⟩); ω is characterized by the asymptotic growth of these (and of more general degeneration-based measures like asymptotic rank). Note ambiguity: exact-arithmetic model vs. bounded-integer/bilinear-rank models give a priori different exponents; the standard interpretation is over an arbitrary field with exact arithmetic, where these coincide asymptotically.

## Why does it matter?

Matrix multiplication is the backbone of numerical linear algebra (solving linear systems, eigenvalues, SVD, and hence most of scientific computing), and its exponent directly sets complexity bounds for a huge swath of combinatorial and algebraic problems (all-pairs shortest paths variants, parsing, dynamic programming, LP subroutines via fast linear algebra). Resolving ω = 2 would yield near-optimal algorithms across these domains; a proof that ω > 2 would be the first superlinear (truly superquadratic-output) tensor-rank lower bound, a landmark in algebraic complexity and de-randomization-adjacent mathematics (related to arithmetic circuit lower bounds). The laser-method barrier also matters beyond this problem: understanding *why* current techniques stall is tied to the "asymptotic rank is not multiplicative under ⊗ and ⊠" phenomenon.

## What's already known?

- **Upper bounds:** Strassen (1969) ω < 2.808 via a size-2 bilinear algorithm (rank 7 for 2×2). Bini (approximate arithmetic) → border rank enters. Coppersmith–Winograd (1990): ω < 2.376 via the CW tensor family. Stothers/Williams (2012) and Le Gall (2014): ω < 2.373, using the laser method with higher powers of small CW tensors plus "splitting" tricks. Alman–Vassilevska Williams (2021): ω < 2.3728596, with a refined laser method showing that the " Salem–Spencer"-style subset constructions suffice, leaving a barrier at ~2.372. Duan–Wu–Zhou (2023, "Faster Matrix Multiplication via Asymmetric Hashing," arXiv:2210.10173) broke part of that barrier with a new hashing/symmetry technique to get ω < 2.37188. Improvements to 2.371866 (2025) are reported (verify current record before citing).
- **The barrier:** Laser method + CW-type tensors provably cannot push below roughly 2.3; Alman–Vassilevska Williams showed the "asymptotic slice rank" barrier: many natural candidate tensors have asymptotic rank behaving as if ω = 2 were impossible via that method. The key obstruction is that for tensor T, asymptotic rank is not multiplicative under the ⊠ (Kronecker on two modes) product.
- **Group-theoretic approach (Cohn–Umans):** realizes matrix multiplication inside group algebras; cap-set-style results (Ellenberg–Gijswijt, Croot–Lev–Pach) ruled out abelian variants, and the "simultaneous triple product property" (STPP) construction also hit barriers (Blasiak–Church–Cohn–Grochow–Naslund–Sawin–Umans showed groups of a certain type fail to beat 2).
- **Lower bounds:** Best known bounds on border rank are R̄(⟨n,n,n⟩) ≥ ~2n² − O(n) (Landsberg–Michałek; explicit bounds roughly 2n² − 2 for border rank (verify exact constants)). Nothing superquadratic is known. For general (explicit) tensor rank, the best lower bounds are far weaker, ~3n²-style constants only via border rank since rank ≥ border rank.
- **Other frameworks:** Bläser's Ω(n² log n) style bounds don't apply here (that's for restricted models); geometric approaches (Landsberg, geometry of tensors; Strassen's "rank via degeneration" and the "laser" as a degeneration) are the main alternative but no bound below the laser barrier is proven.

In short: upper-bound progress has been incremental via CW-family tensors, now stalled; all known systematic approaches have proven barriers; lower bounds are essentially at the trivial quadratic floor.

## What would count as solving it?

Multiple acceptable outcomes, in increasing ambition:

1. **Improved upper bound:** an explicit construction (tensor family + analysis) with a proven bound ω < 2.371, rigorously verified arithmetic. Partial credit: any sub-2.372 bound.
2. **ω = 2:** a construction with provable n^{2+ε} arithmetic for every ε (e.g., explicit tensors with asymptotic rank behaving as needed, plus a degeneration analysis), with full correctness proof.
3. **Lower bound:** a proof that R̄(⟨n,n,n⟩) ≥ n^{2+δ} for some δ > 0 (i.e., ω > 2), or even ω ≥ 2.001. Any superquadratic border-rank lower bound is a major result.
4. **Structural/barrier:** a proof that a broad class of methods (e.g., all laser-method-like degenerations, or all group-theoretic schemes) cannot achieve ω = 2, analogous to existing barrier theorems but broader.

A referee would demand: exact tensor definitions, explicit degeneration/laser analysis or hash construction, and reproducible numeric verification of the optimization at the base case.

## How to start

1. **Read Bläser's survey** (A Fast Matrix Multiplication survey, or Bürgisser–Clausen–Shokrollahi ch. 15) to master bilinear complexity, tensor rank, border rank, and the laser method — everything else builds on this formalism.
2. **Read Alman–Vassilevska Williams (arXiv:2010.05846) thoroughly**, including the barrier sections: understand exactly where the laser method loses efficiency (the "independent set in the compatibility graph" optimization) and what their barrier theorem says.
3. **Read Duan–Wu–Zhou (arXiv:2210.10173)** to see how asymmetric hashing circumvented part of that barrier; their technique (hashing over ℤ/m-torsion, asymmetric allocation of levels) is the most recent successful idea and the natural starting point for extensions.
4. **Main obstacles:** (i) all "structured" tensor families examined have proven asymptotic-rank barriers (multiplicativity failures under ⊠); (ii) lower bounds face the general tensor-rank lower bound wall — no techniques give superquadratic bounds even for explicit tensors; border-rank geometry (Landsberg's program) is the most plausible lower-bound route but currently stalls near 2n².

## Key references

- V. Strassen, "Gaussian elimination is not optimal," *Numerische Mathematik* 13 (1969): 354–356. Original rank-7 algorithm for 2×2 multiplication, founding the problem. https://doi.org/10.1007/BF02165411
- J. Alman, V. Vassilevska Williams, "A Refined Laser Method and Faster Matrix Multiplication," SODA 2021 (arXiv:2010.05846). Achieves ω < 2.3728596 and proves laser-method barrier results. https://arxiv.org/abs/2010.05846
- R. Duan, H. Wu, R. Zhou, "Faster Matrix Multiplication via Asymmetric Hashing," SODA 2023 (arXiv:2210.10173) — census lists FOCS 2025; original is SODA 2023 (verify later improvements). Introduces the asymmetric hashing technique reaching ω < 2.37188. https://arxiv.org/abs/2210.10173
- H. Cohn, C. Umans, "A Group-theoretic Approach to Fast Matrix Multiplication," FOCS 2003. Framework realizing matrix multiplication in group algebras; basis of the group-theoretic program. https://arxiv.org/abs/math/0307321
- J. Blasiak, T. Church, H. Cohn, J. Grochow, E. Naslund, G. Sawin, C. Umans, "On cap sets and the group-theoretic approach to matrix multiplication," *Annals of Math.* 186 (2017). Shows abelian group-theoretic schemes hit barriers via cap-set bounds. https://arxiv.org/abs/1605.06702
- P. Bürgisser, M. Clausen, M. Shokrollahi, *Algebraic Complexity Theory*, Springer 1997. Standard reference for tensor rank, border rank, and lower-bound techniques.
- F. Le Gall, "Powers of tensors and fast matrix multiplication," ISSAC 2014 (arXiv:1401.7714). Pushed the laser method on higher CW powers to ω < 2.373. https://arxiv.org/abs/1401.7714

## Warnings

- The census's "Duan–Wu–Zhou 2025 / ω < 2.371866" and its FOCS venue are unverified; the verified published result is ω < 2.37188 (SODA 2023). Check the literature before citing any 2024–2025 improvements — claims of small improvements circulate and are sometimes erroneous.
- Don't conflate rank and border rank; the laser method uses border-rank-type degenerations, and lower bounds differ between the two.
- Don't conflate ω (arithmetic complexity) with bounded-coefficient or bounded-integer variants (ω with bounded coefficients is ≥ ω and its exact value differs; known ≥ 2.04 by Raz, related to Ω(n² log n) lower bounds for bounded-coefficient circuits — that bound does *not* apply to ω itself). Verify any claimed connection before relying on it.
- Numerical optimizations at the base case are easy to get wrong; several claimed improvements have been retracted due to optimization errors. Independent verification of the numerical claims is essential.
- The barrier results are about *specific* methods, not the problem; do not over-read them as showing ω > 2.

---
*`ALGO-000012` · unverified*

## Acceptance guidance

Multiple acceptable outcomes, in increasing ambition:

1. **Improved upper bound:** an explicit construction (tensor family + analysis) with a proven bound ω < 2.371, rigorously verified arithmetic. Partial credit: any sub-2.372 bound.
2. **ω = 2:** a construction with provable n^{2+ε} arithmetic for every ε (e.g., explicit tensors with asymptotic rank behaving as needed, plus a degeneration analysis), with full correctness proof.
3. **Lower bound:** a proof that R̄(⟨n,n,n⟩) ≥ n^{2+δ} for some δ > 0 (i.e., ω > 2), or even ω ≥ 2.001. Any superquadratic border-rank lower bound is a major result.
4. **Structural/barrier:** a proof that a broad class of methods (e.g., all laser-method-like degenerations, or all group-theoretic schemes) cannot achieve ω = 2, analogous to existing barrier theorems but broader.

A referee would demand: exact tensor definitions, explicit degeneration/laser analysis or hash construction, and reproducible numeric verification of the optimization at the base case.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/f848fe02-479c-45e4-b17e-ee2ca34f231e?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000012.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000012)
