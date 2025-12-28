# Science Olympiad LaTeX Template

A professional LaTeX template system for creating Science Olympiad exams, specifically designed for astronomy, astrophysics, and astronautics competitions. This template was created for the Colombian Astronomy, Astrophysics and Astronautics Olympiad (OCAAA - Olimpiada Colombiana de Astronomía, Astrofísica y Astronáutica).

## Overview

This repository provides a complete LaTeX framework for creating multi-round Science Olympiad examinations with professional formatting, including:

- Multiple competition rounds (First Round, Second Round, Final Round)
- Customizable cover pages with logos and author information
- Student information forms with grading tables
- Multiple question types (multiple choice and open-ended questions)
- Answer key generation (show/hide solutions)
- Professional headers and footers with organizational branding
- Pre-configured astronomy/astrophysics notation and units

## Repository Structure

```
sci-olys/
├── First Round/              # First round exam (Clasificatoria)
│   ├── Clasificatoria.tex    # Main LaTeX file
│   ├── Config/
│   │   └── preamble.tex      # Package imports and formatting
│   ├── Pages/
│   │   ├── cover.tex         # Cover page
│   │   ├── form.tex          # Student information form
│   │   ├── Problems/         # Actual exam problems
│   │   └── Templates/        # Question templates
│   └── Photos/               # Logos and images
├── Second Round/             # Second round exam (Selectiva)
│   ├── Selectiva.tex         # Main LaTeX file
│   └── [similar structure]
├── Final Round/              # Final round exam
│   ├── Final Round.tex       # Main LaTeX file
│   └── [similar structure]
├── Example PDFs/             # Sample compiled PDFs
└── LICENSE.md                # CC BY-NC-SA 4.0 License
```

## Getting Started

### Prerequisites

You need a LaTeX distribution installed on your system:

