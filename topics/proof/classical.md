# Classical Logic and Proof


This section contains a brief overview of how Mathematical propositions are
stated and proved using classical logic. We will see later that this is not the
only foundational theory of logic and proof.

In fact, classical logic is not well suited to propositions and proof in a
computational context (we will see why later). Alternative foudational theories
are used (Martin-Löf type theory, calculus of constructions) when creating type
theories concerning propositions and proof (for example dependent types).


## Statements

A _statement_ is something that can be clearly interpreted as being true or
false.

Examples:

1. 1 + 1 = 2
2. The square root of 2 is irrational
3. There are a finite number of primes

Here 1. and 2. are true, 3. is false.


## Predicates

A _predicate_ is a statement involving a symbol that is true or false when we
substitute the symbol with an element of a set. For example:

> The natural number `x` is less than `10`.

Let's call the predicate `P(x)` then `P(9)` is true and `P(10)` is false. We
have constructed a _truth function_ from the set of natural numbers, ℕ, to the
set of Booleans, `B = {t, f}`.

> `T : ℕ -> B` where `T(n) = t` if `P(n)` is true and `T(n) = f` if `P(n)` is false

NB: This is not well suited to a computational context because for a general
predicate involving natural numbers we'd have to compute an infinite number of
values to know the truth function.


## Quantifiers

We can make statements that _quantify over_ a predicate.

Let `S` be a subset of `X` (the domain of definition of the predicate). Then we
can for the following statements.

> for all `x ∈ S`, `P(x)` is true
>
> for some `x ∈ S`, `P(x)` is true

The mathematical symbols used are the _universal quantifier_ ∀ for the first and
the _existential quanitifier_ ∃ for the second.

> `∀ x ∈ S: P(x)`
>
> `∃ x ∈ S: P(x)`

Examples:

1. `∀ n ∈ ℕ: ` `n` is even.
2. `∃ n ∈ ℕ: ` `n` is even.

The first is false the second is true.


## Conjunctions

_Conjunctions_ are used to combine existing statements. The regular conjunctions
we use are _and_, _or_, _imples_, _if and only if_ denoted ∧, ∨, ⇒, ⇔.

Their meaning can be given using a _truth table_ which is a way to write down
the truth function for the conjunction.

### And, ∧

| P     | Q     | P ∧ Q |
|-------|-------|-------|
| true  | true  | true  |
| true  | false | false |
| false | true  | false |
| false | false | false |

### Or, ∨

| P     | Q     | P ∨ Q |
|-------|-------|-------|
| true  | true  | true  |
| true  | false | true  |
| false | true  | true  |
| false | false | false |

### Imples, ⇒

| P     | Q     | P ⇒ Q |
|-------|-------|-------|
| true  | true  | true  |
| true  | false | false |
| false | true  | true  |
| false | false | true  |

### Imples, ⇔ 

| P     | Q     | P ⇔ Q |
|-------|-------|-------|
| true  | true  | true  |
| true  | false | false |
| false | true  | false |
| false | false | true  |


## Tautology and Contradiction

A statement is called _tautology_ if it is true whatever truth values are
subsituted for the symbols it contains. 

Examples:

1. P ∨ (¬P)
2. P ∧ (Q ∨ R) ⇒ (P ∧ Q) ∨ (P ∧ R) 

A statement is called a _contradiction_ if it is false whatever truth values are
substituted for the symbols it contains.

Examples:

1. P ∧ (¬P)
2. ¬P where P is a tautology

NB: ¬ is the symbol for logical negation.

We'll see that P ∧ (¬P) is not a tautology in some other logics.


## Inference

A tautology (P₁ ∧ P₂ ∧ … ∧ P\_n) ⇒ Q is called an _inference_. If the statements
on the left hand side of the implications are true then we infer that Q is true.


## Proof

A proof of P ⇒ Q given the truth of the hypothesis statements H₁, H₂, … H\_p is a
sequence of steps, S\_k, starting with S₁ = P and ending with S\_n = Q. Each step is
equal to a hypothesis statement or a statement or predicate satisfying:

> (S₁ ∧ … S\_{k-1}) ⇒ S\_k

That is, we infer the next step from all the previous ones.


## Standard Deductions

Standard patterns called _deductions_ are used in proofs to replace statements
with logically equivalent statements that are easier to prove. 

1. _Contrapositive_: P ⇒ Q is equivalent to ¬Q ⇒ ¬P
2. _Proof by contradiction_: P is equivalent to (¬P) ⇒ C (where C is a
   contradiction)
3. P ⇔ Q is equivalent to (P ⇒ Q) ∧ (Q ⇒ P)


## Examples

### Prove that there is no smallest rational number greater than √2.

Let's use _proof by contradiction_ to deduce that this is equivalent to:

> (∃ a smallest rational number greater than √2) ⇒ C (where C is a
> contradiction)

To prove this we follow our proof recipe, our first step is the left hand side
of the implication.

### *Step 1* ∃ a smallest rational number greater than √2

Let _S_ be the set of rational numbers greater that √2.

> S = { s ∈ ℚ : s > √2 }

Let _ι_ be the smallest element of S, which exists due to *Step 1*.

### *Step 2* (ι - √2) > 0

We can use _contradiction_ again to deduce Step 2:

> (ι - √2 ≤ 0) ⇒ C (for some contradiction C)
>
> ι - √2 ≤ 0
> ⇒ ι ≤ √2
> ⇒ ¬(ι ∈ S) (a contradiction due to definition of ι)

### *Step 3* ∃ a rational number r between √2 and ι

Again let's use _contradiction_ to deduce Step 3:

> ¬(∃ r ∈ ℚ: √2 < r < ι) ⇒ C (for some contradiction C)

Choose a fixed q ∈ ℕ and let T = { p/q : p ∈ ℤ }. Let m be the smallest member of
T greater than ι (why does this exist?). The rational number m can be written as
p/q because from the definition of T.

We know:
* There are no rationals between √2 and ι (by hypothesis in this step)
* (p-1)/q < ι (by the construction of p/q in the previous paragraph)
* p/q ≥ ι (by the construction of p/q, non-strict inequality because ι could be
  a member of T)

So we deduce that (p-1)/q < √2 and therefore

> p/q - (p-1)/q > ι - √2
> ⇒ 1/q > ι - √2

We can choose q large enough such that this inequality is false. So we've found
our contradiction C. We conclude that ∃ r ∈ ℚ: √2 < r < ι.

This gives us our overall contradiction.

> The existence of r < ι contradicts the statement that ι was the least rational
> greater than √2.
