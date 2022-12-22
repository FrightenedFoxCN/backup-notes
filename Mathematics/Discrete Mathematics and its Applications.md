# Discrete Mathematics and its Applications, Kenneth H. Rosen

## 1 The Foundations: Logic & Proofs

### Propositional calculus

**Def 1. Proposition** A declarative sentence that is either true or false, but not both. Letters like $p$ used to denote propositions are called **propositional variables** or **sentential variables**. The **truth value** of a proposition is denoted by $\mathbb{T}$ or $\mathbb{F}$. The area of logic that deals with propositions is called the **propositional calculus** or **propositional logic**.

**Def 2. Atomic propositions** Propositions that cannot be expressed in terms of simpler propositions.

**Def 3. Compound propositions** Propositions constructed by combining one or more propositions with **logical operators**.

> **Logical operators:**
>
> 1. the **negation** of $p$, denoted by $\neg p$ or $\bar p$, literally means "It's not the case that $p$".
>
>    *! in $\LaTeX$, typed with `\neg p` or `\bar p`*.
>
>    also denoted by $\sim p$ *! (`\sim p` in $\LaTeX$)*, $-p$, $p'$, $\mathrm{N}p$ *! (`\mathrm{N}p` in $\LaTeX$)* and $!p$.
>
>    the **truth table**:
>
>    |     $p$      |   $\neg p$   |
>    | :----------: | :----------: |
>    | $\mathbb{T}$ | $\mathbb{F}$ |
>    | $\mathbb{F}$ | $\mathbb{T}$ |
>    
> 2. the **conjunction** of $p$ and $q$, denoted by $p \wedge q$, literally means "$p$ and $q$".
>
>    *! in $\LaTeX$, typed with `p \wedge q`*.
>
>    the truth table:
>
>    |     $p$      |     $q$      | $p \wedge q$ |
>    | :----------: | :----------: | :----------: |
>    | $\mathbb{T}$ | $\mathbb{T}$ | $\mathbb{T}$ |
>    | $\mathbb{T}$ | $\mathbb{F}$ | $\mathbb{F}$ |
>    | $\mathbb{F}$ | $\mathbb{T}$ | $\mathbb{F}$ |
>    | $\mathbb{F}$ | $\mathbb{F}$ | $\mathbb{F}$ |
>
> 3. the **disjunction** of $p$ and $q$, denoted by $p \vee q$, literally means "$p$ or $q$".
>
>    *! in $\LaTeX$, typed with `p \vee q`*.
>
>    the truth table:
>
>    |     $p$      |     $q$      |  $p \vee q$  |
>    | :----------: | :----------: | :----------: |
>    | $\mathbb{T}$ | $\mathbb{T}$ | $\mathbb{T}$ |
>    | $\mathbb{T}$ | $\mathbb{F}$ | $\mathbb{T}$ |
>    | $\mathbb{F}$ | $\mathbb{T}$ | $\mathbb{T}$ |
>    | $\mathbb{F}$ | $\mathbb{F}$ | $\mathbb{F}$ |
>
>    *! **Remarks:** Etymologically, disjunction can date back to Lat. disjunctĭo, fr. disjungo, which literally means 'separate'. And the Lat. word for conjunction is fr. conjungo, under the meaning of 'unite'. the $\LaTeX$ notations relate much more to its shape than to its meaning.*
>
> 4. the **exclusive or** of $p$ and $q$, denoted by $p \oplus q$ or $p\ \mathrm{XOR}\ q$, *! literally means "there is only one of p and q being true"*.
>
>    *! in $\LaTeX$, typed with `p \oplus q` or `p\ \mathrm{XOR}\ q`*.
>
>    the truth table:
>
>    |     $p$      |     $q$      | $p \oplus q$ |
>    | :----------: | :----------: | :----------: |
>    | $\mathbb{T}$ | $\mathbb{T}$ | $\mathbb{F}$ |
>    | $\mathbb{T}$ | $\mathbb{F}$ | $\mathbb{F}$ |
>    | $\mathbb{F}$ | $\mathbb{T}$ | $\mathbb{F}$ |
>    | $\mathbb{F}$ | $\mathbb{F}$ | $\mathbb{F}$ |
>
> 5. the **conditional statements** such as "if $p$, then $q$" is denoted by $p \rightarrow q$.
>
>    *! in $\LaTeX$, typed with `p \rightarrow q`*.
>
>    the truth table:
>
>    |     $p$      |     $q$      | $p \wedge q$ |
>    | :----------: | :----------: | :----------: |
>    | $\mathbb{T}$ | $\mathbb{T}$ | $\mathbb{T}$ |
>    | $\mathbb{T}$ | $\mathbb{F}$ | $\mathbb{F}$ |
>    | $\mathbb{F}$ | $\mathbb{T}$ | $\mathbb{T}$ |
>    | $\mathbb{F}$ | $\mathbb{F}$ | $\mathbb{T}$ |
>
>    As for the statement $p \rightarrow q$:
>
>    the **converse** is $q \rightarrow p$;
>
>    the **contrapositive** is $\neg q \rightarrow \neg p$;
>
>    the **inverse** is $\neg p \rightarrow \neg q$.
>
>    *! **Remark:** con- is a typical Lat. prefix for "with", and in- is for "not", here's the difference between converse and inverse.*
>
> 6. the **biconditional statements** such as "$p$ if and only if $q$" is denoted by $p \leftrightarrow q$.
>
>    *! in $\LaTeX$, typed with `p \leftrightarrow q`*.
>
>    the truth table: 
>
>    |     $p$      |     $q$      | $p \wedge q$ |
>    | :----------: | :----------: | :----------: |
>    | $\mathbb{T}$ | $\mathbb{T}$ | $\mathbb{T}$ |
>    | $\mathbb{T}$ | $\mathbb{F}$ | $\mathbb{F}$ |
>    | $\mathbb{F}$ | $\mathbb{T}$ | $\mathbb{F}$ |
>    | $\mathbb{F}$ | $\mathbb{F}$ | $\mathbb{T}$ |
>
> **Precedence: **$\neg, \wedge, \vee, \rightarrow, \leftrightarrow$.

