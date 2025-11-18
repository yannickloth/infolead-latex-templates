# Getting Started with Shared LaTeX Preamble

## What Just Happened?

Your dissertation preamble has been extracted into a **shared, reusable structure** at `~/latex-shared/preamble/`. This enables:

- **DRY**: Write once, use everywhere
- **Consistency**: All documents styled identically
- **Flexibility**: Per-document feature selection

## Current Status

### ✅ Completed

1. **Shared preamble created** at `~/latex-shared/preamble/`
2. **Dissertation updated** to use shared preamble (at [dissertation.tex](../../../code/PIV/Dissertation/dissertation.tex:14))
3. **Theorems split** into:
   - `theorems-standard.tex` (generic math: theorem, lemma, corollary, etc.)
   - `theorems-piv.tex` (your custom: principle, directive, instantiation, etc.)
4. **Templates created**:
   - `template-dissertation.tex` (for future dissertations)
   - `template-article.tex` (for papers/articles)
   - `template-book.tex` (for books)

### 📁 Directory Structure

```
~/latex-shared/preamble/
├── README.md                      (comprehensive documentation)
├── GETTING_STARTED.md            (this file)
├── template-dissertation.tex      (dissertation starter)
├── template-article.tex           (article starter)
├── template-book.tex              (book starter)
│
├── koma-config.tex               (KOMA-Script settings)
├── typography.tex                (fonts, unicode)
├── packages.tex                  (core packages)
├── math.tex                      (math operators)
├── theorems-standard.tex         (generic theorems)
├── theorems-piv.tex              (PIV-specific theorems)
│
├── bibliography.tex              (citations)
├── tables.tex                    (table formatting)
├── diagrams.tex                  (TikZ diagrams)
├── algorithms.tex                (algorithm pseudocode)
├── listings.tex                  (code listings)
│
├── spacing.tex                   (spacing adjustments)
├── koma-headers.tex              (page headers/footers)
└── hyperref.tex                  (hyperlinks)
```

## Quick Start: Your Next Document

### Create a New Article

```bash
# 1. Create document directory
mkdir -p ~/documents/my-paper-2025
cd ~/documents/my-paper-2025

# 2. Copy the article template
cp ~/latex-shared/preamble/template-article.tex article.tex

# 3. Edit the template
# - Update title, author, abstract
# - Adjust \sharedpreamble path if needed
# - Add your content

# 4. Compile
pdflatex article.tex
```

### Create a New Dissertation

```bash
mkdir -p ~/documents/my-dissertation
cd ~/documents/my-dissertation
cp ~/latex-shared/preamble/template-dissertation.tex dissertation.tex
# Edit and customize...
```

## Your Current Dissertation

Your dissertation at `~/code/PIV/Dissertation/` now uses the shared preamble. The next time you compile, it will work exactly as before - but now you can:

### Test the Setup

```bash
cd ~/code/PIV/Dissertation
pdflatex dissertation.tex
```

If you see errors about file paths, adjust the relative path in [dissertation.tex:14](../../../code/PIV/Dissertation/dissertation.tex:14):

```latex
\newcommand{\sharedpreamble}{../../../latex-shared/preamble}
```

## Customizing the Preamble

### Example: Change Fonts Globally

Edit `~/latex-shared/preamble/typography.tex`:

```latex
% Replace kpfonts with your preferred font
\usepackage{lmodern}  % Latin Modern
% or
\usepackage{libertine}  % Linux Libertine
```

All documents will use the new font on next compilation!

### Example: Adjust Spacing

Edit `~/latex-shared/preamble/spacing.tex` to make spacing less dense:

```latex
\thm@preskip=1.0\baselineskip  % Increase from 0.5
\thm@postskip=1.0\baselineskip
```

### Example: Disable Features Per-Document

In your document's preamble, comment out features you don't need:

```latex
% \input{\sharedpreamble/diagrams.tex}      % No diagrams = faster compile
% \input{\sharedpreamble/algorithms.tex}    % No algorithms needed
```

## Maintaining the Preamble

### Optional: Version Control

Consider tracking the preamble with git:

```bash
cd ~/latex-shared
git init
git add preamble/
git commit -m "Initial shared LaTeX preamble"
```

### When to Update vs. Override

**Update the shared preamble when:**
- You want the change in ALL documents
- It's a bug fix or improvement
- It's a new feature useful across documents

**Override in individual documents when:**
- The change is document-specific
- Testing experimental settings
- Conference requires specific formatting

## Troubleshooting

### "File not found" errors

The `\sharedpreamble` path is relative. Count the directory levels:

```
~/code/PIV/Dissertation/dissertation.tex
~/latex-shared/preamble/

From Dissertation/ to latex-shared/:
../ (to code/)
../ (to home/)
../ (to nicky/)
../latex-shared/preamble

Path: ../../../latex-shared/preamble
```

### Module dependency errors

If you get "package X required" errors, ensure you're loading modules in order (see README.md).

### Old theorems.tex conflict

The old `theorems.tex` still exists in `~/latex-shared/preamble/` and your local `Dissertation/Preamble/`. You can safely delete both:

```bash
rm ~/latex-shared/preamble/theorems.tex
rm ~/code/PIV/Dissertation/Preamble/theorems.tex
```

Your dissertation now uses `theorems-standard.tex` and `theorems-piv.tex`.

## Next Steps

1. **Test your dissertation** compiles correctly
2. **Read** [README.md](README.md) for comprehensive documentation
3. **Customize** the preamble to your preferences
4. **Create** your next paper using `template-article.tex`
5. **Optional**: Set up version control for the preamble

## Benefits You Now Have

✅ **DRY**: One source of truth for all styling
✅ **Consistency**: All documents look professional and uniform
✅ **Maintainability**: Easy to update and fix issues
✅ **Flexibility**: Per-document feature selection
✅ **PIV**: Each concern varies independently
✅ **Templates**: Quick start for new documents
✅ **Documentation**: Comprehensive guides for all modules

---

**Questions?** Read the comprehensive [README.md](README.md) for detailed module documentation, customization examples, and troubleshooting tips.

**Ready to write!** 🚀
