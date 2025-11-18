# Shared LaTeX Preamble

A modular, PIV-based (Principle of Independent Variation) LaTeX preamble for consistent document styling across dissertations, articles, and books.

## Philosophy

This preamble follows the **Principle of Independent Variation (PIV)**: each concern varies in exactly one place. Every feature (tables, diagrams, algorithms, listings) is self-contained with its own package imports and configuration.

## Quick Start

### For a New Dissertation

```bash
# Copy the template
cp ~/latex-shared/preamble/template-dissertation.tex ~/documents/my-dissertation/dissertation.tex

# Adjust the relative path if needed
# In dissertation.tex, update: \newcommand{\sharedpreamble}{../../../latex-shared/preamble}
```

### For a New Article

```bash
cp ~/latex-shared/preamble/template-article.tex ~/documents/my-article/article.tex
```

### For a New Book

```bash
cp ~/latex-shared/preamble/template-book.tex ~/documents/my-book/book.tex
```

## Preamble Modules

### Core Modules (Always Loaded)

#### `koma-config.tex`
KOMA-Script document class configuration.
- **Requires**: KOMA-Script document class (scrreprt, scrbook, or scrartcl)
- **Provides**: TOC settings, section numbering, page layout
- **Dependencies**: None

#### `packages.tex`
Essential packages shared across multiple features.
- **Requires**: None
- **Provides**: graphicx, xcolor, amsmath/amssymb/amsthm, mathtools, babel, csquotes
- **Dependencies**: None
- **Load order**: Must load early (before feature modules)

#### `typography.tex`
Font configuration and unicode character definitions.
- **Requires**: inputenc, newunicodechar (from packages.tex)
- **Provides**: Kepler fonts (kpfonts), unicode character mappings, textcomp
- **Dependencies**: packages.tex
- **Customization**: Change `\usepackage{kpfonts}` to use different fonts

#### `math.tex`
Mathematical operators and configuration.
- **Requires**: amsmath (from packages.tex)
- **Provides**: argmax, argmin operators, array spacing
- **Dependencies**: packages.tex

#### `hyperref.tex`
Hyperlinks and cross-references.
- **Requires**: None
- **Provides**: hyperref package with customizable settings
- **Dependencies**: None
- **Load order**: MUST load last among all packages

### Theorem Environments

#### `theorems-standard.tex`
Generic mathematical theorem environments.
- **Requires**: amsthm (from packages.tex)
- **Provides**: theorem, lemma, corollary, proposition, hypothesis, definition, example, remark
- **Dependencies**: packages.tex
- **Usage**: Load in all mathematical documents

#### `theorems-piv.tex`
PIV-specific custom theorem environments.
- **Requires**: amsthm (from packages.tex)
- **Provides**: principle, directive, axiom, problem, pattern, design-decision, fallacy, observation, instantiation, construction, speculation
- **Dependencies**: packages.tex
- **Usage**: Optional - only load for software design/PIV documents

### Feature Modules (Optional - Enable As Needed)

#### `bibliography.tex`
Citation and bibliography support.
- **Requires**: None
- **Provides**: cite package
- **Dependencies**: None
- **Usage**: Enable for any document with citations

#### `tables.tex`
Professional table formatting.
- **Requires**: None
- **Provides**: booktabs (better rules), longtable (multi-page tables)
- **Dependencies**: None
- **Usage**: Enable if document contains tables

#### `diagrams.tex`
TikZ diagrams and commutative diagrams.
- **Requires**: xcolor (from packages.tex)
- **Provides**: tikz with positioning/shapes/arrows libraries, tikz-cd
- **Dependencies**: packages.tex (xcolor)
- **Usage**: Enable for documents with diagrams or category theory
- **Performance**: TikZ increases compile time; disable if not needed

#### `algorithms.tex`
Algorithm pseudocode typesetting.
- **Requires**: None
- **Provides**: algorithm (floating environment), algpseudocode (syntax)
- **Dependencies**: None
- **Usage**: Enable for documents with algorithms

#### `listings.tex`
Code listing and syntax highlighting.
- **Requires**: xcolor (from packages.tex)
- **Provides**: listings package, JSON language definition
- **Dependencies**: packages.tex (xcolor)
- **Configuration**: Customizable syntax highlighting colors
- **Usage**: Enable for documents with code examples

#### `spacing.tex`
Fine-tuned spacing adjustments.
- **Requires**: amsthm (from packages.tex)
- **Provides**: enumitem package, theorem spacing, list spacing, equation spacing
- **Dependencies**: packages.tex (amsthm)
- **Customization**: Adjust spacing values for different document densities
- **Note**: Optimized for dense academic writing; may want to relax for articles