**Def 4. Boolean variables **A variable whose value is either true or false. By replacing true and false by 1 and 0, **bit operations** can be defined as follows:

| $x$  | $y$  | $x \vee y$ | $x \wedge y$ | $x \oplus y$ |
| :--: | :--: | :--------: | :----------: | :----------: |
|  0   |  0   |     0      |      0       |      0       |
|  0   |  1   |     1      |      0       |      1       |
|  1   |  0   |     1      |      0       |      1       |
|  1   |  1   |     1      |      1       |      1       |

these operators can be extended to **bit strings**, sequences of 0's and 1's.

**Def 5. Consistency** Specifications is **consistent** if they don't contain conflicting requirements that can derive a **contradiction**.

**Def 6. Tautology, Contradiction and Contingency **A **tautology** is a compound proposition that is always true. A **contradiction** is a compound proposition that is always false. A **contingency** is a compound proposition that is neither a tautology nor a contradiction.

**Def 7. Logical equivalences** The compound proposition $p$ and $q$ are **logically equivalent** if $p \leftrightarrow q$ is a tautology, denoted by $p \equiv q$ or $p \Leftrightarrow q$.

*! in $\LaTeX$ typed with `p \equiv q` or `p \Leftrightarrow q`. Sometimes I'd prefer `p \iff q` for simplicity yet it compiles to become $p \iff q$, much longer and uglier than previous one.* 

**Table 1. Logical Equivalences**

