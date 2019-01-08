# Changes to nbconvert templates for nice formatting

**Files located in:**
/Users/graham/anaconda3/lib/python3.6/site-packages/nbconvert/templates

**Reference**
http://www.markus-beuckelmann.de/blog/customizing-nbconvert-pdf.html

**Change in article.tplx**
documentclass[9pt]{article}
((* block author *))
\author{Group: Graham Chester, John Moran, Nicolas Maire}
((* endblock author *))

**Change in base.tplx**
geometry{verbose,tmargin=0.7in,bmargin=0.7in,lmargin=0.7in,rmargin=0.7in

**Change in document_contents.tplx**
adjustimage{max size={1.05\linewidth}{1.05\paperheight}}{((( filename )))
*then in bblock markdowncell:*
 \setlength{\parindent}{0cm}
 \setlength{\parskip}{1mm}

*then change line 27 to:*
\begin{Verbatim}[commandchars=\\\{\},fontsize=\small]

**Change in style_ipython.tplx**
*Replace line inside block input scoped with:*
 ((( custom_add_prompt(cell.source | highlight_code(strip_verbatim=True, metadata=cell.metadata), cell, 'In ', 'incolor') ))) 

*then add lines:*
((* macro custom_add_prompt(text, cell, prompt, prompt_color) -*))
    ((*- if cell.execution_count is defined -*))
    ((*- set execution_count = "" ~ (cell.execution_count | replace(None, " ")) -*))
    ((*- else -*))
    ((*- set execution_count = " " -*))
    ((*- endif -*))
    ((*- set indention =  " " * (execution_count | length + 7) -*))
\begin{Verbatim}[commandchars=\\\{\},fontsize=\small]
((( text | add_prompts(first='{\color{' ~ prompt_color ~ '}' ~ prompt ~ '[{\\color{' ~ prompt_color ~ '}' ~ execution_count ~ '}]:} ', cont=indention) )))
\end{Verbatim}
((*- endmacro *))
