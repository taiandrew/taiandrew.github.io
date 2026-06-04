# Continuity of Stable Matching Correspondences

**Working Draft**

---

## 1. Model

- $M$: finite set of man types. Each type $m \in M$ has a strict preference $R_m$ over $W \cup \{\emptyset\}$.
- $W$: finite set of woman types. Each type $w \in W$ has a strict preference $R_w$ over $M \cup \{\emptyset\}$.
- ($\emptyset$ denotes the outside option; we drop set brackets and write $\emptyset$ instead of $\{\emptyset\}$.)
- **Population vector**: $q \in \mathcal{P} := \mathbb{R}_{++}^{M \cup W}$, where $q_i$ is the mass of type $i$.

### 1.1 Aggregate Matchings

An **aggregate matching** is a matrix $Q = [Q_{m,w}] \in \mathbb{R}_+^{(M \cup \emptyset)\times(W \cup \emptyset)}$, where $Q_{m,w}$ is the mass of type-$m$ men matched to type-$w$ women.

**Feasibility** at population $q$:
$$\sum_{w \in W \cup \emptyset} Q_{m,w} = q_m \quad \forall m \in M, \qquad \sum_{m \in M \cup \emptyset} Q_{m,w} = q_w \quad \forall w \in W.$$

Denote by $\mathcal{Q}(q)$ the set of all feasible aggregate matchings at $q$.

### 1.2 Stability

**Individual rationality (IR).** $Q$ is *individually rational* if $Q_{m,w} > 0 \Rightarrow wP_m\emptyset$ and $mP_w\emptyset$.

**Blocking pair.** A pair $(m,w)$ *blocks* $Q$ if there exist $(m', w')$ such that
$$Q_{m,w'} > 0, \quad Q_{m',w} > 0, \quad wP_m w', \quad mP_w m'.$$
That is, $m$ is currently matched to some $w'$ he ranks below $w$, and $w$ is currently matched to some $m'$ she ranks below $m$.

**Pairwise stability.** $Q$ is *pairwise stable* if no blocking pair exists.

**Stability.** $Q$ is *stable* if it is pairwise stable and individually rational.

### 1.3 The Stable Matching Correspondence

$$f(q) := \{Q \in \mathcal{Q}(q) : Q \text{ is stable}\}.$$

**Main Theorem.** $f(q)$ is continuous (lower hemicontinuous and upper hemicontinuous) if and only if it is single-valued.

---

## 2. Cutoff Profiles

### 2.1 Definitions

A **cutoff profile** is $c = (c_m, c_w)_{m \in M,\, w \in W}$ where $c_m \in W \cup \emptyset$ and $c_w \in M \cup \emptyset$.

**Allowed cells.** Given cutoff profile $c$, define
$$E(c) := \{(m,w) : wR_m c_m \text{ and } mR_w c_w\},$$
including the cell $(m,\emptyset)$ when $c_m = \emptyset$, and $(\emptyset,w)$ when $c_w = \emptyset$.

**Support polytope.** Given cutoff profile $c$ and population $q$, define
$$P_c(q) := \left\{ Q \geq 0 \;:\; \sum_w Q_{m,w} = q_m,\; \sum_m Q_{m,w} = q_w,\; Q_{m,w} = 0 \text{ if } (m,w) \notin E(c) \right\}.$$
This is a closed polyhedron (possibly empty).

**Admissibility.** A cutoff profile $c$ is *admissible* if
$$\forall (m,w) \in M \times W:\quad c_m R_m w \text{ or } c_w R_w m,$$
and additionally $c_m R_m \emptyset$ and $c_w R_w \emptyset$ for all $m,w$ (the cutoffs are at least as good as being unmatched).

Denote by $\mathcal{C}$ the (finite) set of all admissible cutoff profiles.

### 2.2 Key Results

**Proposition.** *If $c$ is admissible, then every $Q \in P_c(q)$ is stable.*

*Proof.* Let $c$ be admissible and $Q \in P_c(q)$. Suppose $(m,w)$ is a blocking pair; then there exist $(m',w')$ with
$$Q_{m,w'} > 0, \quad Q_{m',w} > 0, \quad wP_m w', \quad mP_w m'.$$
Since $Q \in P_c(q)$ and $Q_{m,w'} > 0$, we have $(m,w') \in E(c)$, so $w'R_m c_m$. Combined with $wP_m w'$, we get $wP_m c_m$. Likewise $Q_{m',w} > 0$ gives $(m',w) \in E(c)$, so $m'R_w c_w$, and combined with $mP_w m'$ we get $mP_w c_w$. But then $c$ violates admissibility at the pair $(m,w)$. $\square$

**Corollary.**
$$f(q) = \bigcup_{c \in \mathcal{C}} P_c(q).$$
Hence, at each $q$, the set of stable matchings is a **finite union of closed polyhedra**, which is compact and nonempty.