| No.  |                         Equivalence                          |                Name                 |
| :--: | :----------------------------------------------------------: | :---------------------------------: |
|  1   |  $p \wedge \mathbb{T} \equiv p, p \vee \mathbb{F} \equiv p$  |            Identity laws            |
|  2   | $p \vee \mathbb{T} \equiv \mathbb{T}, p \wedge \mathbb{F} \equiv \mathbb{F}$ |           Domination laws           |
|  3   |           $p \vee p \equiv p, p \wedge p \equiv p$           |           Idempotent laws           |
|  4   |                   $\neg (\neg p) \equiv p$                   |         Double negation law         |
|  5   |   $p \vee q \equiv q \vee p, p \wedge q \equiv q \wedge p$   |          Commutative laws           |
|  6   | $(p \vee q) \vee r \equiv p \vee (q \vee r), \\(p \wedge q) \wedge r \equiv p \wedge (q \wedge r)$ |          Associative laws           |
|  7   | $(p \vee q) \wedge r \equiv (p \wedge r) \vee (q \wedge r),\\ (p \wedge q) \vee r \equiv (p \wedge q) \vee (q \wedge r)$ |          Distributive laws          |
|  8   | $\neg (p \wedge q) \equiv \neg p \vee \neg q,\\ \neg(p \vee q) \equiv \neg p \wedge \neg q$ |          De Morgen's laws           |
|  9   | $p \vee (p \wedge q) \equiv p, p \wedge (p \vee q) \equiv p$ |           Absorption laws           |
|  10  | $p \vee \neg p \equiv \mathbb{T}, p \wedge \neg p \equiv \mathbb{F}$ |            Negation laws            |
|      |             **Involving conditional statements**             |                                     |
|  11  |            $p \rightarrow q \equiv \neg p \vee q$            | Conditional-disjunction equivalence |
|  12  |      $p \rightarrow q \equiv \neg q \rightarrow \neg p$      |                                     |
|  13  |            $p \vee q \equiv \neg p \rightarrow q$            |                                     |
|  14  |       $p \wedge q \equiv \neg (p \rightarrow \neg q)$        |                                     |
|  15  |       $\neg (p \rightarrow q) \equiv p \wedge \neg q$        |                                     |
|  16  | $(p \rightarrow q) \wedge (p \rightarrow r) \equiv p \rightarrow (q \wedge r)$ |                                     |
|  17  | $(p \rightarrow r) \wedge (q \rightarrow r) \equiv (p \vee q) \rightarrow r$ |                                     |
|  18  | $(p \rightarrow q) \vee (p \rightarrow r) \equiv p \rightarrow (q \vee r)$ |                                     |
|  19  | $(p \rightarrow r) \vee (q \rightarrow r) \equiv (p \wedge q) \rightarrow r$ |                                     |
|      |            **Involving biconditional statements**            |                                     |
|  20  | $p \leftrightarrow q \equiv (p \rightarrow q) \wedge (q \rightarrow p)$ |                                     |
|  21  |  $p \leftrightarrow q \equiv \neg p \leftrightarrow \neg q$  |                                     |
|  22  | $p \leftrightarrow q \equiv (p \wedge q) \vee (\neg p \wedge \neg q)$ |                                     |
|  23  | $\neg (p \leftrightarrow q) \equiv p \leftrightarrow \neg q$ |                                     |

<HERE TO ADD MORE EQUIVALENCES WITH PROOFS IN EXERSISES>

**Def 8. Satisfiability** A compound proposition is **satisfiable** if there is an assignment of truth values to its variables that makes it true (i.e. when it is a tautology or a contingency). Otherwise the compound proposition is unsatisfiable. A particular assignment of truth values to its variables to make it true is called a **solution** to this satisfiability problem.

**Def 9. Dual** The dual of a compound proposition that contains only the logical operators $\vee$, $\wedge$ and $\neg$ is the compound proposition obtained by replacing each $\vee$ by $\wedge$, each $\wedge$ by $\vee$, each $\mathbb{T}$ by $\mathbb{F}$, and each $\mathbb{F}$ by $\mathbb{T}$. The dual of $s$ is denoted by $s^*$.

**Th.** The duals of two equivalent compound propositions are also equivalent, where these compound propositions contain only the operators $\wedge$, $\vee$ and $\neg$.

> <TO PROVE>

**Def 10. Disjunctive and *! conjunctive* normal form** Taking the disjunction of conjunctions of the variables or their negations, with one conjunction included for each combination of values for which the compound proposition is true, the resulting compound proposition is said to be in **disjunctive normal form**. *! the conjunctive normal form means taking the conjunction of the disjunctions of ...*

***! Def 11. Full disjunctive and conjunctive normal form*** *The disjunctive (and conjunctive) normal form where all the conjunctions(disjunctions) contains all the variables or their negations in the compound proposition.*

**Th. **Every compound proposition is logically equivalent to one in disjunctive normal form.

> <TO PROVE>

**Def 12. Functionally complete** A collection of logical operators is called **functionally complete** if every compound proposition is logically equivalent to a compound proposition involving only these logical operators.