#### `koma-headers.tex`
Page headers and footers.
- **Requires**: KOMA-Script document class
- **Provides**: scrlayer-scrpage package, centered chapter/section headers
- **Dependencies**: KOMA-Script
- **Customization**: Uncomment footer and headsepline options as needed
- **Note**: May want to disable for articles

## Load Order

**Critical**: Load order matters for LaTeX packages. Follow this sequence:

1. `koma-config.tex` (KOMA settings first)
2. `typography.tex` (fonts before math)
3. `packages.tex` (core packages)
4. `math.tex`
5. `theorems-*.tex`
6. Feature modules (bibliography, tables, diagrams, algorithms, listings)
7. `spacing.tex`
8. `koma-headers.tex`
9. `hyperref.tex` (MUST BE LAST)

## Customization

### Enabling/Disabling Features

Comment out features you don't need:

```latex
% \input{\sharedpreamble/diagrams.tex}      % Disabled - no diagrams in this doc
\input{\sharedpreamble/listings.tex}        % Enabled - contains code examples
```

### Per-Document Overrides

After loading the shared preamble, add document-specific customizations:

```latex
\input{\sharedpreamble/hyperref.tex}

% Document-specific customizations
\newenvironment{keywords}{...}
\setlength{\parskip}{1em}  % Override default spacing
```

### Changing Fonts

Edit `typography.tex` and replace:
```latex
\usepackage[oldstylenums,fullsumlimits,fullintlimits,nofligatures]{kpfonts}
```

With your preferred font package (e.g., `\usepackage{lmodern}`, `\usepackage{palatino}`).

### Adjusting Spacing

Edit `spacing.tex` to modify:
- Theorem spacing: `\thm@preskip` and `\thm@postskip`
- List spacing: `topsep`, `itemsep`, `parsep`
- Equation spacing: `\abovedisplayskip`, `\belowdisplayskip`

### Adding Custom Theorem Environments

Create a new file `theorems-custom.tex`:

```latex
\theoremstyle{definition}
\newtheorem{mytheorem}{My Theorem}[section]
```

Load it after standard theorems:
```latex
\input{\sharedpreamble/theorems-standard.tex}
\input{\sharedpreamble/theorems-custom.tex}
```

## Templates

### `template-dissertation.tex`
For dissertations and theses (scrreprt).
- Single-sided layout
- All features enabled by default
- Includes TOC, maketitle structure

### `template-article.tex`
For conference/journal articles (scrartcl).
- Shorter document structure
- Abstract and keywords environment
- Headers disabled by default
- Basic sectioning (\section, \subsection)

### `template-book.tex`
For books and monographs (scrbook).
- Two-sided layout
- Front matter, main matter, back matter structure
- Chapter-based organization
- Optional dedication, preface, index

## Dependency Graph

```
packages.tex
├── typography.tex (requires inputenc, newunicodechar)
├── math.tex (requires amsmath)
├── theorems-*.tex (requires amsthm)
├── diagrams.tex (requires xcolor)
├── listings.tex (requires xcolor)
└── spacing.tex (requires amsthm)

koma-config.tex (requires KOMA-Script class)
koma-headers.tex (requires KOMA-Script class)

hyperref.tex (no dependencies, MUST load last)
```

## Updating the Preamble

When you update a preamble file, all documents using it are automatically updated on next compilation. Test changes with:

```bash
cd ~/documents/test-document
pdflatex test.tex
```

## Benefits

### DRY (Don't Repeat Yourself)
- Single source of truth for all styling
- Change once, apply everywhere
- No style drift between documents

### Consistency
- All documents automatically styled identically
- Professional, uniform appearance
- Predictable behavior

### Maintainability
- Easy to find and fix issues
- Clear module responsibilities
- Self-documenting structure

### Flexibility
- Per-document feature selection
- Easy to override settings
- Supports multiple document types

### PIV Compliance
- Each concern varies independently
- Minimal coupling between modules
- Explicit dependencies

## Troubleshooting

### "File not found" errors
Check the `\sharedpreamble` path is correct relative to your document:
```latex
\newcommand{\sharedpreamble}{../../../latex-shared/preamble}
```

### "Package X required" errors
The dependency check system will tell you which package is missing. Ensure you're loading modules in the correct order.

### Compilation is slow
Disable unused features, especially `diagrams.tex` (TikZ) which significantly increases compile time.

### Spacing looks wrong
Article spacing may look too tight. Comment out `\input{\sharedpreamble/spacing.tex}` or adjust values in that file.

## Version Control

Consider tracking the shared preamble in git:

```bash
cd ~/latex-shared
git init
git add preamble/
git commit -m "Initial preamble structure"
```

For individual documents, you can use git submodules to pin specific preamble versions.

## License

Customize this section based on your licensing preferences.

## Contact

Your Name <your.email@example.com>