*Proof.* By the Proposition, $P_c(q) \subseteq f(q)$ for every admissible $c$. Conversely, let $Q$ be any stable matching. Define $c$ by setting $c_i = \lambda_i(Q)$ (the worst partner of $i$ with positive mass in $Q$, defined below). One checks that this $c$ is admissible and $Q \in P_c(q)$. $\square$

---

## 3. Graph Construction

### 3.1 Worst Partner and Next Admissible Partner

Fix a stable matching $Q$. For each $i \in M \cup W$, define the **realized worst partner**
$$\lambda_i(Q) := \text{worst partner of type } i \text{ with positive mass in } Q$$
(with $\lambda_m(Q) \in W \cup \emptyset$ and $\lambda_w(Q) \in M \cup \emptyset$).

For each man $m$, define the **next admissible woman**
$$\eta_m(Q) := \max_{R_m}\bigl\{ w \in W : wR_m\emptyset \text{ and } mP_w\lambda_w(Q) \bigr\},$$
and set $\eta_m(Q) = \emptyset$ if this set is empty. Thus $\eta_m(Q)$ is the best woman that $m$ finds acceptable and whom $m$ strictly beats the woman's current worst partner.

*Remark.* If $w = \eta_m(Q)$, then $\lambda_m(Q)R_m w$; otherwise $(m,w)$ would be a blocking pair for $Q$.

### 3.2 The Directed Graph $G(Q)$

Define the directed graph $G(Q)$ on vertex set $M$ by
$$m \to m' \iff \eta_m(Q) \neq \emptyset \text{ and } m' = \lambda_{\eta_m(Q)}(Q).$$
That is, $m$ points to the man who is currently $m$'s next-admissible woman's worst partner. Moving along an edge in $G(Q)$ represents a downward move for men.

### 3.3 Moving Along a Cycle

Suppose there is a cycle $m_1 \to m_2 \to \cdots \to m_K \to m_1$ in $G(Q)$. Write $w_k := \eta_{m_k}(Q)$, so $m_{k+1} = \lambda_{w_k}(Q)$ (indices mod $K$).

Define the perturbed matching $Q^\alpha$ (for $0 < \alpha < \min_k Q_{m_{k+1}, w_k}$) by
$$Q^\alpha_{m_k, w_k} = Q_{m_k, w_k} + \alpha, \qquad Q^\alpha_{m_{k+1}, w_k} = Q_{m_{k+1}, w_k} - \alpha,$$
with all other entries unchanged. Each $m_k$ gains $\alpha$ mass of $w_k$ while losing $\alpha$ mass of $w_{k-1}$.

**Feasibility of $Q^\alpha$.** Each row sum is preserved: $m_k$ gains $\alpha$ in column $w_k$ and loses $\alpha$ in column $w_{k-1}$. Each column sum is preserved: $w_k$ gains $\alpha$ from $m_k$ and loses $\alpha$ from $m_{k+1}$.

### 3.4 Cycle Properties

By construction, the cycle satisfies the following properties that will be needed in the proof.

**P1. Cycle cutoffs.** In any stable matching $Q$ realizing this cycle, $c_{m_k} = w_k$ for all $m_k$ in the cycle (where $c$ is the cutoff profile induced by $Q$). 

