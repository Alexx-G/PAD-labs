### Simple LaTeX template for a lab report

#### Installation
- Install LaTeX ([more info](https://www.latex-project.org/get/));
To deal with dependencies you should either:
    - install full distribution of the LaTeX (`texlive-full`);
    - install at least the following packages - `texlive-latex-extra texlive-lang-european`;
    - install the package `texlive-lang-french` for the support of the franch language;
- [Getting started](https://www.latex-project.org/help/documentation/);

#### Build PDF from sources
Just open the folder with your report template and run the following command

`latexmk -pdf Lab_template.tex`

This will genenerate some verbose output and will update/create the `Lab_template.pdf` file.

#### Template structure
You will work mostly only with `.tex` files. Other files contain either some configuration
or just build info.

```
.
├── biblio.tex
├── Chapter_1.tex
├── Conclusions.tex
├── Introduction.tex
├── Lab_template.tex # Entry point for your report. This defines structure of your report
└── Title.tex
```

- **Lab_template.tex** - entry point for your report. This defines structure of your report.
You won't update this, since it will be the same for all your reports.
- **Title.tex** - title page of the report;
- **Introduction.tex** - a brief introduction for this lab (objectives, short description);
- **Chapter_1.tex** - lab content (tasks, implementation, examples, code snippets if necessary);
- **Conclusions.tex** - conclusions;
- **biblio.tex** - references.
