# MeTTa Symbolic Knowledge Graph & Inference Engine

A clean, functional prototype demonstrating symbolic data representation and pattern-matching using the **OpenCog Hyperon MeTTa** framework.

## 🧠 Core Architecture
* **Atomspace Data:** Stores facts and relational predicates uniformly as symbolic Atoms.
* **Pattern Matching:** Employs the native `match` engine for non-deterministic graph traversal.
* **Variable Substitutions:** Uses explicit symbols (`$x`, `$y`) to resolve multi-variable constraints.

---

## 🛠️ Logic Rules Implemented

### 1. Transitive Ancestry
Recursively traverses parental nodes across multiple generations:
```metta
(= (Ancestor $x $y)
   (match &self (Parent $x $y) True))
   
(= (Ancestor $x $y)
   (match &self (Parent $x $z) (Ancestor $z $y)))
```

### 2. Sibling Resolution
Locates intersections where distinct entities share an identical parental node:
```metta
(= (Sibling $x $y)
   (match &self (and (Parent $parent $x) (Parent $parent $y)) $y))
```

---

## 💻 Execution Verification
The script executes inside a Python runtime utilizing the native `hyperon` interpreter bindings.

### Console Output:
```text
Query 1: Who is the sibling of Joseph?
Result: [[Benjamin]]

Query 2: List all direct children of Jacob:
Result: [[Joseph], [Benjamin]]
```

---

## 🎯 Key Takeaways
* **Uniformity:** Code and data share an identical S-expression structural format.
* **Decoupling:** Offloads complex reasoning logic completely to the symbolic layer.
