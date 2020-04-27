# Sphinx Autosar diagnostics documentation


The [`sphinx`](http://www.sphinx-doc.org/) python tool creates 
html or latex documentation sources from the 
*reStructuredText* or *Markdown* sources.

In order to create documentation:

1. install `python 3+`

2. install sphinx  with `pip install sphinx`

3. install sphinx_rtd_theme with `pip install sphinx_rtd_theme`

Build the HTML documentation:

```sh
sphinx-build -b html source build/html
```

Build the LaTeX documentation:

```sh
sphinx-build -b latex source build/latex
```
