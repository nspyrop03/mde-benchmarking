Compile the tex file with the xelatex compiler:

```
xelatex --shell-escape report.tex
biber report
xelatex --shell-escape report.tex
xelatex --shell-escape report.tex
```