> 1. $\neg$, $\wedge$ and $\vee$ form a functionally complete collection of logical operators.
>
>    <TO PROVE>
>
> 2. $\neg$ and $\wedge$ form a functionally complete collection of logical operators.
>
>    <TO PROVE>
>
> 3. $\neg$ and $\vee$ form a functionally complete collection of logical operators.
>
>    <TO PROVE>
>
> 4. the **Sheffer stroke** $\mid$ is functionally complete collection of logical operators.
>
>    *! in $\LaTeX$, typed with `\mid` or `\vert` or `|`*
>
>    The truth table:
>
>    |     $p$      |     $q$      |  $p \mid q$  |
>    | :----------: | :----------: | :----------: |
>    | $\mathbb{T}$ | $\mathbb{T}$ | $\mathbb{F}$ |
>    | $\mathbb{T}$ | $\mathbb{F}$ | $\mathbb{T}$ |
>    | $\mathbb{F}$ | $\mathbb{T}$ | $\mathbb{T}$ |
>    | $\mathbb{F}$ | $\mathbb{F}$ | $\mathbb{T}$ |
>
>    <TO PROVE>
>
> 5. the **Peirce arrow** $\downarrow$ is a functionally complete collection of logical operators.
>
>    *! in $\LaTeX$, typed with `\downarrow`*
>
>    The truth table:
>
>    |     $p$      |     $q$      | $p \downarrow q$ |
>    | :----------: | :----------: | :--------------: |
>    | $\mathbb{T}$ | $\mathbb{T}$ |   $\mathbb{F}$   |
>    | $\mathbb{T}$ | $\mathbb{F}$ |   $\mathbb{F}$   |
>    | $\mathbb{F}$ | $\mathbb{T}$ |   $\mathbb{F}$   |
>    | $\mathbb{F}$ | $\mathbb{F}$ |   $\mathbb{T}$   |
>
>    **Lemma 1. **$p \downarrow p \equiv \neg p$
>
>    > *! **Pf. **From the truch table*
>
>    **Lemma 2. **$(p \downarrow q) \downarrow (p \downarrow q) \equiv p \vee q$
>
>    <TO PROVE>

****

### Predicate calculus

**Def 13. Predicate** The **predicate** refers to a property that the subject of the statement can have. The statement $P(x)$ is also called the value of the **propositional function** $P$ at $x$, where $P$ denotes the predicate. A statement of the form $P(x_1, x_2, \cdots, x_n)$ is the value of the propositional function $P$ at the $n$-tuple $(x_1, x_2, \cdots, x_n)$. $P$ is also called an $n$**-place predicate** or an **$n$-ary predicate**.

**Def 14. Preconditions and Postconditions** The statements that describe valid input are known as **preconditions** and the conditions that the output shoud satisfy when the program has run are known as **postconditions**.

**Def 15. Quantifiers** Quantification expresses the extend to which a predicate is true over a range of elements. The area of logic that deals whth predicates and quantifiers is called the **predicate calculus**.

**Def 16. Domain** Many statements assert that a property is true for all values of a variable in a particular domain, called the **domain of discourse**, **universe of discourse** or often just referred to as **domain**.

> **Quantifiers:**
>
> 1. the **universal quantifier** that means "for all" or "for every" is denoted by $\forall$
>
>    *! in $\LaTeX$, typed with `\forall`.*
>
> 2. the **existial quantifier** that means "there exists" is denoted by $\exists$
>
>    *! in $\LaTeX$, typed with `\exists`*
>
> 3. the **unickness quantifier** that means "there exists a unique" is denoted by $\exist!$ or $\exist_1$
>
> the quantifiers have higher precedence than all logical operators from propositional calculus.

**Th. De Morgan's Laws for Quantifiers** $\neg \exists x P(x) \equiv \forall x \neg P(x), \neg \forall x P(x) \equiv \exists x \neg P(x)$

**Table 2. Null quantification** Assuming that the domain is nonempty and $x$ does not occur as a free variable in $A$:

| $(\forall x P(x)) \vee A \equiv \forall x(P(x) \vee A), (\exists x P(x)) \vee A \equiv \exist x (P(x) \vee A)$ |
| :----------------------------------------------------------: |
| $(\forall x P(x)) \wedge A \equiv \forall x (P(x) \wedge A), (\exists x P(x)) \wedge A \equiv \exists x(P(x) \wedge A)$ |
| $\forall x(A \rightarrow P(x)) \equiv A \rightarrow \forall x P(x), \exists x (A \rightarrow P(x)) \equiv A \rightarrow \exists x P(x)$ |
| $\forall x (P(x) \rightarrow A) \equiv \exists x P(x) \rightarrow A, \exists x(P(x) \rightarrow A) \equiv \forall x P(x) \rightarrow A$ |

**Def 17. Prenex normal form (PNF)** A statement is in **prenex normal form** if and onlt if it is of the form$Q_1x_1Q_2x_2\cdots Q_kx_kP(x_1, x_2, \cdots, x_k)$, where each $Q_i$ is either the existential quantifier or the universal quantifier, and $P(x_1, x_2, \cdots, x_k)$ is a predicate involving no quantifiers.

**Th. **Every statement formed from propositional variables, predicates, $\mathbb{T}$, and $\mathbb{F}$ using logical connectives and quantifiers is equivalent to a statement in prenex normal form.

<TO PROVE>

### Inference & Proof

**Def 18. Argument** A sequence of statements that end with a conclusion is called an argument. All but the final proposition in the argument are called **premises** and the final proposition is called the **conclusion**. An argument is **valid** if the truth of all its premises implies that the conclusion is true.

