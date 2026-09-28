# BACH Study Notes Template

A modular, pdfLaTeX-based template for assembling consistent first-year
Bachelor of Applied Computer Science notes. The example subject is Business
Processes.

## Project structure

- `main.tex` assembles the document and selects its subject and chapters.
- `preamble.tex` loads packages and configures document-wide behavior.
- `style.tex` centralizes colors, box styles, and code highlighting.
- `macros.tex` defines metadata commands, chapter logic, and the content API.
- `subjects/business-processes/subject.tex` contains subject metadata.
- `subjects/business-processes/chapter-01.tex` and `chapter-02.tex` contain sample notes.
- `assets/` is the place for figures and other local resources.

## Create another subject

1. Copy `subjects/business-processes/` to a new subject folder.
2. Update the metadata in its `subject.tex`; code, academic year, and author can be left blank.
3. Create chapter files using `\chaptertopic{Chapter title}` and add their content.
4. In `main.tex`, input the new `subject.tex` before `\begin{document}`, then replace the sample chapter inputs with your new chapter files.
5. Keep all note content in the subject/chapter files; change presentation in `style.tex` or shared behavior in `macros.tex`.

## Compile

Run pdfLaTeX twice from the project directory so the table of contents and cross-references settle:

```sh
pdflatex main.tex
pdflatex main.tex
```

The template uses `listings`, so code highlighting works without `-shell-escape`. Required LaTeX packages include `lmodern`, `microtype`, `geometry`, `amsmath`, `graphicx`, `float`, `booktabs`, `tabularx`, `array`, `enumitem`, `titlesec`, `xparse`, `xstring`, `xcolor`, `textcomp`, `tcolorbox`, `listings`, `fancyhdr`, and `hyperref`.

## Content macro reference

- `\subject{...}`, `\subjectcode{...}`, `\academicyear{...}`, `\authorname{...}` set optional metadata.
- `\chaptertopic{...}` creates the next automatically numbered chapter and resets chapter-scoped question and definition counters.
- `\begin{learningobjectives} ... \item ... \end{learningobjectives}` creates an objectives block.
- `\definition{Term}{Text}` or `\definition[label]{Term}{Text}` creates a numbered, referenceable definition box.
- `\begin{questionlist} ... \end{questionlist}` contains numbered questions. Use `\q{Question}` or `\q[label]{Question}`; labels reference the chapter.question value with `\ref`.
- `\qa{Question}{Answer}` and `\qa[label]{Question}{Answer}` add a less prominent answer. `\answer{...}` can follow a `\q` directly.
- `\examquestion{Question}` and `\examquestion[label]{Question}` create a subtly emphasized exam question inside a question list. `\examqa{Question}{Answer}` also adds an answer.
- `\keyconcept{Term}{Text}`, `\important{Text}`, `\note{Text}`, and `\example{Title}{Text}` create distinct, consistent content boxes.
- `\term{Text}` highlights a term inline.
- `\begin{summarybox} ... \end{summarybox}` formats a chapter summary.
- `\begin{codeblock}{Python} ... \end{codeblock}` formats source code. Supported names: `C\#`, `CSharp`, `JavaScript`, `TypeScript`, `Python`, `SQL`, `HTML`, `CSS`, `Bash`.

Definitions, answers, and box contents can include ordinary LaTeX content, including paragraphs, lists, and equations. Question commands and exam-question commands belong inside `questionlist`.

## Figures, tables, and lists

Figures use ordinary `figure` and `\includegraphics` commands; `graphicx` and `float` are loaded (so `[H]` is available). Store image files in `assets/` and reference them from `main.tex`'s directory, for example `assets/process-model.png`. Use `tabularx` with `booktabs` for tables; `itemize` and `enumerate` have compact, readable default spacing.

## Styling

Edit the color definitions and shared `tcolorbox`/`listings` styles in `style.tex` to update the visual theme. `macros.tex` controls the structure and public command behavior; `preamble.tex` controls package loading, page geometry, links, and headers/footers.
