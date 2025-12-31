# Theorem Environments Migration Guide

This document describes the consolidation of theorem-like environments from three separate files into a single unified `theorems.tex` file.

## Summary of Changes

The following files have been consolidated:

| Old File | Status | Contents |
|----------|--------|----------|
| `theorems-standard.tex` | **Deprecated** | Standard math theorems (theorem, lemma, corollary, etc.) |
| `theorems-ivp.tex` | **Deprecated** | IVP-specific environments (axiom, principle, pattern, etc.) |
| `theorems-scientific.tex` | **Deprecated** | Scientific claims with tcolorbox styling (achievement, prediction, etc.) |
| **`theorems.tex`** | **New unified file** | All environments combined |

## Migration Steps

### Step 1: Update Package Loading Order

**Before:**
```latex
% Theorem-like environments
\input{\preamble/theorems-standard.tex}
\input{\preamble/theorems-ivp.tex}

% ... other packages ...

\usepackage[most]{tcolorbox}
\input{\preamble/theorems-scientific.tex}
```

**After:**
```latex
% Colored boxes (required by unified theorems module)
\usepackage[most]{tcolorbox}

% Unified theorem-like environments
\input{\preamble/theorems.tex}
```

### Step 2: Remove Deprecated Inputs

Remove any `\input` statements for:
- `theorems-standard.tex`
- `theorems-ivp.tex`
- `theorems-scientific.tex`

These files will be removed in a future update.

## New Features in Unified File

### Enhanced Visual Styling (B&W Print Friendly)

The scientific claim environments now have distinctive visual styles that work well in both color and black-and-white printing:

| Environment | Visual Style | Purpose |
|-------------|-------------|---------|
| `achievement` | Double border | Novel breakthroughs |
| `prediction` | Dashed border | Testable predictions |
| `warning` | Left bar | Caveats and limitations |
| `open_question` | Dotted border | Unresolved problems |
| `requirement` | Corner brackets | Necessary conditions |
| `postdiction` | Solid border | Matches known data |
| `consistency_check` | Simple box | Reproduces known physics |

### New Environments

The following new environments are now available:

- **`postdiction`**: For derived results that match already-known experimental data (epistemic honesty about what is a genuine prediction vs. a fit to existing data)
- **`consistency_check`**: For verification that the theory reproduces known physics
- **`derivation`**: For step-by-step mathematical derivations that aren't formal theorems
- **Starred variants**: `achievement*`, `prediction*`, `open_question*`, `warning*` for unnumbered versions

### Shared Counter

All scientific claim environments (`achievement`, `prediction`, `warning`, `open_question`, `requirement`, `postdiction`, `consistency_check`) now share a single counter `scientificclaim`, numbered within chapters as `X.Y`.

## Complete Environment Reference

### Part 1: Standard Mathematical Environments

| Environment | Style | Counter |
|-------------|-------|---------|
| `theorem` | plain (italic) | chapter-based |
| `lemma` | plain | shares with theorem |
| `corollary` | plain | shares with theorem |
| `proposition` | plain | shares with theorem |
| `hypothesis` | plain | shares with theorem |
| `definition` | definition (upright) | chapter-based |
| `example` | definition | chapter-based |
| `remark` | remark | unnumbered |

### Part 2: IVP and Design Theory Environments

| Environment | Style | Counter |
|-------------|-------|---------|
| `axiom` | definition | global |
| `principle` | definition | global |
| `directive` | definition | global |
| `problem` | definition | global |
| `pattern` | definition | global |
| `design-decision` | definition | global |
| `fallacy` | definition | global |
| `observation` | definition | global |
| `instantiation` | definition | global |
| `construction` | definition | global |
| `speculation` | definition | global |
| `assumption` | definition | global |
| `conclusion` | remark | global |

### Part 3: Scientific Claim Environments (tcolorbox)

| Environment | Visual Style | Counter |
|-------------|-------------|---------|
| `achievement` | Double border, gray bg | scientificclaim |
| `prediction` | Dashed border | scientificclaim |
| `warning` | Left bar | scientificclaim |
| `open_question` | Dotted border | scientificclaim |
| `requirement` | Corner brackets | scientificclaim |
| `postdiction` | Solid border | scientificclaim |
| `consistency_check` | Simple box | scientificclaim |
| `derivation` | Minimal | scientificclaim |

## Usage Examples

### Achievement (Novel Result)
```latex
\begin{achievement}[Vacuum Spacetime Structure]
\label{ach:vacuum-fcc}
We derive the microscopic geometric structure of empty spacetime...
\end{achievement}
```

### Prediction (Testable Claim)
```latex
\begin{prediction}[Gravitational Decoherence]
Universal gravitational decoherence rate $\Gamma = Gm^2/(\hbar\Delta x)$...
\end{prediction}
```

### Open Question (Unresolved Problem)
```latex
\begin{open_question}[The Initial State Problem]
\label{oq:initial-state}
What determines $\Gamma_0$, the initial graph configuration?
\end{open_question}
```

### Requirement (Necessary Condition)
```latex
\begin{requirement}[Convergence Conditions]
For the emergent metric to be well-defined, the graph must satisfy...
\end{requirement}
```

### Warning (Limitation)
```latex
\begin{warning}[Current Experimental Status]
Zero experimental confirmations exist. All agreements are postdictions.
\end{warning}
```

## Dependencies

The unified `theorems.tex` requires:
- `amsthm` package (must be loaded before)
- `tcolorbox` package with `most` option (auto-loaded if missing)
- `xcolor` package (usually included via tcolorbox)

## Backward Compatibility

The unified file defines all environments from the deprecated files, so existing documents should compile without changes after updating the `\input` statements.

## Questions?

If you encounter issues during migration, check:
1. Is `tcolorbox` loaded with the `most` option before `theorems.tex`?
2. Are there any duplicate environment definitions in your document?
3. Is `amsthm` loaded (via `packages.tex` or directly)?