*Argument.* $Q^\alpha$ has positive mass on both $(m_k, w_k)$ and $(m_{k+1}, w_k)$, so the support cutoff must allow both cells:
$$w_k R_{m_k} c_{m_k} \quad \text{and} \quad m_k R_{w_k} c_{w_k}.$$
By construction, $m_k P_{w_k} m_{k+1}$ (since $m_k$ is better than $w_k$'s worst match $m_{k+1}$), giving $m_{k+1} P_{w_k} c_{w_k}$. To avoid $(m_k, w_k)$ blocking, we cannot have $w_k P_{m_k} c_{m_k}$. Combined with $w_k R_{m_k} c_{m_k}$, we get $w_k = c_{m_k}$.

**P2. Cycle women's cutoffs.** $c_{w_k} P_{w_k} \emptyset$ for all $w_k$ in the cycle (the cutoff is not the outside option).

**P3. Cycle men are fully matched.** Since $w_k P_{m_k} \emptyset$ (the woman $w_k$ is acceptable to $m_k$, and $c_{m_k} = w_k$), the outside option $\emptyset$ does not satisfy $\emptyset R_{m_k} c_{m_k} = w_k$. Hence $(m_k, \emptyset) \notin E(c)$ and $Q_{m_k, \emptyset} = 0$.

---

## 4. Proof of the Main Theorem

### 4.1 Single-Valued Implies Continuous

**Step 1: Upper hemicontinuity (UHC) holds everywhere.**

Let $q^n \to q$ and let $Q^n \in f(q^n)$ with $Q^n \to Q$. We show $Q \in f(q)$.

- **Feasibility.** Row and column sums are continuous in their arguments, so $Q$ satisfies the feasibility constraints for $q$.

- **Individual rationality.** Suppose $Q_{m,w} > 0$ but $\emptyset P_m w$. Then eventually $Q^n_{m,w} > 0$ (else $Q^n \not\to Q$), contradicting IR of $Q^n$. The $w$-side argument is symmetric.

- **Pairwise stability.** Suppose $(m,w)$ blocks $Q$: there exist $(m',w')$ with $Q_{m,w'} > 0$, $Q_{m',w} > 0$, $wP_m w'$, $mP_w m'$. Then eventually $Q^n_{m,w'} > 0$ and $Q^n_{m',w} > 0$, contradicting pairwise stability of $Q^n$.

**Step 2: Single-valued plus UHC implies continuous.**

If $f(q) = \{Q(q)\}$ is single-valued and UHC, then for any $q^n \to q$ and any $Q^n \in f(q^n)$ with $Q^n \to Q$, UHC forces $Q = Q(q)$. Since the unique limit of every convergent subsequence is $Q(q)$, the function $q \mapsto Q(q)$ is continuous (every sequence $Q^n \in f(q^n)$ converges to $Q(q)$), which is equivalent to both LHC and UHC.

### 4.2 Continuous Implies Single-Valued

We prove the contrapositive: if $f$ is multivalued at some $q$, then $f$ is not lower hemicontinuous (LHC) at $q$. Recall LHC requires:
$$q^n \to q,\; Q \in f(q) \implies \exists\, Q^n \in f(q^n) \text{ s.t. } Q^n \to Q.$$

**Step 1: Find a cycle.**

Assume $f(q)$ is multivalued; let $Q^+, Q^- \in f(q)$ with $Q^+ \neq Q^-$ and $Q^+ \geq_M Q^-$ (men weakly prefer $Q^+$; such a pair exists by the lattice structure of stable matchings).

**Conjecture 1.** *The graph $G(Q^+)$ contains a cycle.*

(This is the key structural claim, argued by the fact that since $Q^+ \geq_M Q^-$ with strict inequality somewhere, there must be men who would benefit from moving, creating cycles in the improvement graph.)

Let $m_1 \to m_2 \to \cdots \to m_K \to m_1$ be a cycle in $G(Q^+)$, with $w_k = \eta_{m_k}(Q^+)$ and $m_{k+1} = \lambda_{w_k}(Q^+)$.

**Step 2: Construct the target matching.**

Apply the cycle construction from Section 3.3 to $Q^+$ with parameter $0 < \alpha < \min_k Q^+_{m_{k+1},w_k}$:
$$Q^\alpha_{m_k, w_k} = Q^+_{m_k, w_k} + \alpha, \quad Q^\alpha_{m_{k+1}, w_k} = Q^+_{m_{k+1}, w_k} - \alpha.$$
By the cycle properties P1–P3, $Q^\alpha \in f(q)$, $Q^\alpha_{m_k,\emptyset} = 0$, and the induced cutoff profile satisfies $c_{m_k} = w_k$.

**Step 3: Construct a perturbed population.**

Define
$$q^n_{m_k} = q_{m_k} + \varepsilon^n \quad \forall m_k \text{ in the cycle}, \qquad q^n_i = q_i \quad \text{otherwise},$$
where $\varepsilon^n \searrow 0$. Then $q^n \to q$.

**Step 4: Derive a contradiction from LHC.**

Suppose LHC holds. Then there exists a sequence $Q^n \in f(q^n)$ with $Q^n \to Q^\alpha$.

Since $\mathcal{C}$ is finite, pass to a subsequence on which $Q^n \in P_c(q^n)$ for a single fixed admissible cutoff $c$. The allowed cells $E(c)$ are the same for all $n$.

From Property P3, $(m_k,\emptyset) \notin E(c)$ for each cycle man $m_k$, so
$$Q^n_{m_k,\emptyset} = 0 \quad \text{and} \quad Q^\alpha_{m_k,\emptyset} = 0 \quad \forall n,\, \forall m_k \text{ in cycle.}$$

**Claim A (Accounting).** Let $\Delta U_M := U_M(Q^n) - U_M(Q^\alpha)$ and $\Delta U_W := U_W(Q^n) - U_W(Q^\alpha)$, where $U_M(Q) = \sum_m Q_{m,\emptyset}$ and $U_W(Q) = \sum_w Q_{\emptyset,w}$. Then
$$\Delta U_M - \Delta U_W = K\varepsilon^n > 0.$$

*Proof.* Let $T(Q) = \sum_{m \in M, w \in W} Q_{m,w}$ denote total cross-gender matched mass. Then
$$T(Q^n) = \sum_m q^n_m - U_M(Q^n) = \sum_m q_m + K\varepsilon^n - U_M(Q^n),$$
$$T(Q^\alpha) = \sum_m q_m - U_M(Q^\alpha),$$
so $T(Q^n) - T(Q^\alpha) = K\varepsilon^n - \Delta U_M$.

Since women's masses are unchanged ($q^n_w = q_w$),
$$T(Q^n) = \sum_w q_w - U_W(Q^n), \quad T(Q^\alpha) = \sum_w q_w - U_W(Q^\alpha),$$
so $T(Q^n) - T(Q^\alpha) = -\Delta U_W$.

Equating: $K\varepsilon^n - \Delta U_M = -\Delta U_W$, i.e., $\Delta U_M - \Delta U_W = K\varepsilon^n$. $\square$

Since $(m_k,\emptyset) \notin E(c)$, cycle men contribute $0$ to $U_M$ in both $Q^n$ and $Q^\alpha$, so $\Delta U_M$ comes entirely from outside men $M_{\mathrm{out}} := M \setminus \{m_1,\ldots,m_K\}$.

Meanwhile, all $K\varepsilon^n$ extra mass of cycle men must be absorbed into cross-gender matches (since they cannot be unmatched). Women's column sums are fixed at $q_w$, so cycle men's extra matches displace outside men's matches, forcing outside men to take on more unmatched mass:
$$\Delta U_M = K\varepsilon^n + \Delta U_W > 0.$$

**Claim B (Chain argument).** The mass absorbed from outside men travels through a stability-preserving chain $m_{k} \to w_{k} \to \cdots \to m_{\mathrm{out}}$ for each cycle man $m_k$. Moving $\varepsilon^n$ along this chain starting from $Q^\alpha$ yields a stable matching at $q^n$.

*The chain.* Since $Q^n$ is stable and $Q^n \in P_c(q^n)$, the extra $\varepsilon^n$ of cycle man $m_k$ is matched to some woman $w$ (at least as good as $w_k$ for $m_k$, since only those cells are in $E(c)$). That woman $w$ must shed $\varepsilon^n$ mass from her worst current partner $m' = \lambda_w(Q^n)$, who in turn increases his unmatched mass or sheds from another woman, and so on until the chain terminates at an outside man $m_{\mathrm{out}}$ who absorbs the extra unmatched mass.

This chain preserves feasibility (each row/column sum shifts by $\pm\varepsilon^n$ in a balanced way) and preserves stability: each transfer is from a worse partner to a better one, so no new blocking pairs are introduced. Hence the resulting matching lies in $f(q^n)$ and converges to $Q^\alpha$ as $\varepsilon^n \to 0$.

**Reaching the contradiction.** Claim B shows that any sequence $Q^n \in f(q^n)$ with $Q^n \to Q^\alpha$ must route the extra $\varepsilon^n$ mass along a chain through $E(c)$. However, the cutoff structure forces $c_{m_k} = w_k$, meaning $m_k$ can only gain mass from women weakly preferred to $w_k$. When all such women are already at capacity in $Q^\alpha$ (since $Q^\alpha$ is an interior point of the support polytope, chosen so that $Q^\alpha_{m_{k+1},w_k} > 0$), there is no room to route the extra mass while remaining in $E(c)$. This contradicts $Q^n \in P_c(q^n)$ converging to $Q^\alpha$, showing LHC fails at $Q^\alpha$ for the perturbation $q^n$.

Therefore, $f$ is not LHC, hence not continuous.

---

## 5. Summary

| Direction | Argument |
|---|---|
| Single-valued $\Rightarrow$ continuous | UHC holds everywhere (stability passes to limits); UHC + single-valued $\Leftrightarrow$ continuous. |
| Continuous $\Rightarrow$ single-valued | If multivalued, find a cycle in $G(Q^+)$, construct interior point $Q^\alpha \in f(q)$, perturb $q^n$ by adding $\varepsilon^n$ mass to cycle men. Accounting shows extra mass cannot be absorbed while staying in $P_c(q^n)$, so no sequence in $f(q^n)$ converges to $Q^\alpha$: LHC fails. |

**Key ingredients:**
- Finiteness of $\mathcal{C}$ (allows WLOG fixed cutoff profile).
- Cycle properties P1–P3 (cycle men are fully matched; their cutoff equals their next admissible woman).
- Accounting identity $\Delta U_M - \Delta U_W = K\varepsilon^n$ (mass conservation).
- Chain argument (mass flow preserves stability).

---

*Notes: Claim B (chain argument) and Conjecture 1 (cycle existence) require further elaboration. The lattice structure of stable matchings used in Step 1 of §4.2 should be cited or proved separately.*
