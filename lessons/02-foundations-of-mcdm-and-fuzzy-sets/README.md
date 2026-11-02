# Lesson 02 — Foundations of MCDM and Fuzzy Sets

These notes capture my understanding of the second class session: translating a real-world decision problem into a mathematical model, moving from a single objective to multiple conflicting criteria, distinguishing MADM from MODM, and introducing crisp and fuzzy sets.

## 1. From a real-world problem to a mathematical solution

Operations research begins by translating an unstructured real-world problem into a mathematical model:

```text
Real-world problem → Mathematical model → Solution → Interpretation
```

A mathematical optimization model normally contains four components:

1. **Decision variables:** quantities controlled by the decision-maker.
2. **Objective function:** the performance measure to maximize or minimize.
3. **Constraints:** limitations that every feasible decision must satisfy.
4. **Variable domains:** restrictions such as non-negativity, integrality, or binary values.

For a production problem with two products, the decision variables may be

$$
x_1=\text{quantity of product 1}, \qquad
x_2=\text{quantity of product 2}.
$$

A profit objective can be written as

$$
\max z_1=5x_1+2x_2,
$$

subject to resource constraints such as

$$
2x_1+3x_2\leq100,
$$

$$
1.5x_1+x_2\leq500,
$$

and non-negativity conditions

$$
x_1,x_2\geq0.
$$

The set of all points that satisfy every constraint is the **feasible region**. Optimization searches this region for a decision that gives the best objective value.

> The numerical model above reconstructs the structure shown in the class notes. The original real-world units and the complete set of constraints were not recorded, so the coefficients should be read as an illustrative formulation rather than a complete production case.

## 2. Continuous, integer, and binary decisions

The correct variable domain depends on what the variable represents.

### Linear programming

In a **linear program (LP)**, the objective and constraints are linear and the variables are continuous unless stated otherwise. Values such as $x_1=2.4$ are valid when a variable represents time, weight, volume, or another divisible quantity.

### Integer linear programming

If all decision variables must be whole numbers, the model is an **integer linear program (ILP)**:

$$
x_1,x_2\in\mathbb{Z}_{\geq0}.
$$

This is appropriate for indivisible entities such as machines, employees, or vehicles.

### Mixed-integer linear programming

A **mixed-integer linear program (MILP)** contains both integer and continuous variables. For example,

$$
x_1\in\mathbb{Z}_{\geq0}, \qquad x_2\in\mathbb{R}_{\geq0}.
$$

A **binary variable** is a special integer variable restricted to

$$
y\in\{0,1\}.
$$

It can represent a yes/no decision, such as whether to open a facility, select a project, or activate a constraint.

## 3. From one objective to multiple criteria

The profit model has one objective:

$$
\max z_1=5x_1+2x_2.
$$

Real decisions rarely depend on profit alone. The decision-maker may also care about cost, environmental impact, risk, quality, or social effects. A second objective might therefore be

$$
\min z_2=0.5x_1+0.2x_2.
$$

The two objectives can conflict: increasing production may improve profit while also increasing cost or environmental damage. Such conflict creates a **trade-off**. In general, no feasible solution simultaneously gives the individually best value of every objective.

The coefficients in $z_2$ are also taken from the class notes. If this minimization objective were used alone with only non-negativity and upper-bound resource constraints, the trivial solution $x_1=x_2=0$ would minimize it. A meaningful full model would therefore require the profit objective, minimum-demand requirements, production targets, or other constraints.

## 4. Multiple-Criteria Decision-Making

**Multiple-Criteria Decision-Making (MCDM)** is the general field concerned with decisions evaluated under two or more criteria, which are often conflicting.

The notation in the class notes uses

$$
A_1,A_2,\ldots,A_m
$$

for alternatives and

$$
C_1,C_2,\ldots,C_n
$$

for criteria. MCDM is commonly divided into two broad problem families:

```text
MCDM
├── MADM: choose or rank known alternatives
└── MODM: design a solution by optimizing decision variables
```

## 5. MADM: Multiple-Attribute Decision-Making

In **Multiple-Attribute Decision-Making (MADM)**, a finite set of alternatives is known in advance. Each alternative is evaluated against several attributes or criteria.

For example, suppose three laptops are compared using price, performance, and battery life:

| Alternative | Price | Performance | Battery life |
|---|---:|---:|---:|
| $A_1$ | 900 | 8 | 7 |
| $A_2$ | 1100 | 10 | 6 |
| $A_3$ | 1000 | 9 | 9 |

The rows are alternatives, the columns are criteria, and the table is a **decision matrix**. The task is to select the preferred alternative or rank all alternatives while accounting for criterion direction, importance, and trade-offs.

Methods listed in the class notes as MADM methods include:

- **AHP — Analytic Hierarchy Process**
- **TOPSIS — Technique for Order Preference by Similarity to Ideal Solution**
- **ANP — Analytic Network Process**

The defining feature is that the alternatives already exist; the method evaluates them rather than generating a new design.

## 6. MODM: Multiple-Objective Decision-Making

In **Multiple-Objective Decision-Making (MODM)**, alternatives are not limited to a short predetermined list. A candidate solution is generated by assigning values to decision variables while respecting the constraints.

The production model is an MODM problem when both objectives are considered:

$$
\begin{aligned}
\max \quad & z_1=5x_1+2x_2,\\
\min \quad & z_2=0.5x_1+0.2x_2,\\
\text{subject to}\quad
&2x_1+3x_2\leq100,\\
&1.5x_1+x_2\leq500,\\
&x_1,x_2\geq0.
\end{aligned}
$$

Every feasible pair $(x_1,x_2)$ is a possible alternative, so the alternative set may be very large or infinite.