- **Windows**: [MiKTeX](https://miktex.org/) or [TeX Live](https://www.tug.org/texlive/)
- **macOS**: [MacTeX](https://www.tug.org/mactex/)
- **Linux**: TeX Live (usually available via package manager)
  ```bash
  # Ubuntu/Debian
  sudo apt-get install texlive-full
  
  # Fedora
  sudo dnf install texlive-scheme-full
  ```

### Quick Start

1. **Clone the repository**:
   ```bash
   git clone https://github.com/jj-sm/sci-olys.git
   cd sci-olys
   ```

2. **Choose a round** (First Round, Second Round, or Final Round)

3. **Compile the main LaTeX file**:
   ```bash
   cd "First Round"
   pdflatex Clasificatoria.tex
   ```
   
   Run the command twice to ensure all references are resolved correctly.

4. **View the generated PDF**: The output will be `Clasificatoria.pdf` (or corresponding file for other rounds)

## Usage Guide

### Creating a New Exam

1. **Select or duplicate a round folder** (e.g., copy `First Round/` to create a new exam)

2. **Edit the main `.tex` file** (e.g., `Clasificatoria.tex`):
   - Toggle answer key visibility by commenting/uncommenting `\printanswers`
   - Include your problem files in the PROBLEMS section

3. **Customize the cover page** (`Pages/cover.tex`):
   - Update exam title
   - Modify author names
   - Change year and olympiad edition

4. **Customize the student form** (`Pages/form.tex`):
   - Adjust exam duration
   - Modify instructions
   - Update grading table structure

5. **Add problems** to `Pages/Problems/`:
   - Create new `.tex` files for each problem
   - Reference them in the main file using `\input{Pages/Problems/your_problem.tex}`

### Template Types

The repository includes several question templates in `Pages/Templates/`:

#### 1. Multiple Choice Questions (`Selección Múltiple.tex`)

Standard multiple choice with one correct answer:

```latex
\section{Section Title (10 puntos)}

Question text here?

\begin{choices}
    \choice Option A
    \correctchoice Option B (correct answer)
    \choice Option C
    \choice Option D
    \choice Option E
\end{choices}

\marginnote{\textbf{(10pt)}}
```

#### 2. Multiple Choice Variants

- **`Selección Múltiple 2.tex`**: Alternate layout with justified text
- **`Selección Múltiple 3.tex`**: Compact format with `oneparchoices`

#### 3. Open-Ended Questions (`Pregunta Abierta.tex`)

For problems requiring calculations or written explanations:

```latex
\section{Problem Title (10 points)}

Problem description and context.

\begin{enumerate}[label=(\alph*)]
    \item Question part A \marginnote{\textbf{(6pt)}}
    \item Question part B \marginnote{\textbf{(4pt)}}
\end{enumerate}

\begin{solutionbox}{3cm}
    Solution text (shown when \printanswers is enabled)
\end{solutionbox}
```

### Answer Key Generation

To create an answer key:

1. Open the main `.tex` file (e.g., `Clasificatoria.tex`)
2. Uncomment the line: `\printanswers`
3. Compile the document

To create the student version:

1. Comment out: `% \printanswers`
2. Compile the document

This will show/hide solutions and highlight correct answers in blue.

## Compilation Instructions

### Basic Compilation

```bash
cd "First Round"
pdflatex Clasificatoria.tex
pdflatex Clasificatoria.tex  # Run twice for references
```

### Using a Makefile (Optional)

You can create a simple Makefile for convenience:

```makefile
.PHONY: all clean

all:
	pdflatex Clasificatoria.tex
	pdflatex Clasificatoria.tex

clean:
	rm -f *.aux *.log *.out *.toc
```

### Using LaTeX Editors

Popular LaTeX editors with built-in compilation:
- **Overleaf** (online, collaborative)
- **TeXstudio** (cross-platform)
- **TeXShop** (macOS)
- **TeXworks** (cross-platform)

Simply open the main `.tex` file and click the compile/build button.

## Customization Guide

### Logos and Branding

Replace the logo files in the `Photos/` directory:
- `Logo OCAAA-8.jpeg`: Main organization logo (appears on left)
- `logoUAN.png`: Institution logo (appears on right)

### Headers and Footers

Edit `Config/preamble.tex` to customize:

```latex
% Header configuration
\fancyhead[L]{\includegraphics[height=1.6cm]{Photos/Logo OCAAA-8.jpeg}}
\fancyhead[R]{\includegraphics[height=1cm]{Photos/logoUAN.png}}
\fancyhead[C]{...exam code...}

% Footer configuration
\fancyfoot[C]{\copyright\ \the\year \ - Your Organization | \LaTeX}
```

### Exam Code Format

Update the exam code in the header (e.g., `PT-CLA-202400`):
- Located in `Config/preamble.tex` in the `\fancyhead[C]` section
- Format: `PT-[ROUND]-YEAR##`

### Astronomy Notation

The template includes pre-defined commands for common astronomy symbols:

```latex
\msun    % Solar mass (M☉)
\rsun    % Solar radius (R☉)
\lsun    % Solar luminosity (L☉)
\mearth  % Earth mass (M⊕)
\rearth  % Earth radius (R⊕)
\au      % Astronomical unit
\parsec  % Parsec
```

Add custom commands in `Config/preamble.tex`.

### Language Support

The template supports both Spanish and English. To change language:
1. Modify section titles in your problem files
2. Update instructions in `Pages/form.tex`
3. Change cover page text in `Pages/cover.tex`

## Example Problems

The repository includes example problems from professional olympiads:
- **Co-orbital satellites**: Multi-part physics problem with derivations
- **Relativistic Beaming**: Advanced astrophysics problem
- Multiple choice examples in Spanish

See `Pages/Problems/` for complete examples in each round.

### Pre-compiled Examples

The `Example PDFs/` directory contains pre-compiled PDFs for all three rounds:
- `First Round.pdf` - Clasificatoria (Qualifying round)
- `Second Round.pdf` - Selectiva (Selection round)
- `Final Round.pdf` - Final round

These demonstrate the expected output and formatting of the template.

## License

This template is licensed under the [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](LICENSE.md).

You are free to:
- **Share**: Copy and redistribute the material
- **Adapt**: Remix, transform, and build upon the material

Under the following terms:
- **Attribution**: Give appropriate credit
- **NonCommercial**: Not for commercial use
- **ShareAlike**: Distribute adaptations under the same license

## Acknowledgments

- Example problems were used from **IOAA 2022 - Georgia** (International Olympiad on Astronomy and Astrophysics)
- Template developed for the **Olimpiada Colombiana de Astronomía, Astrofísica y Astronáutica (OCAAA)**
- Hosted by **Universidad Antonio Nariño** - Oficina de Olimpiadas Colombianas (OC)

## Contributing

Contributions are welcome! If you have improvements or find issues:
1. Fork the repository
2. Create a feature branch
3. Submit a pull request

## Troubleshooting

### Special Characters in Filenames

Some LaTeX distributions may have issues with files containing special characters (e.g., accented letters like "Selección"). If you encounter compilation errors when using template files with such names:

1. **Solution 1**: Rename the template files to use only ASCII characters
2. **Solution 2**: Use actual problem files (which use underscores instead of spaces)
3. **Solution 3**: Ensure your LaTeX distribution supports UTF-8 filenames

The repository includes example problem files with ASCII-safe filenames that compile reliably across all LaTeX distributions.

### Missing Packages

If you get "Package not found" errors:
- **MiKTeX**: Packages are usually auto-installed
- **TeX Live**: Install missing packages using `tlmgr install <package-name>`
- **Full Installation**: Install `texlive-full` (Linux) or complete distributions to avoid missing packages

### PDF Version Warnings

You may see warnings about PDF version compatibility. These are typically harmless, but you can:
- Update your images to PDF 1.5 or lower
- Or ignore the warnings if the output is acceptable

## Support

For questions or issues:
- Open an issue on GitHub
- Contact the OCAAA organizers

## Additional Resources

- [LaTeX Documentation](https://www.latex-project.org/help/documentation/)
- [Exam Document Class](https://www.ctan.org/pkg/exam)
- [IOAA Official Website](http://www.ioaa.info/)
- [OCAAA Website](http://ocaaa.co/) (if available)

---

**Made with ❤️ and LaTeX for Science Olympiad organizers worldwide**