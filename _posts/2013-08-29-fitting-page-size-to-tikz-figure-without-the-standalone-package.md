---
layout: minimal_post
title:  Fitting page size to TIKZ figure size without the standalone package 
comments: True
introduction: I found myself without access to the standalone LaTex package, this is how you fit a TIKZ page size to the figure size without it.
---

We need the `preview` LaTeX package where we specify a tight page and specify the tikzpicture as the preview:

    \usepackage[active,tightpage]{preview}
    \PreviewEnvironment{tikzpicture}
    \setlength\PreviewBorder{5pt}

That is it.
A full document might look like this:

    \documentclass{article}

    \usepackage{tikz}

    \usepackage[active,tightpage]{preview}
    \PreviewEnvironment{tikzpicture}
    \setlength\PreviewBorder{5pt}

    \begin{document}
        \begin{tikzpicture}
            \draw [dashed,color=gray] (0, 0) circle (5cm);
        \end{tikzpicture}
    \end{document}

