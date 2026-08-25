# Advanced LaTeX Lab Manual Template

A highly modular, automated, and typographically modern LaTeX template designed for university lab files, practical reports, and programming assignments. 

This template separates content from styling, utilizes dynamic spacing, and automates file inclusion and numbering to keep your source code clean and your workflow fast.

## 🚀 Key Features

*   **Modular Architecture:** The project is cleanly split into individual files for the preamble, title page, table of contents, and tabular index, isolating configurations from actual content.
*   **Automated Numbering:** Chapter headings automatically format as "Assignment X:" or "Program No. X:".
*   **Dynamic File Loading:** Code listings and terminal outputs are dynamically fetched using the `\thechapter` macro (e.g., `program\thechapter.cpp`), meaning chapters can be reordered without ever rewriting file paths.
*   **Advanced Typography:** Powered by the `fontspec` package, utilizing premium fonts like JetBrains Mono for code blocks and TeX Gyre Pagella for prose.
*   **Semantic Title Page:** Uses responsive vertical springs (`\vfill`) and relative units (`em`) to ensure perfect visual balance regardless of page size or margin adjustments.

## 📂 Directory Structure

```text
.
├── docs/                      # LaTeX source files
│   ├── main.tex               # The root document
│   ├── preamble.tex           # Package imports and custom commands
│   ├── titlepage.tex          # Semantic title page content
│   ├── index.tex              # Standard Table of Contents (TOC)
│   └── tabular_index.tex      # Custom longtable for assignment tracking (S.No, Date, Sign)
├── programs/                  # Your raw source code and outputs
│   ├── program1.cpp
│   ├── output1.txt
│   └── ...
└── images/               
    └── logo.png               # University/Institutional logo
```

## 🛠️ Prerequisites & Compilation

Because this template uses `fontspec` for advanced font rendering, **it will fail to compile with standard pdfLaTeX.** You must compile this project using **LuaLaTeX** (recommended) or XeLaTeX.

### Compilation Command
To compile the document cleanly from the command line while generating all necessary auxiliary files, use `latexmk`:

```bash
latexmk -lualatex -file-line-error -synctex=1 -interaction=nonstopmode main.tex
```
*(If you are using Neovim + VimTeX, simply pressing `<localleader>ll` will execute this automatically based on your Lua configuration).*

**Required Fonts:**
*   **TeX Gyre Pagella:** Main body text.
*   **JetBrains Mono:** Code listings and terminal outputs.
*   **Latin Modern Math:** Mathematical equations.

## 📦 Preamble Package Breakdown

This template relies on a carefully curated list of packages to achieve its layout and typography. Here is what every package in `preamble.tex` is doing:

*   **`geometry`**: Configures page dimensions and layout (e.g., forcing A4 paper and exact 2cm margins).
*   **`amsmath`, `amssymb`, `amsfonts`, `amsthm`**: The core suite for advanced mathematical typesetting, symbols, fonts, and theorem environments.
*   **`graphicx`, `float`**: `graphicx` handles image insertion, while `float` provides the `[H]` specifier to force figures strictly where they are declared in the code.
*   **`fontspec`**: Replaces traditional LaTeX font management, allowing the use of system-installed TrueType (TTF) and OpenType (OTF) fonts via LuaLaTeX/XeLaTeX.
*   **`listings`**: The core package for typesetting source code, enabling custom styles, line numbering, and syntax highlighting.
*   **`xcolor`**: Enables advanced color definitions (used heavily to colorize keywords and comments in the `listings` environments).
*   **`fancyhdr`**: Completely customizes page headers and footers (used for course codes, titles, and page numbers).
*   **`setspace`**: Provides commands like `\onehalfspacing` and `\doublespacing` to elegantly manage line height.
*   **`unicode-math`**: Configures math environments to use proper OpenType math fonts rather than legacy LaTeX math fonts.
*   **`microtype`**: Silently improves document typography by managing micro-adjustments like character protrusion and font expansion, reducing awkward hyphenation and spacing.
*   **`fancyvrb`**: Provides enhanced verbatim environments for raw text output.
*   **`tikz`**: A highly powerful graphical engine for drawing vector shapes, graphs, and diagrams programmatically within LaTeX.
*   **`enumitem`**: Allows extensive customization of list environments (bullet types, indentation, spacing for `itemize` and `enumerate`).
*   **`tocloft`**: Provides granular control over the typography and spacing of the Table of Contents, List of Figures, and List of Tables.
*   **`hyperref`**: Generates clickable hyperlinks for internal cross-references, TOC entries, and URLs, while embedding metadata into the final PDF.
*   **`titlesec`**: Hijacks default heading formats, allowing completely custom layouts for the `\chapter` (e.g., formatting it as "Program No. X") and `\section` commands.
*   **`longtable`, `array`**: Used in `tabular_index.tex`. `longtable` allows the assignment index to seamlessly break across multiple pages, while `array` allows advanced column formatting (like vertically centering paragraph text).

## 💻 Usage Instructions

To add a new practical or assignment, simply declare a new `\chapter{}`. The section numbering and external file inclusions will automatically sync with the chapter number.

```latex
\chapter{Implement classes and objects demonstrating member functions...}

\section{Theoretical Background}
Write your theory here. The section will automatically number itself (e.g., 1.1, 1.2).

\section{Code Implementation}
% Automatically loads program1.cpp for Chapter 1, program2.cpp for Chapter 2, etc.
\lstinputlisting{../programs/program\thechapter.cpp}

\section{Program Output}
\lstinputlisting[style=output]{../programs/output\thechapter.txt}
```