**Def 19. Argument form** An argument form in propositional logic is a sequence of compound proposition involving propositional variables. An argument form is valid if no matter which particular propositions are substituted for the propositional variables in its premises, the conclusion is true if the premises are all true.

**Table 3. Rules of Inference**

|                      Rule of inference                       |            Name            |
| :----------------------------------------------------------: | :------------------------: |
|             $p\\ p \rightarrow q\\\therefore q$              |        Modus ponens        |
|       $\neg q\\ p \rightarrow q\\ \therefore \neg p $        |       Modus tollens        |
| $p \rightarrow q\\ q \rightarrow r \\ \therefore p \rightarrow r $ |   Hypothetical syllogism   |
|             $p \vee q \\ \neg p \\ \therefore q$             |   Disjunctive syllogism    |
|                  $p \\ \therefore p \vee q$                  |          Addition          |
|                 $p \wedge q \\ \therefore p$                 |       Simplification       |
|              $p \\ q \\ \therefore p \wedge q$               |          Conjunc           |
|      $p \vee q \\ \neg p \vee r \\ \therefore q \vee r$      |         Resolusion         |
|             $\forall x P(x) \\ \therefore P(c)$              |  Universal instantiation   |
| $P(c) \mathrm{\ for\ an\ arbitary}\ c \\ \therefore \forall xP(x)$ |  Universal generalization  |
| $\exists x P(x) \\ \therefore P(c) \mathrm{\ for\ some\ element}\ c$ | Existential instantiation  |
| $P(c) \mathrm{\ for\ some\ element\ }c\\ \therefore \exists xP(x)$ | Existential generalization |
| $\forall x (P(x) \rightarrow Q(x)) \\ P(a), \mathrm{\ where}\ a \mathrm{\ is\ a\ particular\ element\ in\ the\ domain}\\ \therefore Q(a)$ |   Universal modus ponens   |
| $\forall x (P(x) \rightarrow Q(x)) \\ \neg Q(a), \mathrm{\ where\ } a \mathrm{\ is\ a\ particular\ element\ in\ the\ domain} \\ \therefore \neg P(a)$ |  Universal modus tollens   |
| $\forall x(P(x) \rightarrow Q(x))\\ \forall x(Q(x) \rightarrow R(x)) \\ \therefore \forall x(P(x) \rightarrow R(x))$ |   Universal transitivity   |

**Def 20. Theorem (facts / results), Propositions, Axioms (postulates), Lemma, Corollary & Conjecture** A theorem(or a fact, a result) is a statement that can be shown to be true. Less important theorems sometimes are called propositions. Axioms(or postulates) are statements we assume to be true. A lemma(Pl. lemmas or lemmata) is a less important theorem that is helpful in the proof of other results. A corollary is a theorem that can be directly established from a theorem that has been proved. A conjecture is a statement that is being proposed to be a true statement, usually on the basis of some partial evidence.

**Def 21. Direct proof & Indirect proof** A direct proof of a conditional statement $p \rightarrow q$ is constructed when the first step is the assumption that $p$ is true; subsequent steps are constructed using rules of inference, with the final step showing that $q$ must also be true. Indirect proofs are those that are not direct proofs

**Def 22. Vacuous proof** In statement $p \rightarrow q$, prove that $p$ is false.

**Def 23. Trivial proof** In statement $p \rightarrow q$, prove that $q$ is a tautology.

**Def 24. Proof by contraposition** Using the fact that $p \rightarrow q \equiv \neg q \rightarrow \neg p$, prove that its contrapositive is true.

**Def 25. Proof by contradiction** If $\neg p \rightarrow(r \wedge \neg r)$ is shown, we can prove that $p$ is true.

**Def 26. Exhaustive proof ** Preceed by exhausting all possibilities.

**Def 27. Existence proof** A proof of a proposition $\exists x P(x)$ is called an existence proof. It is called **constructive** if it's given by finding a **witness** $a$ that $P(a)$, and non-constructive otherwise.

## 2 Basic Structures: Sets, Functions, Sequences, Sums, and Matrices

### Sets

**Def 1. Set** A set is an unordered collection of distinct objects, called **elements** or **members** of the set. A set is called to **contain** its elements, denoted $a \in A$ *! in $\LaTeX$, typed with `a \in A`*. Ways to describe a set: **roster method, set builder notation**.

