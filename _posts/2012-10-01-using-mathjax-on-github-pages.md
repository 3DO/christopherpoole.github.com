---
layout: minimal_post
title: Using MathJax on Github:Pages
comments: True
---

[MathJax](http://www.mathjax.org) is a simple way of including Tex/LaTex/MathML based mathematics in HTML webpages.
To get up and running you need to include the MathJax script in the header of your github pages page, and then write some maths.
For LaTex, there are two delimiters you need to know about, one for block or displayed mathematics `\[ ... \]`, and the other for inline mathematics `\( ... \)`.

### Installation
You can find the MathJax documentation [here](http://www.mathjax.org/resources/docsindex/) however, to get up and running quickly, simply put this into the `<head>` section of the page you would like to display mathematics:

    <head>
    ...
        <script type="text/javascript"
                src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
        </script>
    ...
    </head>

If you are using jekyll, in `_config.yml` set
    
    markdown: kramdown

as `discount` for example automatically replaces `x^2` with `x<sup>2</sup>` which interrupts the MathJax rendering.

### Usage

Using it is pretty easy:

    Here is an example MathJax inline rendering \\( 1/x^{2} \\), and here is a block rendering: 
    \\[ \frac{1}{n^{2}} \\]

Here is an example MathJax inline rendering \\( 1/x^{2} \\), and here is a block rendering:
\\[ \frac{1}{n^{2}} \\]

The only thing to look out for is the escaping of the backslash when using markdown, so the delimiters become `\\[ ... \\]` and `\\( ... \\)` for inline and block maths respectively.
