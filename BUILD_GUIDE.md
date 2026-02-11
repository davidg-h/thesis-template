# Build Guide: Generate `thesis.pdf` from this LaTeX Project

This guide is intended for beginners who are working with LaTeX for the first time.  
It explains how to set up a **fresh Windows, Linux, or macOS machine** so you can build this repository into a final `thesis.pdf`.

It focuses on the two easiest workflows:

1. **Command line using `make`** (via the provided `Makefile`)
2. **VS Code + LaTeX Workshop**

---

## 1) What this project needs

This repository is built with:

- `pdflatex`
- `bibtex`
- standard LaTeX packages (installed via `TeX Live` / `MacTeX` / `MiKTeX`)
- optional but recommended: `latexmk`  
  (mainly for the VS Code workflow; usually included in common LaTeX distributions)
- `make` (for the Makefile-based workflow)

The `Makefile` target `run` builds `thesis.pdf` from `thesis.tex` and bibliography file `refs.bib`.

> **Important project-specific note:**  
> The Makefile checks for a declaration PDF named  
> `SB_0050_FO_Pruefungsrechtliche_Erklaerung_und_Erklaerung_zur_Veroeffentlichung_der_Abschlussarbeit_public.pdf`.  
> If this file is missing, `make run` will stop with an error.

---

## 2) OS-specific installation

### Common dependency overview

Install these tools first:

- A TeX distribution:
  - **Windows**: MiKTeX (or TeX Live)
  - **Linux**: TeX Live
  - **macOS**: MacTeX
- `make`
- (Recommended editor) VS Code + LaTeX Workshop extension

---

### Windows

#### Option A: Make with WSL

If you want to use `make` exactly as in Unix-like environments:

1. Install **WSL** (e.g., Ubuntu).
2. In WSL terminal, install:
   - TeX Live (including `pdflatex`, `bibtex`, `latexmk`)
   - `make`
3. Build inside WSL from the repo folder.

#### Option B: Native Windows

1. Install **MiKTeX**.
2. Install **GNU Make** (for example via Chocolatey, Scoop, or MSYS2).
3. Ensure both are in `PATH`:
   - `pdflatex`
   - `bibtex`
   - `make`
4. Enable MiKTeX automatic package installation (recommended).

---

### Linux (Ubuntu/Debian example)

#### Install full LaTeX distribution (recommended)

To avoid missing-package errors, install the full TeX Live distribution:

```bash
sudo apt update
sudo apt install texlive-full make
```

`latexmk` is normally included in `texlive-full`.  
If it is missing for any reason, install it separately:

```bash
sudo apt install latexmk
```

---

### macOS

1. Install **MacTeX** (includes full TeX toolchain).
2. Install `make` (usually already present via Xcode Command Line Tools).
3. Verify `PATH` includes MacTeX binaries.

---

## 3) Build path A: Command line with Makefile

From the repository root, run:

```bash
make run
```

This triggers the required LaTeX and BibTeX passes and should produce `thesis.pdf`.

### Clean generated artifacts

```bash
make clean
```

### Run build and clean in one command

```bash
make rc
```

If `make run` fails due to declaration PDF

Place the required declaration PDF in the repository root with the exact filename expected by the Makefile:

- `SB_0050_FO_Pruefungsrechtliche_Erklaerung_und_Erklaerung_zur_Veroeffentlichung_der_Abschlussarbeit_public.pdf`

Then run:

```bash
make run
```

---

## 4) Build path B: VS Code + LaTeX Workshop

### Install requirements

1. Install **VS Code**.
2. Install extension **LaTeX Workshop**.
3. Ensure a TeX distribution is installed and in `PATH`
   (`pdflatex`, `bibtex`; `latexmk` recommended).

### Build in VS Code

1. Open this repository folder in VS Code.
2. Open `thesis.tex`.
3. Run: **LaTeX Workshop: Build LaTeX project**.

### Recommended recipe

If available, use a `latexmk (pdf)` recipe in LaTeX Workshop. It handles multiple passes automatically.

If `latexmk` is not installed, LaTeX Workshop can still use `pdflatex` + `bibtex` toolchains, but setup may be more manual.