> Some importent sets:
>
> 1. $\mathbb{N} = \{0, 1, 2, 3, \cdots\}$,  the set of all natural numbers *!`\mathbb{N}` in $\LaTeX$*
>
> 2. $\mathbb{Z} = \{\cdots, -2, -1, 0, 1, 2, \cdots\}$, the set of all integers
>
> 3. $\mathbb{Z}^+ = \{1, 2, 3, \cdots\}$, the set of all positive integers
>
> 4. $\mathbb{Q} = \{\frac p q \mid p \in \Z, q \in \Z, q \ne 0\}$, the set of all rational numbers
>
> 5. $\R$, the set of all real numbers
>
> 6. $\R^+$, the set of all positive real numbers
>
> 7. $[a, b] = \{x \mid a \leqslant x \leqslant b\}$
>
>    $[a, b) = \{x \mid a \leqslant x < b\}$
>
>    $(a, b] = \{x \mid a < x \leqslant b\}$
>
>    $(a, b) = \{x \mid a < x < b\}$

**Def 2. Singleton set **A set with one element is called a singleton set.

> Relationships between sets:
>
> 1. Equal: $A = B := \forall x(x \in A \leftrightarrow x \in B)$
> 2. Subset and superset: $A \sube B := \forall x(x \in A \rightarrow x \in B)$ *! in $\LaTeX$, typed with `\sube` or `\subseteq`*
> 3. Proper subset: $A \sub B := \forall x(x \in A \rightarrow x \in B) \wedge \exists x(x \in B \wedge x \not \in A)$ *! `\sub` or `\subset` in $\LaTeX$*

**Th.** For every set $S$, $\varnothing \sube S$ and $S. \sube S$

**Def 3. Cardinality** Let $S$ be a set. If there are exactly $n$ distinct elements in $S$ where $n$ is a nonnegative integer, we say that $S$ is a **finite** **set** and that $n$ is the cardinality of $S$, denoted by $|S|$. A set is said to be **infinite** if it is not finite.

**Def 4. Power set** Given a set $S$, the power set of $S$ is all subsets of the set $S$, denoted by $\mathcal{P}(S)$.

**Def 5. Ordered $n$-tuple** the ordered $n$-tuple $(a_1, a_2, \cdots, a_n)$ is the ordered collection that has $a_1$ as its first element, $a_2$ as its second element, and $a_n$ as its $n$th element. Specially, ordered $2$-tuples are called **ordered pairs**

**Def 6. Cartesian Product **Let $A$ and $B$ be sets. The Cartesian product of $A$ and $B$, denoted by $A \times B$, is the set of all ordered pairs $(a, b)$, where $a \in A$ and $b \in B$. *`A \times B` in $\LaTeX$* The Cartesian product of the sets $A_1, A_2, \cdots, A_n$, denoted by $A_1 \times A_2 \times \cdots \times A_n$ is the set of ordered $n$-tuples $\{a_1, a_2, \cdots, a_n\}$, where $a_i$ belongs to $A_i$.

> Set operations:
>
> 1. The **union** of $A$ and $B$, denoted by $A \cup B$
>
>    *! in $\LaTeX$, typed with `A \cup B`*
>
>    $A \cup B := \{x \mid x \in A \vee x \in B\}$
>
> 2. The **intersection** of $A$ and $B$, denoted by $A \cap B$
>
>    *! in $\LaTeX$, typed with `A \cap b`*
>
>    $A \cap B:= \{x \mid x \in A \wedge x \in B\}$
>
>    if $A \cap B = \varnothing$, they are called **disjointed**
>
> 3. The **difference** of $A$ and $B$, denoted by $A \backslash B$ or $A-B$
>
>    *! in $\LaTeX$, typed with `A \backslash B`*
>
>    $A \backslash B := \{x \mid x \in A \wedge x \notin B\}$
>
> 4. Let $U$ be the universal set. The **complement** of the set $A$, denoted by $\bar A$
>
>    *! in $\LaTeX$, typed with `\bar A` or `\overline A`*
>
>    $\bar A := U - A$

**Table 1. Set Identities**