### Linear and nonlinear MODM

- If all objective functions and constraints are linear, the model is a **multi-objective linear program (MOLP)**.
- If at least one relevant function is nonlinear, the model may be a **multi-objective nonlinear program (MONLP)**.
- **Goal programming** is a solution approach that specifies desired target levels and minimizes undesirable deviations from those targets.

## 7. MADM versus MODM

| Aspect | MADM | MODM |
|---|---|---|
| Alternatives | Finite and known in advance | Generated through decision variables |
| Typical task | Selection, ranking, or sorting | Design and optimization |
| Main representation | Decision matrix | Objectives, constraints, and variable domains |
| Example | Choosing one laptop from a catalog | Designing a production plan |
| Methods in the notes | AHP, TOPSIS, ANP | MOLP, MONLP, goal programming |

A useful shortcut is:

> **MADM evaluates existing options; MODM creates feasible options.**

## 8. Criteria, attributes, and objective functions

The three terms are related but should not always be treated as exact synonyms:

- A **criterion** is a general basis for evaluation, such as cost, quality, or risk.
- An **attribute** is a measurable property used to describe an alternative, especially in MADM.
- An **objective function** is a mathematical expression to maximize or minimize, especially in MODM.

Thus, price may be a criterion in a laptop decision matrix, while total cost may be represented by an objective function $z_2(x)$ in an optimization model.

## 9. Crisp sets

Let the universe be

$$
X=\{1,2,3,\ldots,10\}.
$$

Define the set of numbers greater than 2:

$$
A=\{3,4,5,\ldots,10\}.
$$

Its membership function is

$$
\mu_A(x)=
\begin{cases}
1, & x>2,\\
0, & x\leq2.
\end{cases}
$$

Every element either belongs to $A$ or does not. This is a **crisp set**, so membership is binary:

$$
\mu_A(x)\in\{0,1\}.
$$

## 10. Fuzzy sets

Now consider the concept “numbers close to 2.” Unlike “greater than 2,” the word *close* has no sharp universal boundary. A fuzzy set represents this gradual concept by assigning each element a degree of membership:

$$
\mu_B(x)\in[0,1].
$$

One illustrative definition could give

$$
\mu_B(2)=1, \qquad
\mu_B(1)=\mu_B(3)=0.5, \qquad
\mu_B(4)=0.
$$

Using standard fuzzy-set notation, this finite example can be written as

$$
B=\left\{
\frac{0.5}{1},
\frac{1}{2},
\frac{0.5}{3},
\frac{0}{4}
\right\}.
$$

Here $0.5/1$ means that the element $1$ has membership degree $0.5$; it is not an arithmetic fraction. The exact membership values depend on how the concept “close to 2” is modeled.

The core distinction is:

| Crisp set | Fuzzy set |
|---|---|
| Sharp boundary | Gradual boundary |
| Membership is 0 or 1 | Membership can be any value in $[0,1]$ |
| Example: numbers greater than 2 | Example: numbers close to 2 |

Lotfi A. Zadeh introduced fuzzy sets in his 1965 paper *Fuzzy Sets*.

## 11. Fuzziness is not probability

Probability and fuzzy membership both use numbers between 0 and 1, but they describe different ideas.

- **Probability** represents uncertainty about whether an event will occur: “The probability of rain tomorrow is 0.7.” Tomorrow it will either rain or not rain; the event is uncertain.
- **Fuzzy membership** represents the degree to which something satisfies a vague concept: “Today’s temperature belongs to the fuzzy concept *hot* with degree 0.7.” The boundary of *hot* is gradual.

Therefore, a membership value of 0.7 is not automatically a 70% probability.

## 12. Soft computing and uncertainty

The class notes connect fuzzy theory, probability theory, and evolutionary algorithms with **soft computing**. These tools allow useful reasoning or optimization when exact classical formulations are difficult:

- **Fuzzy methods** model vagueness and gradual concepts.
- **Probability theory** models randomness and uncertainty about events.
- **Evolutionary algorithms** provide approximate search and optimization inspired by biological evolution.

These approaches are related but not interchangeable. In particular, evolutionary algorithms are primarily optimization techniques rather than a theory of uncertainty.

## Exam-ready checklist

- A mathematical optimization model contains decision variables, objective functions, constraints, and variable domains.
- The feasible region contains every decision satisfying all constraints.
- LP uses linear relationships and continuous variables; ILP requires integer variables; MILP mixes integer and continuous variables.
- Binary variables encode yes/no decisions using $\{0,1\}$.
- Multiple objectives are difficult because improving one objective can worsen another.
- MCDM is the umbrella field; MADM and MODM are its two broad families in this classification.
- MADM evaluates a finite set of predefined alternatives using multiple attributes.
- MODM generates solutions by optimizing several objective functions over a feasible region.
- AHP, TOPSIS, and ANP are MADM methods mentioned in the class notes.
- MOLP is linear multi-objective optimization; MONLP includes nonlinear relationships.
- Crisp membership belongs to $\{0,1\}$; fuzzy membership belongs to $[0,1]$.
- Fuzziness describes vagueness, while probability describes uncertainty about event occurrence.

## References

- [IBM CPLEX: Stating a mixed-integer programming problem](https://www.ibm.com/docs/en/icos/22.1.2?topic=mip-stating-problem)
- [Stanford Encyclopedia of Philosophy: Fuzzy Logic](https://plato.stanford.edu/archives/fall2020/entries/logic-fuzzy/)
- [L. A. Zadeh, “Fuzzy Sets,” 1965](https://doi.org/10.1016/S0019-9958(65)90241-X)
