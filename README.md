# Django-Tex Syntax Highlighting Extension

[![Version](https://img.shields.io/visual-studio-marketplace/v/bfrangi.vscode-django-tex?color=green&include_prereleases&label=Version)](https://marketplace.visualstudio.com/items?itemName=bfrangi.vscode-django-tex)
[![Open VSX](https://img.shields.io/badge/Open%20VSX-vscode--django--tex-purple)](https://open-vsx.org/extension/bfrangi/vscode-django-tex)
[![Open VSX Downloads](https://img.shields.io/open-vsx/dt/bfrangi/vscode-django-tex?color=purple&label=Downloads)](https://open-vsx.org/extension/bfrangi/vscode-django-tex)
[![VS Marketplace](https://img.shields.io/badge/Visual%20Studio%20Marketplace-vscode--django--tex-lightgray)](https://marketplace.visualstudio.com/items?itemName=bfrangi.vscode-django-tex)
[![VS Marketplace Downloads](https://img.shields.io/visual-studio-marketplace/d/bfrangi.vscode-django-tex?color=lightgray&label=Downloads)](https://marketplace.visualstudio.com/items?itemName=bfrangi.vscode-django-tex)
[![GitHub](https://img.shields.io/badge/GitHub-vscode--django--tex-blue)](https://github.com/bfrangi/vscode-django-tex)
[![GitHub Downloads](https://img.shields.io/github/downloads/bfrangi/vscode-django-tex/total?color=blue&label=Downloads)](https://github.com/bfrangi/vscode-django-tex)







The **Django-Tex Syntax Highlighting** extension (`vscode-django-tex`) is a simple *VSCode* extension for syntax highlighting in [`django-tex`](https://github.com/weinbusch/django-tex) (`.tex`) templates. The extension is based on another extension called [Django](https://github.com/vscode-django/vscode-django), which does the same for `.txt` and `.html` templates, so credits to [@batisteo](https://github.com/batisteo) for that.

-------------------------------------------------------------------

## Installation 

You can install this extension directly from the Extension Marketplace in VSCode. You can also launch *VS Code Quick Open* (`Ctrl+P`), paste the following command, and press enter:

```
ext install bfrangi.vscode-django-tex
```

-------------------------------------------------------------------

## Features

* Syntax Highlighting in [`django-tex`](https://github.com/weinbusch/django-tex) (`.tex`) templates:

    <p align="center">
    <img src="https://github.com/bfrangi/vscode-django-tex/raw/main/media/example-template.gif" />
    </p>

    <details>
    <summary>
    <b>Rest of the example code</b>
    </summary>

    Template code:

    ```
    \documentclass{article}

    \begin{document}

        \begin{center}

            \section*{Table for {{date|date}} }

            \begin{tabular}{ 
                {% for _ in table.body.rows.0 %}|c{% endfor %}| 
                } 

                {# This is a comment #}
                \hline
                % This is another comment
            
                \multicolumn{
                    {{table.headers.first.span}}
                    }{|c|}{ {{table.headers.first.value}} } & 
                \multicolumn{ 
                    {{table.headers.second.span}} 
                    }{c|}{ {{table.headers.second.value}} } \\ 
                
                \hline

                \iffalse 
                This is a comment spanning several lines
                \hline \fi
                
                {% for row in table.body.rows %}
                {% for cell in row %}{% if not cell == row.0 %} &
                {% endif %} cell{{cell}} {% endfor %} \\
                {% endfor %}

                {% comment %}
                This is another comment spanning several lines
                \hline {% endcomment %}

                \hline
            
            \end{tabular}

        \end{center}

    \end{document}
    ```

    We could combine the code from the `django-tex` template with the following function based view to render the *LaTeX* document:

    ```python
    from django_tex.shortcuts import render_to_pdf
    from datetime import date

    def render_pdf(request):
            table = {
                'headers': { 
                    'first': {
                        'span': 3,
                        'value': 'First Multicol',
                    },
                    'second': {
                        'span': 3,
                        'value': 'Second Multicol',
                    },
                },
                'body': {
                    'rows': [
                        [i for i in range(6)],
                        [i for i in range(6)],
                        [i for i in range(6)],
                        [i for i in range(6)],
                        [i for i in range(6)],
                    ]
                },
            }
            filename = 'filename.pdf'
            template_name = 'path/to/template_name.pdf'
            
            context = {
                'date': date.today(), 
                'table': table, 
            }

            return render_to_pdf(
                request, 
                template_name, 
                context, 
                filename,
            )
    ```

    This would produce:

    <p align="center">
    <img src="https://github.com/bfrangi/vscode-django-tex/raw/main/media/example-pdf.png" />
    </p>

    </details>

-------------------------------------------------------------------

## Release Notes

### [Unreleased]
- No planned changes

### [0.0.1] - 2022-07-18

#### Added
- Initial working version of the extension by [@bfrangi](https://github.com/bfrangi/).

-------------------------------------------------------------------

## More

* View the extension in the **Visual Studio Marketplace** using [this](https://marketplace.visualstudio.com/items?itemName=bfrangi.vscode-django-tex#review-details) link.


-------------------------------------------------------------------

**Enjoy!**



[Unreleased]: https://github.com/bfrangi/vscode-django-tex/compare/v0.0.1...HEAD
<!-- [0.0.2]: https://github.com/bfrangi/vscode-django-tex/compare/v0.0.1...v0.0.2 -->
[0.0.1]: https://github.com/bfrangi/vscode-django-tex/releases/tag/v0.0.1