|                           Identity                           |        Name         |
| :----------------------------------------------------------: | :-----------------: |
|            $A \cap U = A, A \cup \varnothing = A$            |    Identity laws    |
|       $A \cup U = U, A \cap \varnothing = \varnothing$       |   Domination laws   |
|                 $A \cup A = A, A \cap A = A$                 |   Idempotent laws   |
|                $\overline{(\overline A)} = A$                | Complementation law |
|          $A \cap B = B \cap A, A \cup B = B \cup A$          |  Commutative laws   |
| $A \cup (B \cup C) = (A \cup B) \cup C, \\ A \cap (B \cap C) = (A \cap B) \cap C$ |  Associative laws   |
| $A \cup (B \cap C) = (A \cup B) \cap (A \cup C), \\ A \cap (B \cup C) = (A \cap B) \cup (A \cap C)$ |  Distributive laws  |
| $\overline{A \cap B} = \overline A \cup \overline B, \overline{A \cup B} = \overline A \cap \overline B$ |  De Morgen's laws   |
|        $A \cup (A \cap B) = A, A \cap (A \cup B) = A$        |   Absorption laws   |
|  $A \cup \overline A = U, A \cap \overline A = \varnothing$  |   Complement laws   |

**Def 7. Atomic sets** The sets used to construct more complicated combinations of these sets are called atomic sets. 

**Def 8. Membership tables** Consider each combination of the atomic sets that an element can belong to. To indicate an element is in a set, $1$ is used, otherwise, $0$ is used.

**Def 9. Generalized union and intersection**

$\bigcup \limits_{i = 1}^nA_i = A_1 \cup A_2 \cup \cdots \cup A_n = \{x \mid \bigvee \limits_{i = 1}^n(x \in A_i)\}$

$\bigcap \limits_{i = 1}^nA_i = A_1 \cap A_2 \cap \cdots \cap A_n = \{x \mid \bigwedge \limits_{i = 1}^n(x \in A_i)\}$

$\bigcup \limits_{i = 1}^{\infty}A_i = A_1 \cup A_2 \cup \cdots \cup A_n \cup \cdots = \{x \mid \bigvee \limits_{i = 1}^{\infty}(x \in A_i)\}$

$\bigcap \limits_{i = 1}^{\infty}A_i = A_1 \cap A_2 \cap \cdots \cap A_n \cap \cdots = \{x \mid \bigwedge \limits_{i = 1}^{\infty}(x \in A_i)\}$

**Def 10. Multiset** A multiset is an unordered collection of elements where an element can occur as a member more than once. The notation $\{m_1 \cdot a_1, m_2 \cdot a_2 \cdot\dots \cdot m_n \cdot a_n\}$ denotes the multiset with element $a_i$ occurring $m_i$ times, where $m_i$ is called the **multiplicities** of the element $a_i$.

> The operations on multisets:
>
> 1. The **union** of the multisets $P$ and $Q$ is the multiset in which the multiplicity of an element is the maximum of its multiplicities in $P$ and $Q$, denoted by $P \cup Q$
> 2. The **intersection** of $P$ and $Q$ is the multiset in which the multiplicity of an element is the minimum of its multiplicities in $P$ and $Q$, denoted by $P \cap Q$
> 3. The **difference** of $P$ and $Q$ is the multiset in which the multiplicity of an element is the multiplicity of the element in $P$ less its multiplicity in $Q$ unless this difference is negative, in which case the multiplicity is $0$, denoted by $P \backslash Q$ or $P - Q$
> 4. The sum of  $P$ and $Q$ is the multiset in which the multiplicity of an element is the sum of multiplicities in $P$ and $Q$, denoted $P + Q$

**Def 11. Successor** The successor of the set $A$ is $A \cup \{A\}$

**Def 12. Jaccard similarity** $J(A, B) = \frac{|A \cap B|}{|A \cup B|}$, while $J(\varnothing, \varnothing)=1$.

> Properties of the Jaccard similarity:
>
> 1. $J(A, A) = 1$.
> 2. $J(A, B) = J(B, A)$.
> 3. $J(A, B) = 1 \iff A = B$.
> 4. $J(A, B) \in [0, 1]$.
>
> <TO PROVE>

**Def 13. Jaccard distance** $d_J(A, B) = 1 - J(A, B)$.

> Properties of the Jaccard distance:
>
> 1. $d_J(A, A) = 0$.
> 2. $d_J(A, B) = d_J(B, A)$.
> 3. $d_J(A, B) = 0 \iff A = B$.
> 4. $d_J(A, B) \in [0, 1]$.
> 5. $d_J(A, C) \leqslant d_J(A, B) + d_J(B, C)$, indicating $d_J$ is a metric.
>
> <TO PROVE>

**Def 14. Fuzzy set** Every elements in a fuzzy set has a **degree of menbership**, which is a real number between 0 and 1.

>Operations on a fuzzy set:
>
>1. The **complement** of a fuzzy set $S$ is the fuzzy set $\bar S$, with the degree of the menbership of an element is $\bar S$ equal to 1 minus the degree of membership of this element in $S$.
>2. The **union** of two fuzzy sets $A$ and $B$ is the fuzzy set $A \cup B$, where the degree of membership of an element is the maximum of the degrees of membership of this element in $A$ and in $B$.
>3. The **intersection** of two fuzzy sets $A$ and $B$ is the fuzzy set $A \cap B$, where the degree of membership of an element is the minimum of the degrees of membership of this element in $A$ and in $B$.  

### Functions

<TBC>

## 3 Algorithms

### Definition and examples of algorithms

**Def 1. Algorithm** An algorithm is a finite sequence of precise instructions for performing a computation or for solving a problem.

> Properties of algorithms:
>
> 1. **Input**
> 2. **Output**
> 3. **Definiteness**
> 4. **Correctness**
> 5. **Finiteness**
> 6. **Effectiveness**
> 7. **Generality**

**Alg 1. Sequential search**

```pseudocode
procedure linear_search(x: int, a[1] to a[n]: array of int)
	i := 1
	while (i <= n and x != a[i])
		i := i + 1
	if i <= n then 
		location := i
	else 
		location := 0
	return location
```

**Alg 2. Binary search**

```pseudocode
procedure binary_search(x: int, a[1] to a[n]: an increasing array of int)
	i := 1
	j := n
	while i < j
		m := (i + j) / 2;
		if x > a[m] then
			i := m + 1
		else
			j := m
	if x = a[i] then 
		location := i
	else
		location := 0
	return location
```

**Alg 3. Bubble sort**

```pseudocode
procedure bubble_sort(a[1] to a[n]: an array of int)
	for i := 1 to n - 1
		for j := 1 to n - 1
			if a[j] > a[j + 1] then
				swap a[j], a[j + 1]
```

**Alg 4. Insertion sort**

```pseudocode
procedure insertion_sort(a[1] to a[n]: an array of int)
	for j := 2 to n
		i := 1
		while a[j] > a[i]
			i := i + 1
		m := a[j]
		for k := 0 to j - i - 1
			a[j - k] = a[j - k - 1]
		a[i] := m
```

**Alg 5. Naive string matcher**

```pseudocode
procedure naive_string_matcher(n, m: positive int, m <= n, p[1] to p[m], t[1] to t[n]: string)
	for s := 0 to n - m
		j := 1
		while (j <= m and t[s + j] = p[j])
			j := j + 1
		if j > m then
			print s "is a valid shift"
```

**Def 2. Greedy algorithm** Algorithms that make what seems to be the best choice at each step are called greedy algorithms.

**Th. Halting problem** There is no procedure that takes as input a program and input and determines whether the program will eventually stop when run with this input.

> **Pf.** Assume that there is a procedure called $H(P, I)$ that can do such thing, taking as input procedure $P$ and input $I$. We construct a simple procedure $K(P)$, which does the opposite of what the output $H(P, P)$ specifies. If the output of $H(K, K)$ is "loops forever", then $K(K)$ halts, vise versa. Here comes the contradiction.

**Alg 6. Ternary search**

*! written according to the questions*

```pseudocode
procedure ternary_search(x: int, a[1] to a[n]: increasing array of int)
	i := 1
	j := n
	while i < j
		m := (i + j) < 3
		n := m * 2
		if x < a[m] then
			j := m - 1
		else if x > a[n] then
			i := n + 1
		else
			i := m
			j := n
	if a[i] = x then
		location := x
	else 
		location := 0
	return location
```

**Alg 7. Selection sort**

*! written according to the questions*

```pseudocode
procedure selection_sort(a[1] to a[n]: array of int)
	for i := 1 to n - 1
		index = i
		for j := i to n
			if a[j] < a[index] then
				index = j
		swap a[index], a[i]
```

**Alg 8. Deferred acceptance algorithm/Gale-Shapley algorithm**

*! written according to the questions*

```pseudocode
procedure deferred_acceptance(suitor[1] to suitor[n]: array of suitors, suitee[1] to suitee[n]: array of suitees)
	while some suitors are not having their proposals pending
		unpaired suitors propose to their highest ranked suitees who have not yet rejected them
		sutees receiving proposal suspend only one from highest ranked suitors and reject the rest
	all pending proposals get accepted
```

**Alg 9. Boyer-Moore majority vote algorithm**

*! written according to the questions*

```pseudocode
procedure majority_vote(a[1] to a[n]: array of int)
	majority := a[1]
	counter := 0
	for i := 1 to n
		if majority = a[i] then
			counter := counter + 1
		else if counter > 0 then
			counter := counter - 1
		else majority := a[i]
	if counter = 0 then
		print "No majority element"
	else print majority
```

### The growth of functions

